作成日: 2026-11-24 / STATUS: INFO / TOPIC: AWSAUTO

# AWS業務自動化ナレッジ（週次 2026-11-24）

## 今週のテーマ

今週は「**ルールで見張り、違反したら自動で直す**」をテーマにします。先週までは「Inspector→Systems Managerで即パッチ」や「コストレポート」が中心でした。今週は新しく **AWS Config（設定の記録・評価サービス）の自動修復**、**Conformance Pack（ルール一括パック）の組織展開**、**cdk-nag（IaCをデプロイ前に検査するツール）**、**Security Hub の EventBridge 連携**を取り上げます。「事後対応」から「デプロイ前に止める＋違反を自動修復」へ視点を広げる回です。

※出典は各リンク先の公式情報です。内容は自分の言葉で要約しています。

## 1. ITインフラ運用保守の自動化

### 1-1. Systems Manager Automation の標準Runbook一覧を知る
- Systems Manager Automation（運用作業を手順書化して自動実行する機能）には、AWS・AWS Support・AWS Config が提供する**定義済みRunbook（自動実行用の手順書）**が多数あります。サービス別に整理された公式リファレンスがあり、「まず自作する前に既製品を探す」のが近道です。
- 使いどころ: EC2の再起動、AMI作成、スナップショット整理、セキュリティグループ修正など。
- 出典: https://docs.aws.amazon.com/systems-manager-automation-runbooks/latest/userguide/automation-runbook-reference.html

### 1-2. 自己修復（セルフヒーリング）Runbookの考え方
- AWS Builder Centerの記事で、Systems Manager Automationを使い、繰り返しの運用作業を標準化して手作業ミスを減らす考え方が紹介されています。
- ポイント: 最初は「通知のみ→承認付き実行→完全自動」と段階的に自動化度を上げると安全です。
- 出典: https://builder.aws.com/content/3L8JfyBpo3a1Sn6XZHyBc9vH8B4/aws-systems-manager-automation-build-self-healing-devops-runbooks-for-aws

## 2. セキュリティ／脆弱性管理の自動化

### 2-1. AWS Config の自動修復（Auto Remediation）【新ジャンル】
- AWS Config は、リソースの設定変更を記録し、ルールに沿っているか（準拠／非準拠）を判定します。
- 非準拠のリソースに**修復アクション**を紐づけられ、**手動実行／自動実行**を選べます。実体は Systems Manager Automation のRunbookです。
- 例: 「S3バケットが公開されていた」→ 自動でパブリックアクセスをブロック。
- 注意: 自動修復は本番に影響しうるため、最初は手動修復で挙動を確認し、対象を絞って自動化するのが無難です。
- 出典: https://docs.aws.amazon.com/config/latest/developerguide/setup-autoremediation.html

### 2-2. Conformance Pack を組織全体へ展開
- Conformance Pack（Configルールと修復アクションをまとめた「パック」）を、AWS Organizations 配下の全アカウントへ一括展開できます。CIS等の基準向けサンプルテンプレートもあります。
- 前提: 各アカウントでConfig記録を有効化、成果物用S3バケット（名前が `awsconfigconforms` で始まる）を用意。
- 初めてなら「Operational Best Practices for Amazon S3」パックが分かりやすい入門です。
- 出典: https://aws.amazon.com/blogs/mt/deploying-conformance-packs-across-an-organization-with-automatic-remediation/
- カスタムルール＋修復の組合せ: https://aws.amazon.com/blogs/mt/manage-custom-aws-config-rules-with-remediation-using-conformance-packs/

### 2-3. Security Hub / Inspector の検知を EventBridge で自動対応につなぐ
- Security Hub は検知結果（Finding）をほぼリアルタイムでEventBridgeへ送ります。ルールを書けば、Lambda実行・Step Functions起動・SNS通知・チケット連携などを自動化できます。
- Inspector も同様にイベントを出します。例えば「重大度がHIGHまたはCRITICAL、かつ状態がACTIVE」の検知だけをSNSへ通知するルールを、公式がJSONパターンで示しています。
- 注意: Inspectorのイベントは**リージョンごと**にルール設定が必要です（ベストエフォート配信）。
- 出典（Security Hub）: https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cloudwatch-events.html
- 出典（Inspector）: https://docs.aws.amazon.com/inspector/latest/user/findings-managing-automating-responses.html

## 3. IaC・CI/CD・運用自動化

### 3-1. cdk-nag でCDKをデプロイ前に検査する【新ジャンル】
- cdk-nag は、AWS CDK（コードでインフラを定義するフレームワーク）のスタックやCloudFormationテンプレートを、ルールパックで自動チェックするOSSです（cdklabs管理）。
- パックの例: AWS Solutions、HIPAA、NIST 800-53、PCI DSS、Serverless。
- 例: 「S3が暗号化されていない」「IAMにワイルドカード権限がある」を `cdk synth` 時にエラー化。意図的な例外は理由付きで抑制（suppress/acknowledge）します。
- CI/CDに組み込むと、違反があればパイプラインを止められます（AWS公式のパイプライン参照アーキテクチャでも採用）。
- 注意: 最新READMEでは `Validations.of(app).addPlugins(...)` という新しい書き方になっています。古い記事の `Aspects` 方式とバージョン差があるため、利用バージョンのドキュメントを確認してください。
- 出典: https://github.com/cdklabs/cdk-nag/ ／ https://aws.amazon.com/blogs/devops/manage-application-security-and-compliance-with-the-aws-cloud-development-kit-and-cdk-nag/

## 4. ベストプラクティス

### 4-1. Well-Architected「運用上の優秀性」の柱
- 自動化・可観測性（監視で状態を把握する力）・インシデント対応を継続改善する柱です。
- 「検知（Config/Security Hub）→判断（EventBridgeルール）→実行（Systems Manager）→振り返り」の流れを設計に入れる際の指針になります。
- 出典: https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/welcome.html

## 5. GitHub／コスト自動化の補足
- コスト週次レポート（EventBridge Scheduler＋Lambda＋Cost Explorer API＋SES）は引き続き定番です。実装例: https://builder.aws.com/content/3IN9u3uPo1tCMZax3admnTqreyC/building-an-automated-aws-cost-monitoring-system-using-lambda-and-cost-explorer
- 個人ブログ・サンプルは利用前にコードを確認してください。

## 今週の実践ヒント
1. まずは **Config のマネージドルール1〜2個（例: S3公開禁止）＋手動修復** で試す。
2. 慣れたら対象タグを絞って自動修復へ。
3. CDKを使っているなら、cdk-nag を CI に入れて「違反コードを本番に入れない」入口対策を追加。
4. 検知は EventBridge の重大度フィルタで絞り、通知疲れを避ける。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
