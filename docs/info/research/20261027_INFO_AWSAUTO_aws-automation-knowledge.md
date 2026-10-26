作成日: 2026-10-27 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-10-27

今週のテーマは「**直す作業まで自動化する**」です。検知して通知するだけでなく、Security Hubの修復プラン、ASR（自動セキュリティ対応）のAIツールキット、Systems Managerの診断機能など、2026年8〜10月に発表された新機能を中心に紹介します。出典は各リンクをご確認ください（要約は筆者の言葉です）。

## 1. ITインフラ/サーバ運用保守の自動化

### Systems Managerが「管理不能なEC2」の原因診断を拡充（2026-09-09発表）
- 出典: https://aws.amazon.com/about-aws/whats-new/2026/09/systems-manager-diagnoses-ec2-unmanaged/
- Systems Manager（SSM）は、EC2をパッチ適用・コマンド実行・接続などで操作するための運用管理サービスです。インスタンスがSSMの「管理対象（managed）」でないと、これらは使えません。
- 従来はネットワーク接続の診断のみでしたが、新たにIAM権限、SSM Agentのバージョン、ステータスチェック、OS設定、Default Host Management Configuration、ハイブリッド有効化の6分野も診断できます。原因ごとに手順が表示され、一部はAutomation runbook（自動化手順書）でそのまま修復できます。
- 実践ヒント: 「パッチが当たらないサーバがある」という棚卸し作業の入口として有効です。診断はAutomation課金対象です。

### SSMの運用変更点（ドキュメント履歴より）
- 出典: https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-release-history.html
- Application Managerは2026-07-30から新規利用受付を終了、Advanced-instancesティアは廃止（ハイブリッド/他クラウドのノードは従量課金へ）。Automationはリソース監視にrunbook実行IDを使うようになったため、権限の見直しが必要です。
- 関連: Azure VMもCloud Connector経由でSSMから管理可能に。 https://aws.amazon.com/about-aws/whats-new/2026/06/aws-systems-manager-multicloud-vm/

### EC2のコスト自動制御（Lambda + EventBridge）
- 出典: https://builder.aws.com/content/3JMJZewMiHPHi3z3kBRgNdyMCG6
- 低稼働のEC2をタグとCloudWatchメトリクスで判定し、スケジュール実行のLambdaで停止する定番パターンです。EventBridgeはイベント/スケジュールでサービスを起動する仕組みです。
- 注意: 本番を誤停止しないよう、「停止対象タグ」を付けたものだけを対象にするのが安全です（個人ブログ系の実装例はあくまで参考）。

## 2. セキュリティ・脆弱性管理の自動化

### Security Hubの「修復プラン」（2026-10-01発表）
- 出典: https://aws.amazon.com/about-aws/whats-new/2026/10/aws-security-hub-remediation-plans/
- 同じ根本原因を持つ複数の露出（exposure）をまとめ、1か所直せば複数が解消する形で提示します。優先度（Critical〜Low）と、AWS CLI／Terraform／CloudFormation／Python／CDKの手順例付き。APIでAIエージェントが取得して修正を自動化することも想定されています。Security Hub Essentialsプランで追加料金なし。

### Automated Security Response on AWS（ASR）にAIツールキット（2026-08-31発表）
- 出典: https://aws.amazon.com/about-aws/whats-new/2026/08/automated-security-response-adds-AI-toolkit/
- ASRは検出結果を自動修復するAWS公式ソリューションです。新機能は、(1) AIアシスタントでカスタム修復を生成（安全ガードレール付き）、(2) Inspector／GuardDuty／Macieの検出も自動修復対象に、(3) アカウント/OU/リージョン/タグ単位の設定コンソール、(4) Email/Slack/Jira/ServiceNowへの通知。
- 運用上の注意: 完全自動修復は失敗時に最大3回（15分以上の間隔）で再試行を止める仕様です。 https://docs.aws.amazon.com/solutions/latest/automated-security-response-on-aws/enable-fully-automated-remediations.html

### Security Hub自動化ルールの考え方（AWS Security Blog）
- 出典: https://aws.amazon.com/blogs/security/streamline-security-response-at-scale-with-aws-security-hub-automation/
- 「特定の検出に対しLambdaを呼び出す／タグ付けする／設定を修正する／IAM権限を絞る」といった修復パターンが整理されています。

### Inspectorスキャンのクロスアカウント定期化（規範ガイダンス）
- 出典: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/automate-security-scans-for-cross-account-workloads-using-amazon-inspector-and-aws-security-hub.html
- CloudFormationでEventBridgeのcron、Inspectorスキャン、Security Hub集約、SNS通知までを一括構築するパターンです。

## 3. IaC・CI/CD・SRE

### AMS Trusted Remediator：推奨事項116件の自動修復
- 出典: https://aws.amazon.com/blogs/mt/optimize-cost-and-automate-security-remediation-with-ams-trusted-remediator/
- Trusted Advisor、Security Hub CSPM、Compute Optimizerの推奨を、複数アカウントで一括自動修復します（セキュリティ64、コスト16、耐障害性17など）。組織のバックログ化しがちな推奨事項の消化に向きます。

## 4. ベストプラクティス・手順書

### AWS Config適合パック（Conformance Packs）
- 出典: https://docs.aws.amazon.com/config/latest/developerguide/conformance-packs.html
- Configルールと修復アクションを1セットにして、アカウント/組織全体へ展開できます。IaCに入れておけばガバナンスの標準化が容易です。
- 応用例: PQC（耐量子暗号）対応状況をConfigで棚卸しするスキャナ https://aws-news.com/article/2026-05-14-automating-post-quantum-cryptography-readiness-using-aws-config （第三者記事）

## 今週のまとめ（実践のヒント）
- 「検知→通知」から「検知→優先順位付け→修復」へ。Security Hub修復プランとASRの組み合わせは検討価値大。
- 自動修復は必ず小さな範囲（タグ/OU単位）から開始し、承認フローや再試行上限を確認すること。
- SSMの仕様変更（ティア廃止、権限）は既存環境に影響しうるため棚卸しを推奨。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
