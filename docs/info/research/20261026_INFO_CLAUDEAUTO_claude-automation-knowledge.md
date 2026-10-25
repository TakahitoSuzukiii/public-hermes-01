作成日: 2026-10-26 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code による業務自動化ナレッジ（週次 2026-10-26）

## 今週のテーマ

今週は「インフラ運用の現場でどう使うか」に軸足を置きました。先週までのExcel/PowerPoint単体の話から一歩進め、①月次レポートの一気通貫生成、②障害調査・ログ解析・Runbook（運用手順書）作成、③CI/CD（継続的インテグレーション/デリバリー）上のセキュリティ、④Playwright（ブラウザ自動操作ツール）、⑤awesomeリスト、の順で紹介します。なお各記事の数値や効果は出典側の主張であり、自環境での検証が前提です。

## 1. ITインフラ運用のルーティン自動化（Excel / PowerPoint）

### 1-1. Claude Code × python-pptx × openpyxl で月次KPI資料をワンコマンド生成
- 出典: https://aurant-technologies.com/blog/claude-excel-powerpoint-28013/
- 概要: Excelの月次KPIを読み込み、役員向けPowerPointを自動生成する仕組みの解説です。python-pptx（PowerPoint操作ライブラリ）とopenpyxl（Excel操作ライブラリ）をClaude Codeに書かせ、スクリプト化する流れです。サーバ稼働率やインシデント件数の月次報告にそのまま応用できます。
- 注意点: 会社テンプレートのレイアウト崩れに注意。生成後の目視確認は必須です。

### 1-2. PowerPoint自動生成の3手法比較
- 出典: https://aurant-technologies.com/blog/claude-code-powerpoint-jidoka/
- 概要: 公式スキル・python-pptx・Claude for PowerPointの3手法を比較し、テンプレートを壊さない設計を解説。毎回同形式の報告書なら「スクリプト化して再利用」、単発なら対話型、という使い分けの判断材料になります。
- 注意点: 手法ごとに再現性と手間が異なるため、まず小さい資料で試すのが安全です。

### 1-3. Excel業務（集計・転記・レポート）の自動化と安全運用ルール
- 出典: https://claudecode-cases.com/cases/claude-code-excel-automation-guide-2026/
- 概要: VBA（Excelのマクロ言語）マクロからPythonへの移行手順、pandas/openpyxl実装例、失敗パターンを扱います。属人化したマクロの置き換えに有用です。
- 注意点: 元ファイルは必ずバックアップし、コピーに対して処理させること。

## 2. セキュリティ運用の自動化

### 2-1. Claude Code GitHub Actionのプロンプトインジェクション事例（Microsoft）
- 出典: https://www.microsoft.com/en-us/security/blog/2026/06/05/securing-ci-cd-in-agentic-world-claude-code-github-action-case/
- 概要: AIエージェントをCI/CDに組み込む際、特定条件でワークフローのシークレットに到達されうる経路があったという1次情報の調査記事です。責任ある開示、Anthropic側の緩和策、安全な構成の指針が整理されています。AIを自動化に組み込む側が必ず知っておくべき内容です。
- 注意点: 外部入力（Issue/PR本文）をそのままAIに渡さない、権限とシークレットを最小化する、が基本方針です。

### 2-2. Claude Securityの脆弱性トリアージ参照ハーネス（Anthropic公式）
- 出典: https://github.com/anthropics/defending-code-reference-harness
- 概要: リポジトリの脆弱性をスキャンし、多段階の検証で誤検知（False Positive）を減らし、トリアージ→修正検証→修正案生成まで管理する参照実装です。スキャナのノイズ整理に役立ちます。
- 注意点: 検出結果は人が最終判断する運用にしてください。

## 3. インフラ/SRE・CI/CD・Playwright

### 3-1. SRE・インフラ運用をClaude Codeで効率化（本番に触らせない設計）
- 出典: https://claudecode-cases.com/cases/claude-code-sre-infrastructure-operations-guide-2026/
- 概要: ログ調査、障害切り分け、IaC（Infrastructure as Code：設定のコード化）レビュー、Runbook作成を、本番に直接触らせない安全設計とプロンプト例つきで解説。読み取り専用権限から始める考え方が実務的です。
- 注意点: 権限を絞り、変更系コマンドは人が承認する前提にすること。

### 3-2. kubectl・terraform・ログ解析の自動化ガイド
- 出典: https://techotakulab.com/claude-code-for-infra-engineers-2026/
- 概要: Kubernetes障害調査、Terraformリファクタリング、Hooks（特定タイミングで自動実行される処理）設定、CLAUDE.md（Claudeへの指示書）作成を扱います。危険なコマンドをHooksで止める設定の参考になります。
- 注意点: planの確認なしにapplyさせない運用を徹底。

### 3-3. Playwright skill（ブラウザ操作を自動で書いて実行）
- 出典: https://github.com/lackeyjb/playwright-skill
- 概要: Claudeが必要に応じてPlaywrightのスクリプトを書いて実行するスキル/プラグイン。管理画面の定期確認やスクリーンショット取得など、API無しの画面作業の自動化に向きます。
- 注意点: ログイン情報は環境変数等で管理し、コードやログに残さないこと。個人開発のため導入前に内容確認を。

## 4. awesomeシリーズ

### hesreallyhim/awesome-claude-code
- 出典: https://github.com/hesreallyhim/awesome-claude-code/
- 概要: Claude Code関連のスキル、スラッシュコマンド、CLAUDE.md例、ステータスライン等の厳選リスト。目次に「Infrastructure & DevOps」「Security」「Observability & Monitoring」があり、運用自動化のネタ探しの入口になります。検索時点でスター数は約5.6万と大きなコミュニティです。
- 注意点: コミュニティ投稿の集合体なので、個別ツールの導入前にコード確認が必要です。

## まとめ
今週の要点は「便利さ」と「権限設計」はセットという点です。レポート生成のような低リスク領域から始め、本番に触れる領域は読み取り専用・人の承認を挟む形で段階導入するのが良さそうです。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
