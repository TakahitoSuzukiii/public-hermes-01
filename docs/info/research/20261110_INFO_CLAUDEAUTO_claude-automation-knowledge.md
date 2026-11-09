作成日: 2026-11-10 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code 業務自動化ナレッジ（週次 2026-11-10）

## 今週のテーマ
今週は「**資料作成（Excel／PowerPoint／Word）を“パイプライン”として設計する**」視点を中心に集めました。前週までは個別ツールの紹介が多かったため、今回は①公式 Skills の仕組み、②データ取得→加工→出力の3層設計、③実務者の自作ツール事例、を取り上げます。あわせてセキュリティ運用、Playwright、awesome 系リポジトリの新顔も紹介します。

用語メモ: **Skills**＝Claude に特定作業の手順を教える「SKILL.md」入りフォルダ。**MCP**（Model Context Protocol）＝AI と外部ツールをつなぐ共通規格。**CLAUDE.md**＝プロジェクト用ルールを書く指示ファイル。

---

## 1. ITインフラ運用のルーティン自動化（Excel／PPT 資料作成）

### 1-1. 公式 document-skills で PDF・Excel・Word・PowerPoint を扱う
- 出典: https://qiita.com/TakanobuSano/items/2c9d2686bdbc5e085191
- Anthropic 公式 Skills の文書系セット（pdf / xlsx / docx / pptx の4種）を、`/plugin marketplace add anthropics/skills` などで導入する手順の解説です。「何のツールで読むか」「Excel 数式やテンプレートをどう扱うか」といった作業手順を Claude に教える仕組みで、「Markdown を1スライド1メッセージの資料にする」といった依頼が可能になります。
- 注意点: 記事によると文書系 Skill は「source-available（中身は見られるが自由なOSSではない）」扱いとのこと。契約書・請求書・顧客提出物などは必ず人が最終確認してください。

### 1-2. パワポ・Excel・Word を1本のパイプラインにまとめる設計
- 出典: https://funnel-ai.jp/media/claude-code-business-doc-workflow/
- 「データ取得／加工／出力」の3層に分けると、データ源や出力形式が変わっても他層を使い回せる、という設計論です。出力形式ごとの on/off を設定ファイル（config.yaml）で切り替え、1形式が失敗しても他は続行する、定期実行は cron や GitHub Actions で、生成物はクラウドストレージで版管理するハイブリッド方式、など運用面まで書かれています。
- 注意点: .pptx/.xlsx などのバイナリは Git で差分が見えません。生成条件（設定・日時）を記録に残す工夫が必要です。

### 1-3. 非開発者が1か月で39個の業務ツールを作った事例（Zenn）
- 出典: https://zenn.dev/taku_z3nn/articles/a136f069d2cbf1
- IT 案件の PM/PL が、提案書・調査レポート・手順書・体制図・WBS・バージョンアップ調査表などの自動生成ツールを Claude Code で量産した体験談です。「仕事の3〜4割は資料作成」という実感のもと、体制図を台帳更新＋スクリプト実行で約3分で作る例が具体的です。
- 注意点: 体験談なので効果値は各環境で変わります。CLAUDE.md にルールを書いて品質を揃える点は真似しやすいです。

### 1-4. Claude Cowork：Excel の営業管理表から PowerPoint 報告書を生成
- 出典: https://serverless.co.jp/blog/5hdzvnl3a-fb/
- Cowork が Excel 用・PPTX 用 Skill を自動選択し、手順と進捗を表示しながら四半期レポートを生成する様子を検証した記事です。会社指定テンプレート用の Skill を自作しておけば、指定スタイルで出力できます。
- 注意点: テンプレート Skill の事前整備が前提です。数値の転記ミスは必ず目視確認を。

### 1-5. PowerPoint MCP Server で Excel の月次運用報告から資料を作成
- 出典: https://zenn.dev/acntechjp/articles/69c7340679b4b1
- python-pptx ベースの MCP サーバー（約32ツール）を Claude Code に登録し、IT システム月次運用報告の Excel から顧客向けスライドを自動生成する検証です。
- 注意点: 著者自身が「元 Excel と矛盾する内容が出た」と報告しています。入力データの整形と CLAUDE.md への明確なルール化で精度を上げる、という教訓が重要です。

## 2. セキュリティ運用の自動化

### 2-1. Claude Code の自動セキュリティレビュー（公式ヘルプ）
- 出典: https://support.claude.com/en/articles/11932705-automated-security-reviews-in-claude-code
- `/security-review` コマンドと GitHub Actions を使い、変更差分の脆弱性（SQL インジェクション等）を PR 時点で検出する公式ガイドです。運用保守のスクリプトやIaC変更の「出荷前チェック」に組み込めます。
- 注意点: AI のレビューは人のレビューの代替ではなく補助です。

### 2-2. 【要注意】AI 付き CI/CD 自体のリスク（Microsoft Security Blog）
- 出典: https://www.microsoft.com/en-us/security/blog/2026/06/05/securing-ci-cd-in-agentic-world-claude-code-github-action-case/
- Claude Code GitHub Action にプロンプトインジェクション経由でワークフローの秘密情報へ到達しうる経路が見つかり、開示・緩和された経緯の解説です。自動化を入れる側の防御（権限最小化、外部入力を信用しない）の教材になります。
- 注意点: 個別の修正状況は公式情報で確認し、Action を最新版に保つこと。

## 3. Playwright・ブラウザ自動化

### 3-1. MCP × Claude Code × Bedrock で Playwright 自動化を検証
- 出典: https://zenn.dev/hirata_infosys/articles/598068e56ae342
- Playwright 単体では難しい箇所と、LLM で補うと効果的な箇所の切り分けを検証した記事です。Amazon Bedrock 経由で使いたい企業環境の参考になります。

### 3-2. Claude Code × Playwright MCP の使い方（2026年版）
- 出典: https://omochix.com/claude-code-playwright-mcp-guide-2026/
- 導入、フォーム操作、E2E テスト、認証状態の扱い、安全な使い方までを整理しています。社内ツール巡回やスクリーンショット取得の入口に向きます。
- 注意点: 認証済みセッションを AI に渡す際は、操作範囲を絞ってください。

## 4. 非エンジニア向け導入ステップ

### 4-1. Claude Code × Microsoft 365 連携（中小企業向け）
- 出典: https://www.piste-ai.com/blog/claude-code-microsoft365-integration
- 「週次で繰り返す作業を3つ棚卸し→1業務だけ自動化→検証→横展開」という4ステップ。フォルダ単位の権限分離や、既存 VBA との二重運用回避など、導入時の落とし穴が整理されています。

## 5. GitHub の awesome シリーズ（新顔）
- https://github.com/VoltAgent/awesome-claude-code-subagents — 100以上の専門サブエージェント集。インフラ/DevOps 向けプラグイン（`voltagent-infra`）もあります。
- https://github.com/houshuang/awesome-claude-code — 7500セッション超の実運用から選んだ29個の Skills／hooks／agents。Claude Code が標準対応した項目は「superseded（置き換え済み）」と明記する誠実な運営が特徴で、`prevent-main-commit` のような hooks（特定イベントで自動実行される安全装置）は運用保守にも流用しやすいです。
- https://github.com/rohitg00/awesome-claude-code-toolkit — エージェント・コマンド・hooks・MCP 設定を網羅した大型ツールキット。
- 注意点（共通）: 導入前に Star 数・作者・ライセンス・スクリプトの中身を確認すること（野良スキル対策）。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
