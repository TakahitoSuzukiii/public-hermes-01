# Claude / Claude Code / cowork 業務自動化ナレッジ（週次収集）

作成日: 2026-08-17 / STATUS: INFO / TOPIC: CLAUDEAUTO

## 今週のテーマ

今週は Claude（Anthropic の AI モデル）と Claude Code（コーディング特化のCLI＝コマンドラインツール）による業務自動化動向のうち、前週までとは異なる切り口を中心に収集しました。「PowerPoint アドイン『Claude in PowerPoint』とテンプレート活用」「Claude Code 公式のセキュリティレビュー機能（`/security-review` と GitHub Actions 連携）」「GitHub Actions への Claude Code Action 導入と決済フローの Playwright MCP テスト自動化」「楽天の Claude Code 導入事例」「サブエージェント（Subagent）を大量収録した Awesome リスト」の5カテゴリで整理しています。いずれも一次情報源（公式ドキュメント・公式ブログ・実践者のnote/Zenn/Qiita記事）を優先しました。

---

## 1. ITインフラ/サーバ運用保守のルーティンワーク自動化（PPT・Excel特化）

### How to Create High-Quality PowerPoint Presentations with Claude Code
- 出典: https://note.com/ai__worker/n/nc63f9304f273
- 内容: 2026年2月にリリースされた「Claude in PowerPoint」（PowerPoint に直接組み込まれたアドイン機能）と、Claude Code から `template.pptx` を指定して既存の社内テンプレート（フォント・配色・レイアウト）を維持したままスライドを生成する手法を併記した実践記事。両者の使い分け方も解説されています。
- 便利さ: 「アドインでリアルタイム編集」と「Claude Code + MCP でテンプレート厳守の自動生成」という二つのアプローチの違いが具体的に示されており、社内資料フォーマットを崩したくない現場での選択肢の幅が広がります。
- 注意点: 「Claude in PowerPoint」はリサーチプレビュー扱い（Max/Team/Enterprise プラン向け）のため、一般提供の条件や日本語UIの対応状況は導入前に最新の公式情報を確認する必要があります。

### Claude Codeスキルで運用・保守の初動調査を自動化する
- 出典: https://zenn.dev/third_tech/articles/claude-code-inquiry-skill-maintenance
- 内容: 運用・保守現場で発生する「問い合わせチケットを読む→フォルダを作る→依頼内容を整理する→調査クエリを書く」という定型作業を、Claude Code の Skill 機能（モデルが自律的に呼び出す拡張機能）と Notion MCP（Notion をAIから操作する連携規格）を組み合わせて自動化する仕組みを紹介する記事。
- 便利さ: 問い合わせ対応という「PPT・Excel作成」以外の運用ルーティンワークにも自動化の勘所（スキル分割・MCP連携の設計）が応用できる好例で、初動対応の属人化を減らすヒントになります。
- 注意点: Notion への接続にはOAuth認証の設定が必要で、社内の問い合わせ内容には機密情報が含まれる可能性があるため、Skill がアクセスできる範囲を事前に絞り込む設計が不可欠です。

---

## 2. ゼロデイ攻撃対策・セキュリティ運用の自動化

### Automated Security Reviews in Claude Code（Anthropic公式ヘルプセンター）
- 出典: https://support.claude.com/en/articles/11932705-automated-security-reviews-in-claude-code
- 内容: Claude Code に組み込まれた `/security-review` コマンドと、GitHub Actions 連携によるプルリクエスト単位の自動セキュリティレビュー機能の公式解説。SQLインジェクション・XSS（クロスサイトスクリプティング）・認証不備などを自動検出し、修正案の提示までを一連の流れとして案内しています。
- 便利さ: コマンド一つでローカル開発中にもセキュリティレビューを回せる手軽さがあり、`claude-code-security-review`（Anthropic公式のGitHub Action）と組み合わせればCIパイプラインにも組み込めるため、日常のルーティンとして脆弱性チェックを定着させやすい構成です。
- 注意点: PRのタイトルやコメントに悪意ある指示文を埋め込み、AIレビューを誤動作させる「プロンプトインジェクション」攻撃が実際に報告されています（DEV Community等で事例紹介）。自動レビューの結果を鵜呑みにせず、人間による最終確認を必ず挟む運用が重要です。

---

## 3. インフラ/クラウドエンジニア・SRE・CI/CD・Playwrightによる自動化

### Claude Code GitHub Actionsを使いこなせ
- 出典: https://zenn.dev/acntechjp/articles/3f361da473eac8
- 内容: Claude Code Action（GitHub Actions 上でClaudeを動かす公式アクション）のセットアップ手順を解説した記事。リポジトリの権限設定（Read and write permissions、Pull Request作成の許可可否）や、複数リポジトリを横断して呼び出す設定例まで具体的に示されています。
- 便利さ: Issue や Pull Request 上でのAIレビュー・修正提案を、権限設計の勘所も含めて把握できるため、CI/CD（継続的インテグレーション／継続的デリバリー）パイプラインへの初導入時の設定ミスを防ぎやすい内容です。
- 注意点: Pull Request の自動作成を許可する設定は、意図しないコード変更が自動でマージ候補になるリスクもあるため、まずは提案作成のみを許可し、段階的に権限を広げるのが無難です。

### 毎回手でやっていた決済テスト、Playwright MCPに任せてみた
- 出典: https://qiita.com/chara-gida/items/ae4b3695f37fbaf78f99
- 内容: 複数存在する決済導線のE2E（エンドツーエンド）回帰テストを、Playwright（ブラウザ自動操作ツール）とMCP（Model Context Protocol）を使ってClaude Codeに作成させた実践記。`claude mcp add` コマンドでPlaywright MCPサーバーを登録するところから、テストシナリオ作成の流れまでが具体的に書かれています。
- 便利さ: 決済フローという「毎回手作業で確認していた高リスク領域」をテスト自動化した実例のため、同様に手動確認に頼っているEC・金融系の回帰テスト業務にそのまま応用しやすい構成です。
- 注意点: 決済関連のテストは実際の課金・個人情報に触れる可能性があるため、必ずテスト環境（サンドボックス）を用いて本番データを使わない設計にする必要があります。

---

## 4. ベストプラクティス、実際に構築・検証して効果があった手順書/実績

### Rakuten Claude Code case study（Anthropic公式）
- 出典: https://claude.com/customers/rakuten
- 内容: 楽天がClaude Codeを開発ライフサイクル全体（ユニットテスト作成、APIモッキング、コードレビュー、並行開発セッションの運用）に組み込み、既存プロセスにAIを後付けするのではなく開発ワークフロー自体をClaude Code前提で再設計した事例を紹介するAnthropic公式の顧客事例。
- 便利さ: 大企業の実運用に基づく一次情報のため、「AIを個別タスクの補助に使う」段階から「開発フロー全体を再設計する」段階へ進む際の考え方・組織的な導入プロセスの参考になります。
- 注意点: 楽天規模の開発組織を前提とした事例のため、小規模チームがそのまま同じ体制（並行セッション運用等）を再現するのは難易度が高く、自社規模に合わせた段階的な導入計画が必要です。

---

## 5. GitHubのawesomeシリーズ

### awesome-claude-code-subagents（VoltAgent）
- 出典: https://github.com/VoltAgent/awesome-claude-code-subagents
- 内容: Claude Code のSubagent（特定タスクに特化した副次的なAIエージェント）を10カテゴリ・154種類以上収録した大規模キュレーションリスト。プラグイン形式でのインストール（`/plugin marketplace add` コマンド）にも対応しており、開発・インフラ・セキュリティ・データ・ビジネス領域を横断しています。
- 便利さ: カテゴリ別にSubagentの定義（Markdownファイル）が整理されているため、自社の業務ドメインに近いSubagentをそのまま導入・カスタマイズする起点として使いやすく、「154個全部使う」のではなく必要な数個だけ選んで使う設計にも向いています。
- 注意点: Subagentの数が多いこと自体が良し悪しという議論もあり（hamedtaheri.com の考察記事等）、コンテキスト消費や管理コストの観点から、まずは業務に直結する数個から試験導入するのが推奨されます。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
