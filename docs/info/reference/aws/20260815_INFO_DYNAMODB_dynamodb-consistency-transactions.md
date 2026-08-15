# DynamoDB 整合性モデルとトランザクション設計ガイド

> **対象**: Amazon DynamoDB の「結果整合性」「強整合性」「トランザクション」の違いを理解し、適切に使い分けたい人向け。
> **作成日**: 2026-08-15（JST） / **ステータス**: INFO（情報提供・設計リファレンス）
> **一次情報**: [DynamoDB read consistency（AWS公式）](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html)、[Amazon DynamoDB Transactions（AWS公式）](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/transaction-apis.html)
> **元記事**: public2リポジトリ `dynnamodb/dynnamodb.md` を再構成（内容はweb_searchで裏取りし加筆修正）

---

## 用語ミニ解説（初心者向け）

- **DynamoDB**: AWSが提供するフルマネージドNoSQLデータベース。JOIN（複数テーブルの結合）をサポートせず、キー（パーティションキー／ソートキー）でのアクセスに最適化されている。
- **RCU（Read Capacity Unit）**: DynamoDBの読み取り性能単位。強整合性読み取りは結果整合性読み取りの2倍のRCUを消費する。
- **GSI（Global Secondary Index）／LSI（Local Secondary Index）**: 主キー以外の項目で検索するための補助インデックス。
- **N+1問題**: 1件の親データ取得後、関連する子データをN回の個別クエリで取得してしまい、合計N+1回のクエリが発生する非効率なアクセスパターン。RDB（リレーショナルDB）由来の概念だが、DynamoDBのような正規化されたテーブル構成でも起こりうる。

---

## 1. 結果整合性（Eventually Consistent Read）

DynamoDBの**デフォルトの読み取りモード**。書き込み直後は複数のレプリカ（複製）間でまだ同期が完了していない可能性があり、ごく短時間だけ古いデータが返る可能性がある。

```bash
aws dynamodb get-item \
  --table-name MyTable \
  --key '{"UserId": {"S": "user123"}}'
```

`--consistent-read` を指定しなければ結果整合性になる。

| 向いているユースケース | 理由 |
|---|---|
| 商品一覧・レビュー数などの表示 | 数秒の遅延が許容できる |
| 高スループットが必要な読み取り | RCU消費が強整合性の半分で済む |

## 2. 強整合性（Strongly Consistent Read）

直前の書き込みを必ず反映した最新データを取得するモード。`--consistent-read` を明示指定する。

```bash
aws dynamodb get-item \
  --table-name MyTable \
  --key '{"UserId": {"S": "user123"}}' \
  --consistent-read
```

| 向いているユースケース | 理由 |
|---|---|
| 残高確認直後の送金処理 | 直前の書き込みを確実に反映する必要がある |
| 認証・認可のロール確認 | 権限変更を即時反映したい |

> ⚠️ **公式仕様の確認事項**: 強整合性読み取りはGSI（グローバルセカンダリインデックス）に対しては利用できない（GSIは常に結果整合性）。また、強整合性読み取りはリージョンをまたぐグローバルテーブルでは提供されない。設計時は [AWS公式ドキュメント](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html) で最新の制約を必ず確認すること。

## 3. トランザクション（TransactWriteItems / TransactGetItems）

複数テーブル・複数アイテムにまたがる操作を「全部成功」か「全部ロールバック」で実行するAPI。

### 書き込みトランザクション例

```bash
aws dynamodb transact-write-items \
  --transact-items '[
    {
      "Put": {
        "TableName": "Orders",
        "Item": {"OrderId": {"S": "order123"}, "Status": {"S": "Pending"}}
      }
    },
    {
      "Update": {
        "TableName": "Inventory",
        "Key": {"ProductId": {"S": "item456"}},
        "UpdateExpression": "SET Stock = Stock - :qty",
        "ExpressionAttributeValues": {":qty": {"N": "1"}},
        "ConditionExpression": "Stock >= :qty"
      }
    }
  ]'
```

在庫を条件付きで減算しつつ注文を作成する例。在庫不足なら `ConditionExpression` の条件を満たさずトランザクション全体が失敗する。

| ユースケース | 説明 |
|---|---|
| 複数テーブルの整合性 | 注文と在庫を同時更新するなど |
| 条件付き更新 | 在庫が十分な場合のみ注文確定 |
| 同時実行制御 | 他の処理との競合防止（ConditionCheck） |

### 一貫性・コスト比較

| 処理 | 一貫性 | コスト | ユースケース |
|---|---|---|---|
| 結果整合性 | 遅延あり | 低 | 一覧表示・非同期処理 |
| 強整合性 | 即時反映 | 高（RCU2倍） | 状態確認・認証・制御 |
| トランザクション | 複数操作の原子性 | 高 | 複数テーブル更新・条件付き処理 |

---

## 4. N+1問題とテーブル設計のベストプラクティス

DynamoDBはJOINをサポートしないため、正規化された複数テーブル構成にすると「親データ取得→子データを個別に複数回取得」というN+1問題が発生しやすい。

### 対策

| 対策 | 内容 |
|---|---|
| 非正規化 | よく一緒に使うデータを1アイテムに埋め込む |
| シングルテーブル設計 | 複数エンティティを1テーブルに統合し、PK/SKとGSIでアクセスパターンを制御 |
| BatchGetItem | 複数キーをまとめて取得し、クエリ回数を削減 |
| アグリゲーション事前計算 | 集計値を都度計算せず別項目として保持 |

> DynamoDBの設計思想は「アクセスパターンを先に洗い出し、それに合わせてスキーマを決める」という**アクセスパターン駆動設計**。RDBの「正規化してからJOINで結合する」発想とは逆になる点に注意。

### BatchGetItem 実装例（Python/boto3）

```python
import boto3

dynamodb = boto3.client('dynamodb')

response = dynamodb.batch_get_item(
    RequestItems={
        'UsersTable': {
            'Keys': [
                {'UserId': {'S': 'user1'}},
                {'UserId': {'S': 'user2'}}
            ],
            'ProjectionExpression': 'UserId, Name, Email'
        }
    }
)
users = response['Responses'].get('UsersTable', [])
```

> ⚠️ 最大100アイテム・合計16MBまでの制約あり。`UnprocessedKeys` が返る場合はリトライ処理が必要（スロットリング対策）。

---

## 5. DAX（DynamoDB Accelerator）による読み取り高速化

DAXはDynamoDBの前段に置くインメモリキャッシュ層。

| API | DAXとの相性 |
|---|---|
| `GetItem` | 最も効果的 |
| `Query` | 結果をキャッシュ可能 |
| `Scan` | 非推奨（キャッシュ効果が薄くRCU消費が大きい） |

ベストプラクティス: GetItem/Query中心の設計にする、TTL付きキャッシュで整合性とパフォーマンスを両立する、Scanは避けてGSI設計でQueryに変換する。

---

## 6. 分散トランザクション設計の考え方（応用）

DynamoDBは単一リージョン内でのACIDトランザクションをサポートするが、マルチリージョンや外部システムとの整合性が必要な場合は自前で設計する必要がある。

- **2フェーズコミット的なパターン**: `ConditionExpression` を使った条件付き書き込みで「準備（Prepare）」を表現し、全テーブルが成功した場合のみ「確定（Commit）」を行う擬似的な2段階処理。
- **Step Functions + Lambda**: 中間状態（Prepared等）をDynamoDBやS3に保持し、タイムアウト時に自動ロールバックする設計はAWS上での実用パターン。
- **冪等性の確保**: `TransactWriteItems` には `ClientRequestToken` を指定することで、リトライ時の二重実行を防止できる（AWS公式が提供する冪等化の仕組み）。

---

## まとめ

- 結果整合性はデフォルトかつ低コスト。強整合性は明示指定が必要で、GSIには使えない点に注意。
- トランザクションは複数アイテム・複数テーブルの原子性を保証するが、コストは高め。
- N+1問題対策の基本は「非正規化＋シングルテーブル設計＋BatchGetItem」。RDB的な正規化思考は持ち込まない。
- 読み取りを高速化したいならDAX（ただしScanには不向き）。
- 分散トランザクションが必要な場合はStep Functions等と組み合わせ、冪等性（ClientRequestToken）を必ず設計に組み込む。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
