# Claude/Claude Code/Cowork 業務自動化ナレッジ（2026-08-10）— Excel自動化実践記・Project Glasswing脆弱性発見・GitLab CI/CD公式統合

作成日: 2026-08-10 / STATUS: INFO / TOPIC: CLAUDEAUTO

## 今週のテーマ

今週は Claude（Anthropic の AI モデル）と Claude Code（コーディング特化のCLI＝コマンドラインツール）による業務自動化動向のうち、前週とは異なる切り口を中心に収集しました。「Excel 自動化の実践記」「Anthropic の脆弱性発見プロジェクト Project Glasswing の続報」「GitLab CI/CD への公式統合」「SRE（Site Reliability Engineering＝サイト信頼性エンジニアリング）向けインシデント対応エージェントの公式クックブック」「community 発の Awesome リスト」の5カテゴリで整理しています。いずれも一次情報源（公式サイト・公式ドキュメント・実践者のnote記事）を優先しました。

---

## 1. ITインフラ/サーバ運用保守のルーティンワーク自動化（PPT・Excel特化）

### ClaudeCodeでエクセル作業を自動化してみた ── 毎日30分の時短に成功した話
- 出典: https://note.com/hima_hito/n/nc8dbb597ed48
- 内容: 月末の売上データCSVからグラフ付きレポートを作成しPDF化する作業（毎回30分）を、Claude Codeへの指示だけでopenpyxl（PythonでExcelファイルを操作するライブラリ）を使った全自動処理に置き換えた実践記。集計・グラフ作成・書式設定までを一気通貫で自動化した過程が具体的に書かれています。
- 便利さ: 個人の実体験ベースのため「実際にどれだけ時短できたか」が定量的に分かりやすく、同様の月次レポート業務を持つ現場でそのまま参考にしやすい構成です。
- 注意点: 個人ブログ（note）のため、社内の機密データを扱う場合は同じ手順をそのまま使わず、データの取り扱い・保存先を自社ルールに合わせて再設計する必要があります。

### 【2026年最新】Claude Codeでパワポ自動作成｜編集可能PPTX無料公開
- 出典: https://uravation.com/media/claude-code-japanese-pptx-skill/
- 内容: 日本企業・官公庁向け資料フォーマットに対応したPPTX（PowerPoint形式）自動作成用の「Skill」（Claude Codeが自律的に呼び出す拡張機能）を無料公開している記事。導入手順とプロンプト例が示されています。
- 便利さ: 日本語の文書レイアウト（体裁・フォント・レイアウト慣習）に配慮したテンプレート設計がされており、海外製ツールにありがちな「レイアウト崩れ」の手直しコストを抑えられる点が実務的です。
- 注意点: 無料公開スキルは提供元企業のプロモーションを兼ねる場合があるため、本番導入前にライセンス条件と生成物の権利関係を確認してください。

---

## 2. ゼロデイ攻撃対策・セキュリティ運用の自動化

### Project Glasswing: An initial update（Anthropic公式）
- 出典: https://www.anthropic.com/research/glasswing-initial-update
- 内容: Anthropic が2026年4月に開始した「Project Glasswing」（AIモデル Claude Mythos Preview を使い、世界の重要ソフトウェアの脆弱性を先回りして発見・修正する防御的サイバーセキュリティの取り組み）の初期進捗報告。約50のパートナー団体と協力し、1万件超の高〜重大深刻度の脆弱性を発見したと公式発表しています。
- 便利さ: セキュリティ運用担当者にとって、AIによる大規模脆弱性発見がどのスケール・体制で実運用されているかを一次情報から把握できる貴重な資料です。パッチ適用のリードタイム確保という運用思想が明確に示されています。
- 注意点: Claude Mythos Preview 自体は限定パートナーのみに提供される非公開モデルであり、一般企業がすぐに同様のスキャンを利用できるわけではありません。自社導入は正式な提供形態の発表を待つ必要があります。

---

## 3. インフラ/クラウドエンジニア・SRE・CI/CD・Playwrightによる自動化

### Claude Code GitLab CI/CD（Anthropic公式ドキュメント）
- 出典: https://code.claude.com/docs/en/gitlab-ci-cd
- 内容: Claude Code を GitLab CI/CD（継続的インテグレーション／継続的デリバリーのパイプライン機能）に組み込む公式手順。ANTHROPIC_API_KEY をCI/CD変数として設定し、Merge Request（GitLabにおけるプルリクエスト相当）上でClaudeが変更提案やブランチ作成を自動で行う流れが解説されています。
- 便利さ: GitLab自身がメンテナンスする公式統合のため信頼性が高く、`allowedTools` によるツール許可範囲の制御など、セキュリティ設定を含めた実装の勘所が明記されています。
- 注意点: 本執筆時点でベータ版であり、機能・仕様が今後変わる可能性がある旨が公式に明記されています。本番パイプラインへの組み込みは段階的に検証してください。

### Build an SRE incident response agent with Claude Managed Agents（Anthropic公式クックブック）
- 出典: https://platform.claude.com/cookbook/managed-agents-sre-incident-responder
- 内容: PagerDuty（インシデント管理ツール）のWebhookをトリガーにClaude Managed Agent（Anthropicが提供するマネージド型エージェント基盤）を起動し、チームのランブック（対応手順書）に沿って自動でログ・インフラコードを調査するSREエージェントの構築チュートリアル。
- 便利さ: 公式クックブック形式でコード例が完結しており、「アラート発生→調査→対応案の提示」までの一連の流れをどう実装するか、具体的な設計図として利用できます。
- 注意点: サンドボックス環境内でのbash/read/edit操作を前提とするため、本番インフラへの直接操作権限を与える場合はアクセス制御・監査ログの設計を別途厳格に行う必要があります。

---

## 4. ベストプラクティス、実際に構築・検証して効果があった手順書/実績

### The Claude Code SRE Handbook
- 出典: https://har-ki.github.io/claude-code-sre-handbook/handbook/
- 内容: 汎用コーディングエージェントであるClaude CodeをKubernetes（コンテナオーケストレーションツール）環境の実際の障害シナリオ（本番相当のチェックアウトサービスの競合状態など）に対して実運用し、検証結果をまとめたハンドブック。アラートを起点にドラフトPR（プルリクエスト）を自動生成する「watcher」の仕組みも紹介されています。
- 便利さ: 実際の障害再現テストに基づく検証結果（成功例・失敗例双方）が公開されており、「AIエージェントにどこまで運用作業を任せられるか」の現実的な線引きを考える材料になります。
- 注意点: 個人／コミュニティによる検証プロジェクトのため、記載の効果が自社のKubernetes構成でも同様に再現するとは限りません。導入検討時は自社環境での小規模検証を推奨します。

---

## 5. GitHubのawesomeシリーズ

### awesome-claude-code（jqueryscript）
- 出典: https://github.com/jqueryscript/awesome-claude-code
- 内容: Claude Code のツール・ワークフロー・連携事例を横断的にまとめたキュレーションリスト。「45 tips for getting the most out of Claude Code」など、システムプロンプトの圧縮やGemini CLIとの連携といった実践的なTipsも収録されています。
- 便利さ: 単なるツール紹介にとどまらず、運用ノウハウ（Tips集）へのリンクも整理されているため、Claude Code の基本操作から一歩進んだ活用法を探す起点として使いやすい構成です。
- 注意点: リンク集の性質上、個々の外部リポジトリの保守状況・セキュリティは玉石混交です。導入前に更新頻度・Star数・Issue対応状況を確認することを推奨します。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
