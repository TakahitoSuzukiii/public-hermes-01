作成日: 2026-10-19 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code による業務自動化ナレッジ（週次 2026-10-19）

## 今週のテーマ
今週は「**手法の比較と安全な運用ガード**」に注目しました。Excel／PowerPoint自動化は「3つの手法の使い分け」、セキュリティは「脆弱性の発見→検証→修正を自動で回す参照実装」、SREは「実行は人間・計画はAI」という役割分担が共通のキーワードです。先週までと重複しない記事を選んでいます。

## 1. ITインフラ運用のルーティン：PPT・Excelレポート自動化

### 1-1. Claude CodeでPowerPoint自動生成の実務ガイド（3手法の比較）
- 出典: https://aurant-technologies.com/blog/claude-code-powerpoint-jidoka/
- 公式スキル、python-pptx（PythonでPPTXを操作するライブラリ）、Claude for PowerPointの3手法を比較し、月次レポート等の自動化手順と「会社テンプレートを壊さない設計」を解説しています。定型の月次報告資料を作る運用担当者に向きます。
- 注意: 生成後の目視確認は必須。社内テンプレートに機密がある場合は外部送信範囲を確認してください。

### 1-2. Claude CodeでExcelを自動化する実務ガイド
- 出典: https://aurant-technologies.com/blog/claude-code-excel-jidoka/
- openpyxl（Excelファイル操作ライブラリ）、xlwings（Excel本体を操作）、Claude for Excelの3手法を比較。月次レポート、予実管理表、KPIダッシュボードの自動化手順がまとまっています。サーバの稼働率・容量集計の定期レポートに応用しやすい内容です。
- 注意: 手法により「Excel本体が必要か」が異なるため、実行環境（サーバ上かPC上か）で選びましょう。

### 1-3. 【2026年最新】Excel業務をClaude Codeで自動化する実践ガイド
- 出典: https://claudecode-cases.com/cases/claude-code-excel-automation-guide-2026/
- VBAマクロからPythonへの移行手順、pandas／openpyxl実装例、失敗パターンと安全運用ルールを扱います。既存の古いマクロ資産の置き換えを検討中の方に有用です。
- 注意: 元データは必ずバックアップし、AIが書き換えるのはコピーに限定するのが安全です。

### 1-4. Claude for Excel・PowerPoint・Word（公式情報の整理）
- 出典: https://claudedojo.com/blog/claude-for-microsoft-365-guide
- Office内で使えるClaudeアドインの対応プラン、導入手順、未対応機能、データの扱い、プロンプトインジェクション（外部文書に仕込まれた悪意ある指示でAIを誘導する攻撃）への注意点を整理した記事です。
- 注意: 第三者の解説記事のため、最終判断は公式ドキュメントで再確認してください。

## 2. セキュリティ運用の自動化

### 2-1. anthropics/defending-code-reference-harness（公式参照実装）
- 出典: https://github.com/anthropics/defending-code-reference-harness/
- 脆弱性の探索→検証→重複排除→報告→パッチ作成までをエージェントで回すパイプラインの「参照実装」です。コンテナ（gVisor）内に隔離し、通信をClaude APIのみに制限して実行する設計で、別エージェントが再現確認する二重チェックが特徴です。
- 注意: READMEでも「製品ではなく参考例」と明言。自律トリアージ／パッチは未解決課題で、重大度の判断は環境ごとに人間が行う必要があります。

### 2-2. Claude Securityプラグイン／Claude Securityスキャン手順
- 出典: https://code.claude.com/docs/en/claude-security および https://academy.claude.com/tutorials/getting-started-with-claude-security
- 複数エージェントがコードの構造把握→脅威モデル作成→脆弱性探索→独立レビューを行い、パッチは自動適用されません（`git apply`で人が適用）。運用面では週次の定期スキャン、検出結果のCSV出力、Webhook連携（Slack／Jira通知）が推奨されています。
- 注意: トークン消費が大きくなりうる点と、一部機能はEnterprise向けである点に留意。

### 2-3. wrxck/auto-audit（コミュニティ製）
- 出典: https://github.com/wrxck/auto-audit
- 検出→誤検知判定→PoC（概念実証コード）→修正PR→独立レビュー→マージを、1回の実行で1段階ずつ進めるループ型の監査ツールです。
- 注意: 個人リポジトリで実績・信頼性は未検証。導入前にStar数や作者、コードの確認が必須です。自動マージ設定は特に慎重に（手動マージ設定を推奨）。

## 3. インフラ／SRE／CI/CD／Playwright

### 3-1. AI SRE with Claude Code: 5つのオンコール運用ワークフロー
- 出典: https://www.arcade.dev/blog/claude-code-ai-sre-oncall-workflows/
- 障害一次切り分け、ランブック（手順書）実行、ポストモーテム（振り返り）作成、SLO調査、当番引き継ぎの5つを整理。ポイントは「Claudeが計画を出し、エンジニアが自分の権限で実行・書き込みを承認する」役割分担です。古くなったランブックをステージングで一括再生して劣化を検出する案も実用的です。
- 注意: 著者の所属企業の製品宣伝を含みます。認可・監査ログの整備が運用のボトルネックという指摘は参考になります。

### 3-2. Claude Code × GitHub Actions CI/CD自動化
- 出典: https://ses-base.com/articles/claude-code-github-actions-automation-guide/ ／ https://codingls.com/ai/7573/
- `claude-code-action`（GitHub Actions用の公式アクション）でPRレビュー自動化、`@claude`メンション対応、Issueからの実装、スケジュール実行、ヘッドレス実行（`-p`オプション）まで網羅しています。
- 注意: シークレットはGitHub Secretsに保管し、ワークフロー権限は最小にしてください。

### 3-3. Playwright AIエージェントをGitHub Actionsで実行
- 出典: https://playwright.aims-ai.com/blog/playwright-ai-agents-github-actions
- ClaudeとPlaywright MCPをCIで動かし、失敗テストの自動修復や夜間のテスト草案作成、PR起票までを行う例（YAMLとガードレール付き）です。
- 注意: 自動修復が「テストを通すためだけに期待値を書き換える」危険があるため、人のレビューを必ず挟みましょう。

## 4. ベストプラクティス（今週の共通項）
- AIは「計画・下書き」、人間は「実行承認・最終判断」。
- 自動適用は避け、差分（パッチ／PR）として提示させる。
- 実行環境の隔離と権限最小化（コンテナ、スコープ付き認証情報）。

## 5. awesomeシリーズ
今週は新規の掘り出し物なし（先週紹介の ComposioHQ/awesome-claude-skills を継続参照）。

## 今週の所感
Excel／PPT自動化は手法選びが成否を分けます。セキュリティ自動化は検出の次の「検証と修正」まで自動化が進んだ一方、最終判断を人に残す設計が標準になりつつあります。自環境へ導入する際は、まず読み取り専用の用途から小さく試すのが安全です。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
