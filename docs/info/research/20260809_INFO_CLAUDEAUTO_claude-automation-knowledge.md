# Claude / Claude Code / cowork 業務自動化ナレッジ（週次収集）

作成日: 2026-08-09 / STATUS: INFO / TOPIC: CLAUDEAUTO

## 今週のテーマ

今週は Claude（Anthropic の AI モデル）と Claude Code（コーディング特化のCLI＝コマンドラインツール）を使った業務自動化の最新動向を横断的に収集しました。特に「Excel／PowerPoint 資料作成の自動化」「Anthropic 自身によるゼロデイ脆弱性（未修正の未知の脆弱性）発見の取り組み」「Playwright（ブラウザ自動操作ツール）を使ったテスト自動化」「インフラ運用のベストプラクティス」「OSS（オープンソースソフトウェア）の Awesome リスト」の5カテゴリで整理しています。いずれも一次情報源（公式ブログ・GitHub・専門メディア）を中心に厳選しました。

---

## 1. ITインフラ/サーバ運用保守のルーティンワーク自動化（PPT・Excel特化）

### Claude Codeによる事務自動化の実例10選
- 出典: https://digital-front.jp/blog/1613/
- 内容: Excel・スプレッドシート連携から、集計結果を PowerPoint やドキュメント形式のレポートに自動整形するまでの一連のワークフロー事例を紹介。「数字の貼り付け＋コメント作成」という定型作業をほぼ自動化し、人間は最終チェックと微修正のみ行う運用モデルを提示している。
- 便利さ: Claude Code への指示は「仕様書を書くつもりで具体的に」書くのがコツと明記されており、初心者でも再現しやすい実践的なノウハウが多い。段階的に自動化範囲を広げる設計思想も参考になる。
- 注意点: 実例集は特定の業務フロー前提のため、自社の帳票フォーマットに合わせたカスタマイズ検証は別途必要。

### Claude Codeでパワポを自動生成する方法（python-pptx活用）
- 出典: https://funnel-ai.jp/media/claude-code-pptx-automation/
- 内容: python-pptx（Python で PowerPoint ファイルを操作するライブラリ）と Claude Code を組み合わせ、テンプレートの .pptx ファイルとデータ用 JSON を分離する設計を紹介。デザイン変更は PowerPoint 側で、データ変更は JSON 編集のみで完結する構成。
- 便利さ: コード変更をほぼ発生させずに「デザイン」と「データ」を分離できる点が、保守性の観点で優れている。テンプレート差し替えだけで別案件にも転用しやすい。
- 注意点: 複雑なアニメーションやグラフの自動生成は別途検証が必要な場合がある。

### Claude Codeで営業レポートを自動生成する方法（HubSpot連携）
- 出典: https://start-link.jp/hubspot-ai/ai/claude-code-practice/claude-code-sales-report-automation
- 内容: HubSpot（CRM＝顧客管理システム）のデータをエクスポートし、Claude Code のカスタムコマンド（`/monthly-report` 等）で毎月同じ品質のレポートを自動生成する手順を解説。Before/After比較で効果を定量的に示している。
- 便利さ: 「毎月第1営業日に手動でCSVエクスポート→Excel集計」という定型作業をワンコマンド化した実例として分かりやすい。
- 注意点: CRM連携部分は契約プランやAPI利用制限に依存するため、自社環境での事前確認が必須。

---

## 2. ゼロデイ攻撃対策・セキュリティ運用の自動化

### LLM-discovered 0-days（Anthropic Frontier Red Team）
- 出典: https://red.anthropic.com/2026/zero-days/
- 内容: Anthropic の Frontier Red Team が、Claude を使ってOSS（オープンソースソフトウェア）のゼロデイ脆弱性（未知の脆弱性）を大規模に発見・修正支援する取り組み「LLM-discovered 0-days」を公開。AI モデルによる脆弱性発見が実用段階に入ったことを示す一次情報。
- 便利さ: 防御側（ディフェンダー）がAIを使って攻撃者より先に脆弱性を見つけ、パッチ適用のリードタイムを稼ぐという運用思想が明確に示されている。セキュリティ運用担当者は自動スキャン導入の参考にできる。
- 注意点: 大規模な自動脆弱性発見は攻撃側にも悪用されうる諸刃の剣。社内利用は倫理・法務面のガイドライン整備とセットで検討すべき。

### Claude Mythos、主要OS・ブラウザ横断でゼロデイ脆弱性を大量発見
- 出典: https://thehackernews.com/2026/04/anthropics-claude-mythos-finds.html
- 内容: Anthropic のプレビューモデル「Claude Mythos」が主要なOS・ブラウザを横断して脆弱性を自律的に発見・検証する「Project Glasswing」の取り組みを報じたニュース記事。
- 便利さ: セキュリティ運用担当者にとって、AIによる脆弱性診断がどの水準まで自動化されつつあるかの外形的な把握に役立つ。
- 注意点: プレビュー段階のモデルであり、一般提供時期・利用条件は流動的。導入検討は正式リリース後の情報を待つのが無難。

---

## 3. インフラ/クラウドエンジニア・SRE・CI/CD・Playwrightによる自動化

### playwright-skill（Claude Code Skill for browser automation）
- 出典: https://github.com/lackeyjb/playwright-skill
- 内容: Claude Code の「Skill」機能（モデルが自律的に呼び出す拡張機能）として、Playwright（ブラウザ自動操作ツール）を使ったテスト・検証コードを Claude が自律的に記述・実行できるようにするOSSプロジェクト。
- 便利さ: モデル呼び出し型のため、都度スクリプトを人間が書かなくても Claude がテストシナリオに応じて自動でPlaywrightコードを生成・実行してくれる。CI/CD（継続的インテグレーション／継続的デリバリー）パイプラインへの組み込みイメージが湧きやすい。
- 注意点: GitHub上の個人／コミュニティ発OSSのため、本番導入前にコードレビューとセキュリティ確認は自前で行う必要がある。

### Playwright MCP & Claude Code: AI-Powered Test Automation Guide
- 出典: https://testomat.io/blog/playwright-mcp-claude-code/
- 内容: MCP（Model Context Protocol＝AIモデルと外部ツールを連携させる標準規格）経由で Playwright サーバーをClaude Codeに接続し、AIがブラウザテストを自動化する手順を解説した専門メディアの記事。
- 便利さ: MCPサーバーのセットアップからテストカバレッジ向上までの流れが体系立っており、QA（品質保証）担当者がAI活用のテスト自動化を始める際の入門として使いやすい。
- 注意点: 認証情報を伴うテスト環境で使う場合は、機密情報がログや生成コードに残らないよう運用ルールを事前に設計する必要がある。

---

## 4. ベストプラクティス、実際に構築・検証して効果があった手順書/実績

### Claude Code for Infrastructure as Code: A Practical Guide
- 出典: https://spacelift.io/blog/claude-code-for-infrastructure-as-code
- 内容: IaC（Infrastructure as Code＝インフラ構成をコードで管理する手法）にClaude Codeを適用する実践ガイド。「本番環境への変更は必ず人間のレビュー・承認を経てから適用する」というHITL（Human-in-the-Loop＝人間の確認を介在させる運用）を明確な原則として掲げている。
- 便利さ: 「エージェントに自由に下書きさせ、本番適用前に人間がレビューする」という運用フローは、Optimus自身の運用ルール（AGENTS.md）とも整合しており、社内展開時の参考になる。
- 注意点: Terraform等の特定IaCツールを前提にした記述もあるため、自社の構成管理ツールとの適合性は個別確認が必要。

### How Anthropic teams use Claude Code（Anthropic公式PDF）
- 出典: https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf
- 内容: Anthropic社内チームが、定型的なデータエンジニアリング作業の自動化、複雑なインフラ障害のトラブルシューティング、技術者以外のメンバーもデータ操作できるドキュメント化されたワークフローづくりに Claude Code を活用している事例を紹介する一次情報。
- 便利さ: 開発元自身の社内活用事例のため、機能の想定用途や運用思想を正確に把握できる。ドキュメント化を重視する姿勢はチーム展開時の参考になる。
- 注意点: PDF形式の資料でURLが長いため、社内共有時はリンク切れに備えてアーカイブ保存を推奨。

---

## 5. GitHubのawesomeシリーズ

### awesome-claude-skills（ComposioHQ）
- 出典: https://github.com/ComposioHQ/awesome-claude-skills
- 内容: Claude Skills・Plugins（拡張機能）を1,000件以上収録した大規模キュレーションリスト。Claude.ai や Claude Code だけでなく、Codex・Cursor・Gemini CLI・Antigravity など他のコーディングエージェントでも使える汎用スキルも横断的にカバー。
- 便利さ: カテゴリ別に整理されているため、自社の業務（レポート作成、コードレビュー、ドキュメント生成等）に近いスキルを探す際の起点として有用。星（Star）数が多く継続更新されているため信頼性も高い。
- 注意点: 収録数が膨大なため、個々のスキルの品質・保守状況にはばらつきがある。導入前に更新日・Issue状況を確認することを推奨。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
