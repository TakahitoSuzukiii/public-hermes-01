作成日: 2026-11-02 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code 業務自動化ナレッジ(週次) 2026-11-02号

## 今週のテーマ
今週は「**Office資料(Excel/PowerPoint)の定型レポート自動化**」「**PR(プルリクエスト)単位のセキュリティレビュー自動化**」「**SRE(Site Reliability Engineering=サイト信頼性工学)のインシデント対応エージェント**」を中心に紹介します。先週までと重複しない、新しい出典を選んでいます。共通の教訓は「AIに下書き・調査を任せ、書き込みや本番操作は人が承認する」設計です。

## 1. ITインフラ運用のルーティン自動化(Excel/PPTレポート)

### 1-1. claude-office-skills(Claude in Excel / PowerPoint のスキルをClaude Code用に再構成)
- 出典: https://github.com/fivetaku/claude-office-skills
- 便利さ: Anthropicが各Officeアドインに組み込んでいる専門スキルを、通常の `SKILL.md` ファイル(Claudeに手順を教える説明書)として再構成したものです。Claude Codeからローカルの .xlsx / .pptx を直接扱えるため、アドインを開かずに月次レポートの整形や集計を自動化できます。
- 注意点: 非公式の個人リポジトリです。導入前にStar数・作者・コード内容(外部通信の有無)を必ず確認してください。

### 1-2. Claude Skills API で PPTX / XLSX を生成するサンプル
- 出典: https://github.com/r123singh/Claude-Excel-PPT-Skills
- 便利さ: Claude Skills API(事前用意された文書作成機能)を PowerShell / Bash から呼び、PowerPoint やExcelをプログラムで生成する実例です。サーバ稼働レポートを夜間バッチで自動作成する、といった応用が考えられます。
- 注意点: APIキーは環境変数・シークレット管理で扱い、スクリプトに直書きしないこと。

### 1-3. Claude Code Playbooks「Automated Report Generator」
- 出典: https://www.claudecodehq.com/playbooks/report-generator
- 便利さ: 「データ取得→表→グラフ→コメント→整形」という毎月繰り返す作業を、Claude Codeに任せる型(プレイブック)として整理しています。自社のレポート工程を分解する際のチェックリストとして使えます。
- 注意点: 第三者サイトの解説であり、内容は自環境で検証してから採用してください。

### 1-4. 公式ドキュメント: Claude for Excel
- 出典: https://claude.com/docs/office-agents/excel
- 便利さ: Excelアドインとして表計算上でClaudeを使う公式手順です。Pro/Max/Team/Enterpriseプランが対象で、手作業の数式整備や集計の補助に向きます。
- 注意点: 機密を含むシートをどこまで送るか、社内ルールを先に確認してください。

## 2. セキュリティ運用の自動化

### 2-1. Anthropic公式ブログ: Claude Codeによるセキュリティレビュー自動化
- 出典: https://claude.com/blog/automate-security-reviews-with-claude-code
- 便利さ: `/security-review` コマンドでコミット前にSQLインジェクション(不正なSQL実行)やXSS(クロスサイトスクリプティング)等を点検でき、GitHub Actionと組み合わせれば全PRに自動で指摘コメントを付けられます。
- 注意点: AIの指摘は誤検知もあり得ます。最終判断は人が行います。

### 2-2. claude-code-security-review(公式GitHub Action)
- 出典: https://github.com/anthropics/claude-code-security-review/
- 便利さ: PRの差分だけを解析し、重大度と修正案を行単位でコメントします。誤検知フィルタ付き。
- 注意点: READMEにある通り、**プロンプトインジェクション(悪意ある入力でAIを誤誘導する攻撃)への耐性は強化されていません**。信頼できるPRにのみ使い、外部コントリビューターのワークフロー実行は承認制にしましょう。

### 2-3. Deriv社の導入事例
- 出典: https://derivai.substack.com/p/automated-security-code-reviews-claude-code-github-actions
- 便利さ: 4つのGitHub組織に展開し、重大度・CWE(共通脆弱性分類)・修正コード付きでPRにレビューを出す運用例です。Claudeが修正ブランチを作っても、pushは開発者の承認待ちにする点が実務的です。
- 注意点: 事例は企業自身の報告です。効果の数値は自社で測定してください。

### 2-4. 週次の脆弱性・依存関係修復ワークフロー例
- 出典: https://github.com/alexander-turner/TurnTrout.com/blob/main/.github/workflows/security-vulnerability-scan.yaml
- 便利さ: 毎週月曜にDependabot等のアラートを集約し、Claudeがまとめて修正PRを1本作る構成です。ゼロデイ(未修正の脆弱性)公表後の追随を定期化する発想の参考になります。
- 注意点: 個人リポジトリの設定例です。権限(permissions)は最小に絞って流用してください。

## 3. SRE・インフラ自動化

### 3-1. Claude Cookbook「The site reliability agent」
- 出典: https://platform.claude.com/cookbook/claude-agent-sdk-03-the-site-reliability-agent
- 便利さ: Claude Agent SDKとMCP(Model Context Protocol=AIと外部ツールをつなぐ共通規格)で、障害調査→原因特定→修復→ポストモーテム(事後報告書)作成までを行うエージェントを作る公式チュートリアルです。Runbook(手順書)をスキル化する考え方も学べます。
- 注意点: サンプルは設定編集や再起動もできるため、本番では権限と承認フローを必ず設けてください。

### 3-2. Arcade「Claude Code for AI SRE on-call」
- 出典: https://www.arcade.dev/blog/claude-code-ai-sre-oncall-workflows/
- 便利さ: 障害切り分け・Runbook実行・ポストモーテム下書き・SLO調査・当番引き継ぎの5ワークフローを整理。「Claudeは計画を出し、実行は当番者が自分の権限で行う」という線引きが参考になります。
- 注意点: 認証・権限範囲・監査ログの整備が最大のボトルネックと指摘されています。ベンダー記事のため製品訴求を含みます。

### 3-3. 承認キュー付きSRE障害対応エージェントのレシピ
- 出典: https://claude-agents-cookbook.cloudjugaad.com/docs/recipes/sre-incident-agent/
- 便利さ: 読み取りツールは自動、再起動などの書き込みは人の承認(HITL=Human-in-the-Loop)を必須にする設計例です。
- 注意点: コミュニティ製資料。公式ではありません。

## 4. awesomeシリーズ
### jqueryscript/awesome-claude-code
- 出典: https://github.com/jqueryscript/awesome-claude-code
- 便利さ: 公式リソース、エージェント、スキル、プラグイン、監視ツールなどをカテゴリ別に整理した一覧です。セキュリティ用の `defending-code-reference-harness`(脅威モデリング〜パッチ適用のスキル群)も載っています。
- 注意点: Star数などは記録時点の固定値。導入前は各リポジトリの信頼性(作者・更新状況・ライセンス)を確認してください。

## まとめ
Excel/PPTレポートはスキル化、セキュリティはPR単位の自動レビュー、SREは「調査はAI、書き込みは人が承認」が今週の共通解です。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
