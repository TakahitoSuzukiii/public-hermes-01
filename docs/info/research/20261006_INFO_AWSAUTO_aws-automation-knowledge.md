作成日: 2026-10-06 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-10-06

今週のテーマは「**コスト/パッチのレポート自動化」「検知→自動修復の配線」「GitHub Actions×CDKの鍵なしデプロイ（OIDC）**」です。前週までのConfig/Cost Anomaly/CDK Pipelinesとは別角度の話題を中心に選びました。
※本記事は検索結果の概要情報をもとに自分の言葉で要約したものです。詳細は各出典をご確認ください。

## 1. ITインフラ/サーバ運用保守の自動化（レポート・コスト・棚卸し）

### Lambda + EventBridge Scheduler + Cost Explorer APIで日次/週次コストレポートを自動配信
Lambda（サーバを持たずにコードを実行するサービス）からCost Explorer API（料金データ取得API）を呼び、集計結果をSES（メール送信サービス）やSlackへ送る構成です。EventBridge Scheduler（定時起動サービス）で自動実行し、S3にも保存すれば記録が残ります。レポート自動化の最小構成として参考になります。
出典: https://dev.to/bhatiagirish/automate-aws-cost-usage-report-using-event-bridge-lambda-ses-s3-aws-cost-explorer-api-3j3n ／ https://dev.to/ragul_21/automating-aws-cost-management-reports-with-lambda-d90

### Lambda + CloudWatchで「ムダ」を探して片付ける・止める
未使用リソースの検出、夜間・休日のリソース停止スケジュール、コストポリシーの強制といった「削減の自動化」の整理記事です。報告だけでなく是正まで自動化したい場合の設計の足がかりになります。
出典: https://oneuptime.com/blog/post/2026-02-12-automate-cost-optimization-with-lambda-and-cloudwatch/view

### AWS公式：FinOps自動化と「信頼」の考え方（2026-09-10）
FinOps（クラウド費用を財務と技術で管理する活動）の自動化を、AWSがどう捉えているかを述べた公式ブログです。自動化結果をどう信頼・検証するかという観点があり、運用ルール作りの参考になります。
出典: https://aws.amazon.com/blogs/aws-cloud-financial-management/category/aws-cloud-financial-management/aws-cost-explorer/

## 2. セキュリティ・脆弱性管理の自動化

### Security Hub → EventBridge → Lambda/Step Functions/SSMの自動対応
Security Hub（セキュリティ検出結果の集約サービス）の検出結果をEventBridge（イベント連携サービス）に流し、Lambda・Step Functions（処理の流れを制御）・SNS（通知）・SSMを起動して自動修復する公式手順です。基本の配線を確認するのに最適です。
出典: https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cloudwatch-events.html ／ https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-v2-automations.html

### GuardDuty/Macie/Security Hubのイベントをまとめて自動対応（2026-05）
EventBridgeルールでGuardDuty（脅威検知）やMacie（機密データ検出）のイベントも捕捉し、修復ワークフローにつなぐ実践記事です。サービスごとにバラバラにせず、一つの仕組みに集約する考え方が学べます。
出典: https://www.haggath.re/blog/leveraging-eventbridge-for-security-automation/

### Bedrock + Systems Managerで検出結果の修復を加速（AWS公式・2024）
生成AI（Amazon Bedrock）で検出結果から修復手順を導き、SSM Automationで実行するパターンです。記事自体は2024年ですが、AIと自動修復の組み合わせの原型として押さえておく価値があります。なお実行権限は最小限にし、本番適用前に承認ステップを挟むのが安全です。
出典: https://aws.amazon.com/blogs/machine-learning/building-automations-to-accelerate-remediation-of-aws-security-hub-control-findings-using-amazon-bedrock-and-aws-systems-manager/

## 3. IaC・CI/CD・Systems Manager運用自動化・SRE

### AWS DevOps Agentでパッチ失敗の原因分析を自動化（AWS公式・2026-07-30）
Systems Manager Patch Managerでパッチ適用が失敗すると、コマンドID・インスタンスID・エラー状態を含むイベントが発行されます。これを契機にAWS DevOps Agent（運用調査を支援するAIエージェント）が原因分析を自動で始める、イベント駆動の構成が紹介されています。「失敗の一次切り分けを自動化する」SRE（サイト信頼性エンジニアリング）的な好例です。
出典: https://aws.amazon.com/blogs/mt/autonomous-root-cause-analysis-for-aws-systems-manager-patch-failures-using-aws-devops-agent/

### Patch Managerの基本手順（ベースライン・スキャン・コンプライアンス確認）
EC2のパッチ適用自動化を、SSM Agent準備→パッチベースライン（適用ルール）→スキャン用Association→準拠状況の確認という流れで説明する入門ガイドです。あわせて、Fleet Manager・Session Manager・Run Commandの本番活用をまとめた記事（2026-10-05）もあります。
出典: https://streaver.com/insights/blogs/automating-patch-management-on-cloud-systems ／ https://osamaoracle.com/2026/10/05/aws-systems-manager-fleet-management-patch-automation-and-session-manager-in-production/

### GitHub Actions × CDKを「アクセスキーなし」で：OIDC連携
OIDC（OpenID Connect、外部IDで一時的な認証を行う仕組み）で、GitHub ActionsからIAMロールを引き受けるとアクセスキーの保管が不要になります。要点は次のとおりです。
- IAMロールの信頼ポリシーで `sub`（どのリポジトリ/ブランチか）を必ず絞る。ワイルドカードのみは避ける
- ワークフローに `id-token: write` 権限が必要
- 環境ごとにロールを分け、本番はGitHub Environmentsの承認者を設定する
- CDKでは新規作成なら `OidcProviderNative`（CloudFormation標準リソース利用）が推奨
- GitHub公式ドキュメントによると、2026-07-15以降に作成したリポジトリ等では `sub` にオーナー/リポジトリの不変IDが含まれる場合があるため、信頼ポリシーの形式確認が必要
出典: https://docs.github.com/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services ／ https://aws.amazon.com/blogs/security/use-iam-roles-to-connect-github-actions-to-actions-in-aws/ ／ https://towardsthecloud.com/blog/aws-cdk-openid-connect-github ／ https://github.com/aws-samples/github-actions-oidc-cdk-construct

## 4. ベストプラクティス・手順書

### Systems Manager Automation Runbookリファレンス
AWSが提供済みの修復・運用用Runbook（自動化手順書）一覧と必要なIAM権限が載った公式リファレンスです。ゼロから作る前に既存Runbookを探す習慣が、保守コスト削減に有効です。
出典: https://docs.aws.amazon.com/systems-manager/latest/userguide/automation-documents-reference.html

## 今週のまとめ（実践のヒント）
- 「報告」から始め、安定したら「是正」へ。自動修復は承認ステップと最小権限を付ける
- 失敗イベント（パッチ失敗等）をトリガーに調査を自動化すると、運用負荷が下がる
- 長期アクセスキーはOIDCで廃止し、信頼ポリシーを絞る

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
