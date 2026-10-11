作成日: 2026-10-12 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code 業務自動化ナレッジ（週次 2026-10-12）

## 今週のテーマ
今週は「資料作成（PPT＝PowerPoint／Excel）の自動化」と「Claude Code 公式のセキュリティ自動化プラグイン」を中心に紹介します。先週までと重複しないよう、公式ドキュメントの新しめの機能（Claude Securityプラグイン、security-guidanceプラグイン）と、Office資料生成系の事例を選びました。
※出典の説明文を元に要約しています。実環境で使う前に各自で検証してください。

---

## 1. ITインフラ運用のルーティン：PPT・Excelレポート自動化

### 1-1. Claude-Excel-PPT-Skills（GitHub）
- 出典: https://github.com/r123singh/Claude-Excel-PPT-Skills
- Claude Skills API（Claudeに専門手順を持たせる仕組み）で、PowerPointやExcelをスクリプト（PowerShell／Bash）から生成するサンプル集です。月次の稼働報告書など「定型フォーマットを毎回作る」作業を、コマンド一発に寄せる足がかりになります。
- 注意: 個人リポジトリのため、導入前に内容・ライセンス・スター数を確認し、社内データを渡す前にコードを目視確認してください。

### 1-2. PowerPoint MCP Server
- 出典: https://powerpointmcpserver.dev/
- MCP（Model Context Protocol＝AIと外部ツールをつなぐ共通規格）経由でスライド、編集可能なグラフ、表、発表者ノートを作る仕組みです。サイトの例では、Excelで分析した結果から7枚の役員向け資料を作る流れが紹介されています。
- 注意: 第三者サービスです。信頼性チェック（作者・更新状況・通信先）を済ませるまで本番データには使わないでください。

### 1-3. Claude MCPでExcelレポートを生成するチュートリアル
- 出典: https://thedailyworkflow.com/mcp/tutorial/generate-reports-from-excel-with-claude-mcp
- ExcelのMCPサーバーをClaudeにつなぎ、既存Excelからレポートを自動作成する手順解説（2026-04公開）。サーバーの月次リソース集計表のような反復業務に応用しやすいです。
- 注意: 数式や集計結果は必ず人が突き合わせて検算してください。

### 1-4. Claude Design＋Skillsで Excel→PPT デッキ作成
- 出典: https://davidariasfinance.com/ai-implementations/powerpoint-automation/
- Excelのデータから、プロンプトとSkillsでスライド資料を組み立てる手順の紹介です。金融向けの例ですが、「データ→構成→スライド」の型はインフラ報告にも流用できます。
- 注意: 金融特化のため、自環境向けにテンプレートの調整が必要です。

---

## 2. セキュリティ運用の自動化

### 2-1. Claude Securityプラグイン（公式）
- 出典: https://code.claude.com/docs/en/claude-security
- `/claude-security` コマンドで、複数のAIエージェントがリポジトリ構造を把握→脅威モデル作成→脆弱性探索→独立検証までを行い、結果をSARIF（静的解析結果の標準形式）形式でも出力します。修正パッチも作成されますが、自動適用はされず、人がレビューして適用する設計です。
- 注意: スキャンは実行ごとに結果が変わりえます（非決定的）。既存の静的解析・依存関係スキャンの代替ではなく併用が前提です。使用量（コスト）も消費します。

### 2-2. security-guidanceプラグイン（公式）
- 出典: https://code.claude.com/docs/en/security-guidance
- Claudeがコードを書く最中に、①編集時のパターン照合（モデル呼び出しなし）、②ターン終了時のバックグラウンドレビュー、③commit／push時の深掘りレビューの3段階で脆弱性を自己チェックします。フック（hooks＝処理の差し込み機構）で実装されています。
- 注意: 書き込みをブロックする強制力はありません。強制したい場合はフックやCIチェックと組み合わせます。

---

## 3. Playwrightによるブラウザ自動化

### 3-1. Playwright公式：Claude Code向けMCP設定
- 出典: https://playwright.dev/mcp/clients/claude-code
- Claude CodeのCLIでPlaywright MCPサーバーを追加する公式手順です。追加すると次回セッションから、AIがブラウザを操作してUI確認やテスト生成ができます。
- 注意: ログイン情報を扱う場合は専用アカウント・最小権限にし、認証情報をプロンプトに書かないこと。

### 3-2. Builder.io：Playwright MCP＋Claude Code実践
- 出典: https://www.builder.io/blog/playwright-mcp-server-claude-code
- 1コマンドでの導入、AI自身による動作確認（セルフQA）、探索的テスト、保存済みログイン状態の利用、トラブル対処をまとめた解説です。
- 注意: 英語記事です。保存した認証状態ファイルは機密として扱い、リポジトリにコミットしないでください。

---

## 今週の所感
資料作成系は「テンプレート＋Skills／MCP＋人の検算」の三点セットが現実的です。セキュリティ系は公式プラグインが層（編集時→PR→CI）で整理されてきたため、既存ツールとの役割分担を決めるのが次の一手です。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
