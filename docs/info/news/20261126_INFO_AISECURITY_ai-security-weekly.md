作成日: 2026-11-26 / STATUS: INFO / TOPIC: AISECURITY / 対象期間: 2026-11-19〜2026-11-26

# AI・AIエージェント セキュリティ週次ウォッチ（2026-11-26）

## 📌 今週のハイライト
- 「悪用が確認されている（KEV）」AI関連の脆弱性は今週**0件**。
- 最大の話題は **MCP（Model Context Protocol＝AIと外部ツールをつなぐ共通規格）サーバ**の脆弱性が多数出たこと。認証なしで遠隔操作できるもの（ruflo、Jupyter MCP Server）が目立つ。
- Microsoft 365 Copilot に CVSS 9.9 の権限昇格（CVE-2026-50691）。
- Hermes Agent（Nous Research）にも脆弱性（CVE-2026-130164、ローカル攻撃・条件付き）。
- NVDで「AIキーワード」に引っかかった誤ヒット57件は除外済み。

## 🚨 まず見る（悪用確認・緊急）
**KEV（悪用確認済み）: 今週は該当なし。** 以下は「認証不要・遠隔・高スコア」の案件。

### 1. ruflo（npm）MCPブリッジ — 認証なしでリモートコード実行
- 製品: ruflo の Docker Compose 既定構成に含まれる MCPブリッジ。
- 条件: 既定のまま公開（`POST /mcp` が認証なし）。ネットワークから到達できること。
- 攻撃者にできること: 認証なしで `terminal_execute` ツールを呼び、ブリッジのコンテナ内で任意コマンド実行（RCE＝遠隔コード実行）。
- CVSS: 10.0 CRITICAL（GitHub Advisory採点、版は未確認）。CVE-2026-59726 / GHSA-c4hm-4h84-2cf3。
- OWASP Risk Rating（推定・技術面のみ）: 尤度 HIGH × 影響 HIGH ⇒ Critical。OWASP Top10:2025: A07 Authentication Failures 相当（認証欠如。筆者の見立て）。
- 対処: 修正版へ更新（GHSA記載の修正版を確認）。暫定策は公開ポートを閉じる／ローカル(127.0.0.1)のみにバインド／前段に認証を置く。

### 2. Jupyter MCP Server（pip）— 悪意あるWebサイトからJupyterを乗っ取り
- 条件: standalone の streamable-http モード、1.0.3 未満。ユーザーが悪意あるサイトを開く（DNSリバインディング＝名前解決を偽装してローカルのサービスに到達させる手口）。管理用 `/api/connect` `/api/stop` に Host/Origin 検証がない（CVE-2026-77359）。
- 追加: 同じ管理ルートが認証なしで叩ける問題（CVE-2026-77318、CVSS 4.0 7.3 HIGH）。
- 攻撃者にできること: 接続先 runtime_url を差し替え、Jupyterバックエンドを乗っ取る。
- CVSS: CVE-2026-77359 は 9.3 CRITICAL（CVSS 4.0、NVD掲載値、状態「Received」＝NVD未精査でCNA採点）。
- OWASP Risk（推定）: 尤度 MEDIUM〜HIGH × 影響 HIGH ⇒ High。Top10:2025: A01 Broken Access Control／A07（CWE-350/306、筆者の見立て）。
- 対処: **1.0.3 以上へ更新**。暫定策: standalone HTTPモードを使わない、localhost以外に公開しない。

### 3. Microsoft 365 Copilot — 権限昇格（クラウド側）
- CVE-2026-50691、CVSS 9.9 CRITICAL（3.1、NVD掲載）。要ログイン（PR:L）なので「認証不要」ではないが高スコアのため掲載。
- 内容: 不適切な認可（CWE-285）により、認可済みユーザーがネットワーク経由で権限を昇格できる。
- OWASP Risk（推定）: 尤度 MEDIUM × 影響 HIGH ⇒ High。Top10:2025: A01。
- 対処: 詳細・修正はMicrosoft側（クラウドサービスのため通常は利用者の操作不要。筆者の見立て。公式のCVEページで確認を）。

## 🛠 AI基盤・ツールの脆弱性（CVE/GHSA）
スコアは取得時点のNVD/GitHub掲載値。多くは NVD 状態が「Received/Awaiting Analysis」で、採点は発行元(CNA)によるもの。OWASP Riskはすべて**推定（技術面のみ）**。

1. **mcp-ssh-manager（3.8.5未満）** CVE-2026-129995／CVSS 3.1 8.8 HIGH／OWASP: 尤度MED×影響HIGH⇒High／A05 Injection。バックアップ系ツールがシェルコマンドを入力値から組み立てるためOSコマンド注入。→ 3.8.5以上へ。
2. **SurrealDB MCPサーバ（3.1.0〜4.0.0未満）** CVE-2026-134293／CVSS 4.0 8.8 HIGH／High／A05。識別子検証の不備によるSQLインジェクション。→ 4.0.0以上へ。
3. **obsidian-sync-mcp（0.5.7未満）** CVE-2026-77283／CVSS 4.0 8.8 HIGH／High／A01/A07。認証トークン未設定のHTTP /mcp が Host/Origin 未検証で、悪意あるサイト経由でObsidianの保管庫に触れる。→ 0.5.7以上＋MCP_AUTH_TOKEN設定。
4. **llama.cpp（複数）** CVE-2026-137057（CVSS 4.0 8.7、b7118〜b12604未満：GBNF文法の `{5,2}` で認証なしDoS＝サービス停止）／CVE-2026-133710（8.5、GGUFモデルのメタデータ細工による整数オーバーフロー→メモリ破壊。出所不明のモデルを読まない）。OWASP: 尤度HIGH×影響MED⇒High（DoS）／LLM Top10: LLM03 サプライチェーン相当（筆者の見立て）。→ 最新ビルドへ。
5. **Gradio（6.27.0〜6.32.0未満）** CVE-2026-134825／CVSS 4.0 8.3 HIGH／High／A07。ssr_mode有効時、偽の `Host: localhost` で運用者が保存したHugging Faceトークンを使われる。→ 6.32.0以上、ssr_modeを無効化。
6. **Hermes Agent（0.21.6〜0.23.1）** CVE-2026-130164／CVSS 3.1 7.8 HIGH／OWASP: 尤度LOW×影響HIGH⇒Medium。非ローカルのターミナルバックエンド上でBot Desktopを動かす場合に限り、バックエンドが書き込める環境ファイルを検証せず読み込み（CWE-426）、権限昇格の恐れ。→ 修正版へ更新。使用中の場合はバージョンと使用バックエンドを要確認。
7. **n8n（ワークフロー自動化）** CVE-2026-130166（CVSS 4.0 7.7、1.123.90/2.14.0未満：署名なし招待で既存メンバーが新規アカウントを乗っ取れる）／CVE-2026-130167（7.5、2.47.6等未満：独自ロールの管理者がオーナーのパスワードリセットを取得）。OWASP: A01/A07、Medium〜High。→ 該当版へ更新。
8. **ServiceNow Now Assist for CSM の Email Response AI Agent** CVE-2026-18883／CVSS 4.0 7.1 HIGH／間接プロンプトインジェクション（メール等の外部文面に紛れた命令でAIを操る）。ベンダー側で集中修正済み、悪用は未確認と発表。LLM Top10: LLM01 Prompt Injection。
9. **AutoGPT（0.7.1〜0.8.4）** CVE-2026-133448／CVSS 3.1 7.1：Claude Code CLIへ渡す文章が前処理され、ツール許可リストやフックを回避。LLM Top10: LLM06 Excessive Agency（過剰な権限）。別件で課金回避・サンドボックス放置（CVE-2026-132255/132260、各6.5）も。→ 0.11.0以上へ。
10. **codebase-memory-mcp（0.9.0未満ほか）** CVE-2026-114494/114495 ほか計5件（7.8〜5.5）：細工したリポジトリ・クエリでメモリ破壊、DoS、引数注入。信頼できないリポジトリを読ませない。→ 0.10.0以上。
11. **pmo-platform（Claude Code向け）** CVE-2026-77350（7.3）ほか3件：安全装置のフックが `jq` 不在時に「成功」を返し素通りする（fail-open）。→ 3.73以上。
12. **その他**: browser-use 1.0.0未満（CVE-2026-136452、6.1：URL解析差で許可ドメイン制限を回避）／Amazon ECS MCP Server 0.1.36未満（CVE-2026-135614、6.8：環境変数やシークレット参照が漏れうる）／one-hub（CVE-2026-133875、5.3 SSRF）／Flyto2 Core（CVE-2026-77315、GitHub 8.5：ページ送りURLでSSRF）。

※ 第三者のMCPサーバ/ツールを導入する際の信頼性指標（Star数・ライセンス・作成日・owner種別）は今回のデータに無く『不明』。導入前に信頼性チェック（コード目視・作者・ライセンス）を。

## 🧠 AI特有の攻撃・インシデント（報道・公式）
今週は検索で新規の大型インシデントを確認できず、直近の整理記事のみ。
- Adversa AI「AI agent security November 2026」（2026-11-05）：AgentCoreの一発プロンプトによる乗っ取り、組み込みブラウザ悪用、エージェントが監視を無効化する事例等の月次まとめ。https://adversa.ai/blog/top-ai-agent-security-resources-november-2026/
- Cloud Security Alliance「Poisoned Skills」（2026-06-24）：スキル市場・MCPの導入前に、公開者・版履歴・承認時刻の棚卸しを推奨。https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-skill-supply-chain-attacks-20260624-csa/
- CSA「Agentjacking」（2026-06-12）：Sentryのイベント投入を介し、MCP接続の開発用AIを乗っ取る手法。https://labs.cloudsecurityalliance.org/research/csa-research-note-agentjacking-mcp-sentry-injection-20260612/
- ruflo のRCE（CVE-2026-59726）の詳細解説：https://advisories.gitlab.com/npm/ruflo/CVE-2026-59726/

筆者の見立て: 今週のCVEは「MCPサーバの管理面に認証・Origin検証がない」型が繰り返し出ている。

## 🇯🇵 国内の公的機関の動き
今週は該当なし（IPA・JPCERT/CC で対象キーワードの新着なし）。

## 📚 OWASP GenAI の更新
今週は該当コミットなし（省略）。

## ✅ 今週のやること（筆者の提案）
該当製品を使っている場合のみ対応。
1. MCPサーバ（ruflo／Jupyter MCP／obsidian-sync-mcp等）を使っていれば版確認と更新。HTTP公開していないか確認。
2. Hermes Agent のバージョンと端末バックエンド構成を確認（CVE-2026-130164）。
3. llama.cpp・Gradio・n8n・AutoGPT を使う場合は該当版以上へ。
4. 出所不明のGGUFモデルや信頼できないリポジトリをAIに読ませない。
5. エージェントの許可リスト・フックが「失敗時に通す」設計になっていないか点検。

## ℹ この記事の見方
- 取得: データ取得スクリプトが公式API（NVD・GitHub Advisory・CISA KEV・IPA/JPCERT・OWASP）から収集。取得失敗の情報源は無し（21件成功）。
- 数値は取得時点の値。NVD未精査の案件は発行元採点。CVSS 3.1と4.0は直接比較不可。
- OWASP Risk Rating は技術面のみの**推定**（業務影響は環境依存のため未採点）。Top10の分類は筆者の見立て。
- ruflo以外のGHSA詳細（修正版番号）は個別確認していない。

## 出典
- https://nvd.nist.gov/ （各CVEページ）
- https://github.com/advisories/GHSA-c4hm-4h84-2cf3
- https://github.com/advisories/GHSA-9x8x-crjq-g64h
- https://github.com/advisories/GHSA-24pw-rf5p-mgp7
- https://github.com/advisories/GHSA-2mr3-rxrq-238c
- 上記「報道・公式」節のURL

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
