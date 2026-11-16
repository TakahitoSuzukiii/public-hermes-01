作成日: 2026-11-17 / STATUS: INFO / TOPIC: AWSAUTO

# AWS業務自動化ナレッジ（週次 2026-11-17）

## 今週のテーマ
今週は「**止める・守る・標準化する**」を軸に集めました。使っていない時間帯にサーバを自動停止してコストを減らす仕組み、脆弱性（ぜいじゃくせい：攻撃に悪用されうる弱点）の検知から修正までの自動化、そして運用手順書（Runbook）をコード化する考え方です。
※本記事は各出典の要点を自分の言葉で要約したものです。詳細は必ず原文をご確認ください。

---

## 1. ITインフラ運用保守の自動化（コスト・棚卸し）

### 1-1. Instance Scheduler on AWS（EC2/RDSの自動起動・停止）
- 出典: https://docs.aws.amazon.com/solutions/instance-scheduler-on-aws/ ／ https://github.com/aws-solutions/instance-scheduler-on-aws
- AWS公式の「ソリューション」（すぐ展開できる構成済みテンプレート）。リソースに付けたタグとLambda（サーバ管理不要でコードを動かすサービス）を使い、EC2・Auto Scalingグループ・RDS（マネージドDB）を決めた時間に自動で起動/停止します。
- 使っていない夜間・休日に止めるだけでコスト削減になります。CDK（コードでインフラを定義するツール）でもデプロイ可能、Apache 2.0ライセンス。
- ポイント: 本番は止めない、検証環境のみ対象にするなど、タグで対象を絞るのが安全です。

### 1-2. RDSの自動停止・起動を自前で作る（Lambda＋EventBridge／Systems Manager）
- 出典: https://aws.amazon.com/blogs/database/save-costs-by-automating-the-start-and-stop-of-amazon-rds-instances-with-aws-lambda-and-amazon-eventbridge/ ／ https://aws.amazon.com/blogs/database/schedule-amazon-rds-stop-and-start-using-aws-systems-manager/
- タグの値で停止/起動時刻を指定する方式（Lambda版）と、Systems Manager State Manager（望ましい状態を維持する機能）版の2通りが紹介されています。小さく始めるならLambda版、既にSystems Managerを使っているなら後者が管理しやすいです。
- 注意: RDSは停止しても一定期間（公式仕様で上限あり）で自動再起動される点を確認してください。

### 1-3. Cost Explorer APIで週次/月次コストレポートをメール・Slack配信
- 出典: https://builder.aws.com/content/2dKeNrWeMj8E1Yh6CXITS7Hg0cU/automate-aws-cost-report-using-eventbridge-lambda-cost-explorer-api ／ https://github.com/antstackio/cloud-cost-alert ／ https://github.com/ysoares0209/aws-costs-report-automation
- EventBridge Scheduler（時刻で処理を起動する仕組み）→ Lambda → Cost Explorer API（コスト取得API）→ SES（メール送信）／S3（保存）／Slackという王道構成です。
- `cloud-cost-alert`（AWS SAMで構築）は、週次コスト、月次予測、未使用リソース（低稼働EC2、未接続EBS、放置スナップショット、アイドルのRDS/LB等）の棚卸しを複数リージョンで行いSlackに通知する構成。ただしStar数がまだ少ない新しいリポジトリなので、そのまま使わず**コードを読んで参考にする**のが無難です。
- 週次コストレポートの自動化は、レポート作成の手作業を減らす入口として費用対効果が高いです。

---

## 2. セキュリティ／脆弱性管理の自動化

### 2-1. Inspector検知 → Security Hubのカスタムアクション → Systems Managerで即パッチ
- 出典: https://aws.amazon.com/blogs/mt/automate-vulnerability-management-and-remediation-in-aws-using-amazon-inspector-and-aws-systems-manager-part-1/
- Amazon Inspector（脆弱性スキャナ）が見つけた弱点を、Security Hub（検知結果の集約サービス）上でワンクリック（カスタムアクション）してSystems ManagerのAutomation Runbook（自動実行手順）を起動し、該当パッケージだけを更新します。
- 緊急の脆弱性（ゼロデイ等）で定期パッチ日を待てない時の「オンデマンド修正」の型です。再起動あり/なしを選べ、なしなら保守時間帯に回せます。修正後はInspectorの検知が自動でCLOSEDになります。
- 制約: Linuxかつ EC2のパッケージ脆弱性が対象（ネットワーク到達性やECRのコンテナイメージは対象外）。記事は2022年のもので、Windows対応など現在の仕様は公式で再確認してください。

### 2-2. 「条件を満たした時だけ」自動で直すパターン（タグ・重大度で制御）
- 出典: https://builder.aws.com/content/3LcqcbLXiefCQhlkxGezBI14YmD/from-cve-to-patch-automatic-remediation-with-amazon-inspector-and-systems-manager
- 流れ: Inspector → EventBridge（重大度HIGH/CRITICALかつ修正版あり、の時だけ反応）→ SSM Automation（`AutoPatch=true`タグがあるか確認）→ Patch Manager（パッチ適用・必要なら再起動）→ 検証 → SNS通知。
- 工夫: タグで「自動で直してよいサーバ」を選別。本番DBを昼間に勝手に再起動する事故を防ぐ、というガードレール（安全柵）の考え方が参考になります。

### 2-3. Security Hubの「自動化ルール」と組織横断のインシデント対応
- 出典: https://aws.amazon.com/blogs/security/aws-security-hub-launches-a-new-capability-for-automating-actions-to-update-findings/ ／ https://aws.amazon.com/blogs/mt/best-practices-to-respond-to-security-risks-across-your-aws-organizations/
- Security Hubの自動化ルールは、取り込まれた検知結果の重大度変更・抑制・メモ追加をコード（Lambda）無しで自動化できます。例: 重要アカウントの検知は自動でCriticalに、受容済みリスクは自動で抑制。
- 後者は、Security Hubで優先度付け → EventBridgeで自動応答 → Systems Managerの修復Runbookという多アカウント向けの運用設計を解説しています。

---

## 3. IaC／運用自動化（CDK・Systems Manager）

### 3-1. Systems Manager AutomationのRunbookをCDKで書く・テストする
- 出典: https://aws.amazon.com/blogs/mt/build-aws-systems-manager-automation-runbooks-using-aws-cdk/
- Document CDK Libraryを使うと、RunbookをTypeScript等で記述し、YAML/JSONへ出力、さらにAPI呼び出しをモックして**デプロイ前にローカルでシミュレーションテスト**できます。繰り返し部分を部品化して標準化できるのも利点です。
- 関連: Terraformで作るなら cloudposse の `terraform-aws-ssm-patch-manager`（https://github.com/cloudposse/terraform-aws-ssm-patch-manager）が、パッチベースライン・メンテナンスウィンドウ・ログ用S3をまとめて構築します（利用前にコードの確認を推奨）。

---

## 4. ベストプラクティス（Well-Architected）

### 4-1. 手順書(Runbook/Playbook)を段階的に自動化する
- 出典: https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_ready_to_support_use_runbooks.html ／ https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/ops_event_response_auto_event_response.html ／ https://aws.amazon.com/blogs/mt/achieving-operational-excellence-using-automated-playbook-and-runbook/
- Runbook＝作業手順書、Playbook＝障害調査手順書。Well-Architected（AWSの設計指針）は、まず文章で書く → 他の人に試してもらい検証 → 短くて頻度の高いものから自動化、の順を推奨しています。
- 自動化の安全策として、レート制限・エラー閾値・承認（`aws:approve`でSNS経由の承認ゲート）を入れる考え方が示されています。共通処理は`aws:executeAutomation`で部品化。
- 設計原則「Safely automate where possible（安全に自動化する）」は、本記事全体の通奏低音です。

---

## 5. GitHub（awesome系）
- https://github.com/donnemartin/awesome-aws ／ https://github.com/brandonhimpfen/awesome-aws
- AWSのライブラリ・ツール・ガイドを集めたキュレーションリスト。ツール探しの起点として使えます。ただしリストは更新頻度に差があるため、採用前に最終更新日・Star数・ライセンスを確認してください。

---

## 今週の実践ヒント
1. まず**検証環境の夜間停止**（1-1）から始めると、効果が見えやすくリスクも低いです。
2. 脆弱性の自動修正は**タグで対象を限定**し、通知（SNS）を必ず付けること。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
