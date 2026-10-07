作成日: 2026-10-07 / STATUS: INFO / TOPIC: HERMES

# 構築手順:セキュリティ一次情報とクラウド人気記事の週次調査cron(4本)

- **記録日:** 2026-10-07(同日に、クラウドブログ週報を3本へ分解して追記)
- **位置づけ:** Prime(Hermes Agent上のアシスタント)に、毎週の情報収集ジョブを2本追加した記録です。「HackerNewsだけでは一次情報が足りない」という問題意識(セカンドオピニオン)から、情報源を広げました。
- **公式ドキュメント:** Hermes https://hermes-agent.nousresearch.com/docs / CISA KEV https://www.cisa.gov/known-exploited-vulnerabilities-catalog / JPCERT/CC https://www.jpcert.or.jp/ / Zenn・Qiita APIは本文末尾の出典を参照
- **マスキング:** ホスト名・IP・ユーザ名・各種IDは`<...>`または`~/`に置換。機密値は記載しない。

## 0. 先に結論(3行)

1. **cronを追加した。** 水曜03:30 = CISA/JPCERT(脆弱性の一次情報)。クラウド系は、当初「統合版1本」(土曜)で作ったが、同日に **3本へ分解**(金=公式ブログ、日=Zenn、火=Qiita。いずれも03:30)。統合版は停止して残してある(§10)。
2. **「取得はスクリプト、文章化はLLM」の分業にした。** 依存ゼロのNodeスクリプトが公式フィード/APIから集め、cron(LLM)は要約・採点・公開だけを担う。
3. **既存cronと同一分で重ならない。** 同時刻に走るLLMジョブは0件(検証済み)。

## 1. 全体像

```mermaid
flowchart LR
  subgraph SRC["公式の公開フィード/API"]
    A1["CISA KEV JSON"]
    A2["CISA アドバイザリ RSS"]
    A3["JPCERT/CC RSS"]
    B1["クラウド4社 公式ブログ RSS"]
    B2["Zenn API"]
    B3["Qiita API v2"]
  end
  SC1["fetch-cisa-jpcert.mjs"]
  SC2["fetch-cloud-blogs.mjs"]
  A1 --> SC1
  A2 --> SC1
  A3 --> SC1
  B1 --> SC2
  B2 --> SC2
  B3 --> SC2
  SC1 --> J1["out/latest-week.json"]
  SC2 --> J2["out/latest-week.json"]
  J1 --> C1["cron: weekly-cisa-jpcert-security<br/>水 03:30"]
  J2 --> C2["cron: weekly-cloud-techblogs<br/>土 03:30"]
  C1 --> D1["NVDでCVSS照会 + OWASP推定"]
  D1 --> OUT1["docs/info/security/cisa-jpcert/"]
  C2 --> OUT2["docs/info/news/"]
  OUT1 --> GH["GitHub public-hermes-01"]
  OUT2 --> GH
  OUT1 --> VW["社内ドキュメントビューア"]
  OUT2 --> VW
```

## 2. 追加したもの一覧(追加のみ・既存変更なし)

| 種別 | パス/名前 | 内容 |
|---|---|---|
| スクリプト | `~/optimus/tasks/cisa-jpcert/fetch-cisa-jpcert.mjs` | CISA KEV・CISA RSS・JPCERT RSSを取得し、直近7日をJSON化 |
| スクリプト | `~/optimus/tasks/cloud-blogs/fetch-cloud-blogs.mjs` | 公式ブログ(4社)+Zenn/Qiitaの人気記事をJSON化 |
| cron | `weekly-cisa-jpcert-security` | 毎週水曜 03:30(`30 3 * * 3`) |
| cron | `weekly-cloud-techblogs` | 毎週土曜 03:30(`30 3 * * 6`) |
| 出力先 | `docs/info/security/cisa-jpcert/` | CISA/JPCERT週報 |
| 出力先 | `docs/info/news/` | クラウドブログ週報(HackerNews週報と同じ場所) |

既存のスクリプト・cron・設定ファイルは**一切書き換えていない**。

## 3. 設計の要点

### 3.1 なぜ「スクリプト+LLM」の分業か
- LLMにWebを直接読ませると、ページ構造の変化で壊れやすく、トークンも食う。
- 公式のRSS/JSON APIをスクリプトで取れば、**同じ入力から同じJSONが出る**(再現性が高く、検証しやすい)。
- 方式は既存の`al2023-security`(ALAS取得スクリプト+cron)と同じ。依存は**Node標準の`fetch`のみ**(npmパッケージなし)。

### 3.2 状態を持たない(冪等)
差分スナップショットではなく「**日付が直近7日以内**」で絞る。再実行しても同じ結果になり、状態ファイルの破損リスクがない。

### 3.3 失敗時の挙動
- 1つの情報源だけ失敗 → 取れた分で記事を作り、末尾に「取得できなかった情報源」を明記。
- 全て失敗 → 記事を作らず`[CRON_FAILURE]`を出力して終了(スクリプトはexit 1)。
- 取得は指数バックオフで再試行(403/429/5xxのみ)。

### 3.4 脆弱性スコア併記ルールの適用
CISA/JPCERT週報には、恒久ルール(2026-10-04確定)に従い、各CVEに**CVSS(NVD公式値、Primary/Secondary明記)**と**OWASP(Risk Rating推定+Top10:2025対応)**を併記する。cronのskillに`vulnerability-scoring-cvss-owasp`を指定して読み込ませた。NVDはレート制限があるため1件ごとに6秒空け、最大20件。
クラウドブログ週報は「ブログ紹介」でありCVE採点はしない(脆弱性の話題はCISA/JPCERT週報へ誘導)。

## 4. 情報源と、取れなかったもの

実際にHTTPで取得できるかを1つずつ検証してから採用した。

### 採用
- **CISA:** KEV JSON(悪用が確認された脆弱性)、アドバイザリRSS(Alert・ICS等)
- **JPCERT/CC:** RSS(注意喚起と週報が同じフィードに入る。IDが`at`始まりが注意喚起)
- **クラウド公式:** Google Cloud(日本語/英語)、AWS(日本語ブログ・News・Architecture・Security・What's New)、Microsoft(Azure Blog・DevBlogs・Security Blog)、Cloudflare(日本語/英語)
- **コミュニティ:** Zenn公開API(`/api/articles?topicname=…&order=latest&count=100`)、Qiita API v2(`tag:…` と `created:>=日付`)

### 不採用/制約(失敗の記録)
| 候補 | 結果 | 理由 |
|---|---|---|
| Microsoft日本語の公式ブログ | 不採用 | 日本マイクロソフトのニュースは2025年9月で更新停止、DevBlogs日本語版は404 |
| Google Security Blog | 不採用 | 最新が4月で更新停止 |
| Zennの企業Publication別フィード、Qiita Organization別フィード | 不採用 | 多くが404(AWS Japan等) |
| Qiita API(認証なし) | 制約あり | 1回100件まで。AWSタグは100件に達するため「上位100件から選定」と注記 |
| Microsoft Security Response Center(MSRC)ブログ | 保留 | RSSの形式が想定と違い、件数を取れなかった |

## 5. 構築手順(再現用)

> 書き込み系は承認(HITL)を得て実施した。以下は再現のための手順であり、実値は含まない。

1. **取得スクリプトを作成**(`~/optimus/tasks/<名前>/fetch-*.mjs`)。`node --check`で構文確認。
2. **実データで検証:** 正常系(件数・先頭の内容)、異常系(不正URLで1フィード失敗しても全体が出力される)、`--days 30`で件数が増えること。
3. **cronを作成**(`cronjob`ツール)。ポイント:
   - `workdir`を`~/optimus`に固定
   - `enabled_toolsets`は`terminal`・`file`・`github-mcp`のみ(最小権限)
   - CISA/JPCERT側のみ`skills`に`vulnerability-scoring-cvss-owasp`
4. **モデルをccproxy経由・最新に統一:**
   `hermes cron edit <job_id> --model claude-sonnet-5-5 --provider anthropic-ccproxy`
   (理由は030番を参照。`cronjob`ツールの`update`では、provider単独の指定ができない)
5. **スケジュールの重なり検証:** `jobs.json`を読み、LLMジョブの同一分重なりが0件であることを確認。
6. **試験実行(`cronjob action=run`)→ 記事の中身を元データと突き合わせ**(KEVのCVE網羅、NVDへの独立再照会、機微情報の検査)。

## 6. スケジュールの設計

既存cronに合わせつつ、LLMジョブ同士が同一分に重ならないようにした。

| 曜日 | 時刻(JST) | ジョブ |
|---|---|---|
| 日 | 01:30 | al2023-security |
| 月 | 01:30 / 03:00 | hackernews / claude-automation-knowledge |
| 火 | 01:30 | aws-automation-knowledge |
| 水 | 02:00 / **03:30** | claude-cli-autoupdate / **cisa-jpcert-security(新)** |
| 木 | 01:30 / 02:00 / 02:30 | hackernews / windows-update-security / megatech-outage-report |
| 金 | 01:30 | github-trending |
| 土 | 02:00 | hermes-autoupdate-notify(`cloud-techblogs`は停止) |
| 金 | 01:30 / **03:30** | github-trending / **cloud-hot-official(新・§10)** |
| 日 | 01:30 / **03:30** | al2023-security / **cloud-hot-zenn(新・§10)** |
| 火 | 01:30 / **03:30** | aws-automation-knowledge / **cloud-hot-qiita(新・§10)** |

- 当初は火曜03:30で作成したが、**水曜に変更**(ご指示)。水曜は02:00のあと1時間30分空く。
- 毎時:00のスクリプト系(LLMなし)とは分がずれている。

## 7. 試験実行の結果

- **CISA/JPCERT週報:** 4分24秒で完了。KEV 5件・CISA 17件・JPCERT 16件が元データと一致。CVSSはNVDへ独立に再照会して一致を確認。GitHubへpush済み。
- **クラウドブログ週報:** 2分53秒で完了(エラーなし)。取得は公式182件・Zenn 32件・Qiita 32件で、記事の構成(ハイライト・今週これだけ読む3本・公式4社・Zenn・Qiita・見方・出典)がすべてそろった。GitHubへpush済み。
  - **機微情報:** 検査で0件。
  - **著者名の扱い:** 本文に個人の著者名は出ていない。QiitaのURLのパスにはユーザーIDが含まれるが、これは記事URLの仕様であり、許容とした(本文での著者名記載の禁止は守られている)。
  - **URLの照合:** 記事内のURLのうち、データ外だったものは各社ブログの一覧ページ(出典欄)のみで、記事のURLの創作はなかった。

## 8. 運用上の注意

- **Qiita/Zennの個人の著者名は記事に載せない**(プロンプトで禁止)。タイトルとURLのみ。公式・企業アカウントは可。
- **いいね数は「取得時点の人気の目安」**で、正確性の保証ではない旨を記事に注記させている。
- **情報源は変わる:** フィードの廃止・URL変更があり得る。`errors`が続く場合はスクリプトの`VENDORS`定義を直す。
- **モデル更新時:** cronの`model`は固定。新モデルへ移行するときは030番の手順で各cronを更新する(今回の2本も対象)。

## 9. 次の改善候補(未実施)

- 試験結果を踏まえた、プロンプトの調整(記事の長さ・ノイズ除去)
- 重大なKEV追加があった日だけDiscordへ通知する、軽量な`monitor`方式(LLMを起動しない)
- JVN・IPA・EPSS(悪用確率)の追加

## 10. 追記:クラウド週報を「サイト別の人気記事」3本へ分解(2026-10-07)

### 10.1 経緯と判断
統合版(`weekly-cloud-techblogs`)は「新着の紹介」が中心で、**何が本当に人気・ホットか**が分かりにくかった。そこで、サイト別に人気指標を付けて3本へ分解した。cronを増やしすぎない方針のため、6本(1社1本)ではなく**3本**(公式4社・Zenn・Qiita)を選んだ。

### 10.2 追加したもの

| 種別 | 名前 | スケジュール(JST) | 内容 |
|---|---|---|---|
| cron | `weekly-cloud-hot-official` | 金 03:30 | 公式ブログ4社の人気記事 |
| cron | `weekly-cloud-hot-zenn` | 日 03:30 | Zennの人気記事 |
| cron | `weekly-cloud-hot-qiita` | 火 03:30 | Qiitaの人気記事 |
| スクリプト | `~/optimus/tasks/cloud-hot/fetch-hot.mjs` | - | `--source official|zenn|qiita` で3系統を切替(依存ゼロ) |
| 出力先 | `docs/info/news/` | - | `<日付>_INFO_CLOUDHOT_<official|zenn|qiita>-hot-weekly.md` |
| 停止 | `weekly-cloud-techblogs`(統合版) | - | 削除せず**停止**(`resume`で復元可能) |

### 10.3 「人気」の測り方(すべて無料の公式API、取得を検証済み)

| 対象 | 指標 | 補足 |
|---|---|---|
| 公式ブログ4社 | はてなブックマーク数 + Hacker News(HN)のポイント | 合計の大きい順。日本語圏と海外の両方の反応が見える。公式ドメインがHNで話題になったが、RSSに載っていない記事も別枠で拾う |
| Zenn | 公式の週間トレンド + 直近7日の新着をいいね順 | 2つのリストは重複するため、記事側で重複を除く |
| Qiita | ホット(直近7日のいいね+ストック順) + 定番(直近30日でストック20以上) | 認証なしは1回100件まで。3ページ(300件)まで走査し、上限に達したら注記 |

- **公式ブログの人気を測る手段:** 公式RSSには、いいね数のような指標がない。そのため、外部の反応(はてブ・HN)で代用した。
- **Microsoftは指標が付きにくい:** 14件中、指標ありは1件。はてブにもHNにも載りにくいため。その場合、記事は「今週は反響の大きい記事なし」+新着の主なものを書く設定。
- **HN検索の注意:** 記事URLでの個別検索は、ほぼヒットしなかった(8件中0件)。**ドメイン検索で直近の投稿を取り、URLを正規化して突き合わせる**方式に変えて、ヒットするようになった。

### 10.4 試験実行の結果(3本とも成功)

| ジョブ | 所要 | 記事サイズ | 検証 |
|---|---|---|---|
| official | 約2分 | 約9KB | 機微0件、データ外URL 0件、はてブ・HNの数値が元データと全件一致 |
| zenn | 約2分 | 約7KB | 機微0件、本文の著者ID 0件、データ外URLなし(トピックの一覧ページのみ) |
| qiita | 約2分 | 約10KB | 機微0件、本文の著者ID 0件、いいね・ストック数が元データと不一致0件 |

- **確認した記述:** Zenn記事の「AWS公式Japanアカウント」は、記事が`aws_japan`のパブリケーション(企業の公式ページ)に載っていることをURLで確認した。事実と合致。
- **初回のデータ(参考):** Cloudflareの新製品発表がHNで641ポイント。AWSのAurora PostgreSQL関連が、はてブ20。

### 10.5 作成手順(再現用)
1. 人気指標の取得を、`curl`相当で1つずつ検証してから採用(はてブ一括API、HN Algolia、Zenn API、Qiita API)。
2. スクリプトを作成し、3系統+異常系(引数なしは使い方を表示して終了、exit 2)を確認。
3. cronを`hermes cron create`で作成。ポイント:
   `--workdir ~/optimus --model claude-sonnet-5-5 --provider anthropic-ccproxy --pin --deliver discord`
   (`enabled_toolsets`はCLIで指定できないため、作成後に`cronjob`ツールのupdateで`terminal`・`file`・`github-mcp`に設定)
4. 統合版を`pause`(削除しない)。
5. 3本を手動実行し、記事を元データと突き合わせて検証。

### 10.6 復元方法(統合版に戻す場合)
- 分解版の3本を停止し、`weekly-cloud-techblogs`を`resume`する(`~/optimus/tasks/cloud-blogs/`のスクリプトは残してある)。

### 10.7 今後の改善候補(未実施)
- 週ごとの比較(先週との差分、継続して人気の記事)
- はてブ・HNに載らないMicrosoftの扱い(Microsoft Learnの更新情報など別指標の検討)

## 出典

- CISA KEV: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリRSS: https://www.cisa.gov/cybersecurity-advisories/all.xml
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- NVD API: https://nvd.nist.gov/developers/vulnerabilities
- Zenn API: https://zenn.dev/api/articles
- Qiita API v2: https://qiita.com/api/v2/docs

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
