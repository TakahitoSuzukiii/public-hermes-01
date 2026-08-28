# info画面「Hermes（構築手順）」カテゴリが0件表示されるバグの修正

> ステータス: DONE / カテゴリ: SETUP / 実施日 2026-08-13
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP 等は placeholder。
> 関連: `001`（NEXUSホーム移行）

## 0. 背景・症状

`https://<hostname>/info#cat=security` のようなinfo画面(タスクボードWebアプリの構築手順・ナレッジ閲覧機能)で、`docs/hermes/`配下に新規記事(`005_DONE_SETUP_ccproxy-api-pro-max-billing-workaround.md`)を追加したにもかかわらず、画面に反映されていないと鈴木さんから報告があった。

調査の結果、症状は当該記事に限らず「⚙️ Hermes（構築手順）」カテゴリ自体が **常に0件** と表示される状態だったことが判明。

## 1. 原因

`task-board/public/info.html` 内のカテゴリ判定関数 `categorize(path)` が、記事パスのプレフィックスで振り分けを行っている:

```js
function categorize(path){
  if(path.startsWith('docs/info/news/'))     return 'news';
  if(path.startsWith('docs/info/security/')) return 'security';
  if(path.startsWith('docs/openclaw/'))      return 'openclaw';  // ← 旧パス
  if(path.startsWith('docs/info/research/')) return TOPIC_CAT[topicOf(path)] || 'techresearch';
  return null;
}
```

`docs/openclaw/` という**OpenClaw時代の旧パス**のままになっており、2026-08-09の「NEXUSホーム → Optimus Task Board」移行（`001_DONE_SETUP_nexus-to-optimus-taskboard-migration.md`参照）で構築手順ドキュメントの実体が `docs/hermes/` に切り替わった際、この判定条件だけ追従していなかった。該当ディレクトリ以下の記事は `categorize()` が `null` を返すため、どのカテゴリにも属さず一覧から漏れていた。

## 2. 対応（追加のみ・デグレ無し）

```diff
   if(path.startsWith('docs/openclaw/'))      return 'openclaw';
+  if(path.startsWith('docs/hermes/'))        return 'openclaw'; // 2026-08-09 OpenClaw→Hermes移行でdocs/hermes/に配下変更。カテゴリkeyは互換のため'openclaw'のまま(追加のみ・デグレ無し)。
```

- 既存の `docs/openclaw/` 判定行は削除せず残置（互換性維持）。
- カテゴリの内部key（`openclaw`）、表示ラベル（`⚙️ Hermes（構築手順）`）は変更せず、パス判定だけを追加。
- `info.html` は `task-board/src/infra/infoDocs.mjs` によりローカルファイルシステム（`~/optimus/docs/`配下）を直接再帰列挙する方式のため、GitHubへのpushは反映に不要（サーバ上のローカルファイルが正）。静的ファイル配信のためサーバ再起動も不要、ブラウザのハードリロードのみで反映された。

## 3. 検証

### 3.1 反映確認
- 修正前: `#cat=hermes` → 「⚙️ Hermes（構築手順） 0 件」
- 修正後: `#cat=hermes` → 「⚙️ Hermes（構築手順） 5 件」（`docs/hermes/`配下の全5記事が表示、`005`のccproxy-api記事も含む）

### 3.2 全体整合性チェック（同期漏れの横展開確認）

ローカル `docs/` 配下の `.md` 総数と、info画面の全カテゴリ件数合計を突き合わせ、他に漏れがないか確認した。

| ローカルディレクトリ | ファイル数 |
|---|---|
| `docs/info/news/` | 22 |
| `docs/info/security/` | 27 |
| `docs/info/research/` | 74 |
| `docs/hermes/` | 5 |
| **合計** | **128** |

| info画面カテゴリ | 件数 |
|---|---|
| News | 22 |
| Tech（techresearchフォールバック） | 25 |
| Design | 8 |
| Cloud | 14 |
| GenAI | 14 |
| ML | 3 |
| Security | 27 |
| Hermes（構築手順） | 5 |
| Health | 2 |
| Finance | 1 |
| SelfDev | 5 |
| Other | 2 |
| **合計** | **128** |

完全一致を確認。`docs/info/research/`配下の各記事は `TOPIC_CAT` マッピング表（`info.html`内）で未登録のTOPICでも `techresearch` にフォールバックする設計のため、今回のような「カテゴリ丸ごと0件化」は `docs/openclaw/`→`docs/hermes/` のケースのみで、他に同種の漏れは無いことを確認した。

## 4. 教訓・再発防止

- ディレクトリ構成を変更する移行作業（今回のOpenClaw→Hermes等）を行う際は、**そのディレクトリを参照している全箇所**（今回で言えば `info.html` のカテゴリ判定ロジック）を洗い出してから着手する。移行ドキュメント（`001_DONE_SETUP_...`）作成時に「影響範囲チェックリスト」を含めるとよい。
- 新規カテゴリ・新規ディレクトリを追加する際は、`docs/` 配下のファイル総数とinfo画面の表示件数合計を突き合わせる簡易チェックを、今後の同種修正時にも実施する。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
