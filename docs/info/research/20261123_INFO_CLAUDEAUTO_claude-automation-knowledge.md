作成日: 2026-11-23 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code 業務自動化ナレッジ（週次 2026-11-23）

## 今週のテーマ

今週は「資料作成の自動化を“型（スキル）”で再現可能にする」「セキュリティ検査を“人間の承認付き”で回す」「ブラウザ自動化はMCPかCLIか」の3本柱で選びました。先週までと重複しない新規の出典を中心に紹介します。

用語メモ:
- **スキル（Skill）**: Claudeに作業手順をまとめて教える部品。`SKILL.md`という手順書ファイルが中核。
- **MCP（Model Context Protocol）**: AIが外部ツールを呼び出すための共通規格。
- **SRE（Site Reliability Engineering）**: サービスの信頼性を運用で守る考え方・職種。
- **SLO（Service Level Objective）**: サービス品質の目標値。
- **E2E（End-to-End）テスト**: 画面操作から結果までを通しで確認するテスト。

---

## 1. ITインフラ運用：PPT・Excel資料作成の自動化

### 1-1. claude-office-skills の仕組み解説（note記事）
- 出典: https://note.com/snake_dragon/n/n1b44e307202a
- Claude Codeが Office ファイルを作る裏側を解説した記事です。形式ごと（pptx/docx/xlsx/pdf）に`SKILL.md`があり、Claudeはそれを読んで手順通りにPython等のツールを呼びます。Excelでは生成後に全セルを走査して`#REF!`等の数式エラーがゼロか確認する、入力セルは薄青・数式セルは白といった色分けルールを守る、という品質ゲートが組み込まれています。PPTではサムネイル画像で人が目視確認する手順が入っています。
- 月次運用レポート（DBから数値取得→Excel→スライド→PDF）の定型化に応用しやすい設計です。
- 注意点: 記事は解説であり、実環境ではテンプレートと数式の検証を自社データで必ず行ってください。

### 1-2. slide-forge（Google スライド生成の自動化）
- 出典: https://github.com/wfukatsu/slide-forge
- 要件聞き取り→構成案承認→検証→生成→見た目チェック→PPTX書き出し、までを1本の流れ（`/forge`）にしたプラグインです。見積・BOM（部品表）のExcel/スプレッドシート出力もあります。事前に無料でオフライン検証できる点が、手戻り削減に効きます。
- 注意点: 個人開発リポジトリです。導入前にStar数・作者・ライセンス・スクリプト内容の確認が必要です（外部スキル導入チェック規約）。Googleアカウント連携が必要な点にも留意。

### 1-3. Claude for Excel / PowerPoint のアップデート（公式）
- 出典: https://claude.com/resources/articles/claude-excel-powerpoint-updates
- ExcelとPowerPointのアドインが会話の文脈を共有し、Excelの集計結果をそのままスライドに反映できるようになりました。チームの手順を「スキル」として保存すれば、ワンクリックで再現できます。Amazon Bedrock等の主要クラウド経由でも使えます。
- 関連: https://claude.com/docs/office-agents/excel （Excelアドインの使い方、セル単位の根拠付き回答）
- 注意点: 対象プラン（Pro/Max/Team/Enterprise）と、扱うデータの社内規程を事前確認してください。

---

## 2. セキュリティ運用の自動化

### 2-1. Claude Security プラグイン（脆弱性スキャン）
- 出典: https://code.claude.com/docs/en/claude-security
- 複数のエージェントがコードの構造把握→脅威モデル作成→脆弱性探索→別エージェントによる検証、という流れでレポートを作ります。修正パッチは`patches/`に出力されるだけで、**自動適用はされません**（人が確認して適用）。スキャン結果は毎回少し変わる性質があるため、定期実行が推奨されています。
- 注意点: 既存の静的解析・依存関係スキャナの代替ではなく併用が前提です。実行は利用枠を消費します。

### 2-2. AIワークフローをCI/CDで使う際の落とし穴（Microsoft）
- 出典: https://www.microsoft.com/en-us/security/blog/2026/06/05/securing-ci-cd-in-agentic-world-claude-code-github-action-case/
- 信頼できない入力（Issue本文など）を処理するAIに、秘密情報へのアクセスと外部送信手段を同時に持たせるのは危険、という「Rule of Two（3つのうち同時に2つまで）」の考え方を紹介しています。トークンは用途ごとに最小権限・別キーにする、という実践的な指針です。該当の不具合はClaude Code 2.1.128で修正済みと記載されています。
- 注意点: 自動化を作る側が読むべき内容です。Actionは最新版に保つこと。

---

## 3. インフラ/SRE/CI/CD・Playwright

### 3-1. claude4ops（DevOps用コマンド集）
- 出典: https://github.com/ops4life/claude4ops
- Kubernetesのデプロイ検証、Terraformの`plan`レビュー（リスク・コスト）、CI/CDパイプライン生成、SLO定義、ポストモーテム（障害の振り返り）などをコマンド化。本番誤操作を防ぐ`block-prod`フックなども含みます。
- 注意点: こちらも個人/小規模OSSの可能性があるため、導入前に信頼性チェックを。まずは読み取り系コマンドから試すのが安全です。

### 3-2. Playwright MCP と Playwright CLI の使い分け
- 出典: https://github.com/microsoft/playwright-mcp （公式）／ https://playwright.dev/docs/getting-started-mcp
- 公式READMEは、コーディングエージェントにはCLI＋スキル方式のほうがトークン効率が良く、MCPは探索的な自動化や自己修復テストなど「状態を保ち続けたい」用途に向く、と整理しています。
- 注意点: `browser_run_code_unsafe`は任意コード実行相当のため、信頼できるクライアントのみで有効化。

### 3-3. Autodesk の E2Eブラウザテスト・スキル群
- 出典: https://github.com/Autodesk/claude-browser-test-skills
- 「自然言語でテスト作成→安定するまで反復→Playwrightの`.spec.ts`へコンパイル」というパイプライン。コンパイル後はLLM無しでCIを回せるので、コストと再現性の両立が狙えます。

---

## 4. awesome シリーズ

### 4-1. ComposioHQ/awesome-claude-skills
- 出典: https://github.com/ComposioHQ/awesome-claude-skills
- 1000件超のスキル/プラグインの一覧。Playwright自動化や Webアプリテスト等が含まれます。
- 注意点: 一覧に載っていることは安全性の保証ではありません。個別に中身を確認してください。

---

## まとめ（今週の学び）
- 資料自動化は「手順書(SKILL.md)＋品質ゲート（数式エラー0、目視サムネイル）」が鍵。
- セキュリティ自動化は「AIが提案、人が承認」を維持。AIに秘密情報と外部送信を同時に持たせない。
- ブラウザ自動化は、探索はMCP、定常運用はCLI/コンパイル済みテストでコスト最適化。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
