作成日: 2026-11-10 / STATUS: INFO / TOPIC: AWSAUTO

# AWS業務自動化ナレッジ（週次 2026-11-10）

## 今週のテーマ
今週は「**ズレ（ドリフト）を見つけて、安全に直す**」を軸に集めました。IaC（Infrastructure as Code：インフラをコードで管理する手法）のドリフト（コードと実環境のズレ）検知、Security Hub等の検知結果を自動で処理する仕組み、コスト日次レポートの自動化、そして運用棚卸しに使えるGitHubのスクリプト集です。
※本記事は各出典の要点を自分の言葉で要約したものです。詳細は必ず原文をご確認ください。

---

## 1. ITインフラ運用保守の自動化（コスト・棚卸し）

### 1-1. Lambda + Cost Explorer で日次コスト監視
- 内容: EventBridge Scheduler（時刻で処理を起動する仕組み）→ Lambda（サーバ不要でコードを実行するサービス）→ Cost Explorer（AWS料金の集計API）で、日次・月初来のサービス別コストを取得し、SES（メール送信サービス）等で通知するサーバレス構成の解説。
- ポイント: 「毎朝、勝手にコストが届く」状態を最小構成で作れる。小さく始めて、閾値超過の警告を足していくのが現実的。
- 出典: https://builder.aws.com/content/3IN9u3uPo1tCMZax3admnTqreyC/building-an-automated-aws-cost-monitoring-system-using-lambda-and-cost-explorer

### 1-2. 無駄リソースの掃除とスケジュール停止
- 内容: Lambda と CloudWatch（監視サービス）で、使われていないリソースの洗い出し、時間帯での起動停止、コストポリシーの強制を行う自動化パターン。
- 注意: 削除系の自動化は、まず「通知のみ」で運用し、誤検知がないと確認してから実行系へ進めるのが安全。
- 出典: https://oneuptime.com/blog/post/2026-02-12-automate-cost-optimization-with-lambda-and-cloudwatch/view （第三者ブログ）

### 1-3. GitHubの棚卸しスクリプト集（優先度5）
- `paulbayer/Inventory_Scripts`: Organizations配下の全アカウント・リージョンのEC2、VPC、CloudFormationスタックを横断で一覧化。VPC一覧は読み取り専用で安全寄り。https://github.com/paulbayer/Inventory_Scripts
- `crahan/aws-scripts`: 全リージョンのEBS暗号化状況、EC2のIMDS（インスタンスメタデータ取得方式）設定、RDSの暗号化・公開有無、S3のHTTPS強制/暗号化などをシェルで一覧化。監査の下調べに便利。https://github.com/crahan/aws-scripts
- `nishantthorat/awesome-aws-cloud`: 棚卸しツール（Cloud Custodian、ScoutSuite、Cartography等）へのリンク集。https://github.com/nishantthorat/awesome-aws-cloud
- 注意: 個人リポジトリが中心でStar数は多くない。実行前にコードを読み、読み取り権限のみのIAMロールで試すこと。

---

## 2. セキュリティ・脆弱性管理の自動化

### 2-1. Security Hub → EventBridge → Lambda の自動対応パイプライン
- 内容: Security Hub CSPM（設定の不備を継続チェックするサービス）がGuardDuty（脅威検知）やInspector（脆弱性スキャン）の検知結果を集約し、EventBridgeで条件に合うものだけLambdaに渡して自動対応する構成。IAM Access Analyzer（外部公開や未使用権限の検出）の併用も紹介。
- 出典: https://builder.aws.com/content/3J2sfi4KhtsrCMDGx8hp2HZikus/building-an-automated-cloud-security-response-pipeline-with-aws-security-hub-guardduty-eventbridge-and-lambda
- 一次情報（公式）: https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cloudwatch-events.html
- 公式ブログ（カスタムアクションで手動承認しつつ修復するプレイブック例）: https://aws.amazon.com/blogs/security/automated-response-and-remediation-with-aws-security-hub/
- GuardDuty側の公式手順: https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_eventbridge.html

**初心者向けの勘所:** 重大度（Severity）ごとに「通知のみ」「自動修復」を分けると事故が減ります。

---

## 3. IaC・CI/CD・運用自動化

### 3-1. Terraformドリフト検知＋重大度で分岐する自動修復（aws-samples）
- 製品/条件: Terraform管理のAWS環境で、コードと実環境がズレたとき。
- 仕組み: EventBridge（定期起動）→ Step Functions（処理の流れ管理）→ CodeBuild（`terraform plan`実行）→ Lambda（変更の重大度判定）。判定は次のとおり。
  - 重大（セキュリティグループ、IAMポリシー、KMSキー）/ 高（EC2、RDS、Lambda、ALB等）: SNSで通知し、人の承認を待つ
  - 低（タグや説明文のみの変更）: `terraform apply`で自動修復
- 設計上の注意: 1回のplanに重大変更が混ざると、全体が承認待ちになる（Terraformは部分適用が難しいため）。ワークスペースを危険度別に分けると緩和できる。
- 出典: https://github.com/aws-samples/sample-terraform-drift-detection/blob/main/README.md

### 3-2. IaCドリフトの検知・予防・修復の整理
- CloudFormation: EventBridgeで夜間/週次にLambdaを起動し`DetectStackDrift`（ドリフト検知API）を実行。IAMロール、セキュリティグループ、S3バケットポリシーなど影響の大きい種類に絞って通知するとノイズが減る。
- Terraform/OpenTofu: `terraform plan -refresh-only -detailed-exitcode`を定期実行し、終了コード2＝ズレありとして通知。
- 緊急時のコンソール手動変更: CloudTrailのイベントをEventBridgeで拾い、IaCへ反映するIssueを自動起票する案。
- 修復方針の目安: 手動変更が正しかった→コード側を更新（import）/ 誤変更→コードの状態へ上書き。
- 出典: https://builder.aws.com/content/3LNt6VjbXZsJkCl42cPEBBxppxk/infrastructure-as-code-drift-detection-prevention-and-remediation-on-aws
- 補足: 「検知」と「修復」は別操作に分ける原則を解説する記事も参照。 https://builder.aws.com/content/3IN7ojgHzH3j5hY67RydhCqPdq8/detecting-infrastructure-drift-in-aws-with-terraformopentofu

### 3-3. TerraformのCI/CD検証パターン（AWS規範ガイダンス）
- 内容: CodePipelineで checkout → validate（tfsec、TFLint、checkov等の静的チェック）→ plan → apply（テスト環境）→ destroy の5段階で設定を検証する。
- 制約: 単一アカウント・単一リージョン前提。複数環境へは設定変更が必要。
- 出典: https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/create-a-ci-cd-pipeline-to-validate-terraform-configurations-by-using-aws-codepipeline.html

---

## 4. ベストプラクティス
- Systems Manager Automation の定義済みRunbook（手順書）は、AWS・Support・Config提供のものが一覧化されている。自作前にまず既製品を探すのが近道。https://docs.aws.amazon.com/systems-manager-automation-runbooks/latest/userguide/automation-runbook-reference.html

---

## 今週のまとめ（運用への示唆）
1. 検知は自動、**修復は危険度に応じて人の承認を挟む**設計が共通のベストプラクティス。
2. コスト通知は小さなサーバレス構成から始められる。
3. 棚卸しはまず読み取り専用スクリプトで現状把握から。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
