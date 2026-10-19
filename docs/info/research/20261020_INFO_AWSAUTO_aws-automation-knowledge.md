作成日: 2026-10-20 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-10-20

今週のテーマは **「検知して終わり」から「直して閉じる」まで**。脆弱性（Inspector）の修復をSystems Managerで自動化する手順、AWS公式の自動修復ソリューション（ASR）、コスト異常検知の通知自動化、GitHub ActionsからのOIDC接続を取り上げます。先週までの内容（パッチ管理基本、ドリフト検知等）とは別の切り口を選んでいます。

> 注: 各項目は出典を要約・紹介したものです。詳細は出典URLをご確認ください。

## 1. ITインフラ/サーバ運用保守の自動化（コスト・レポート）

### Lambda + EventBridge Schedulerで利用料を自動監視（サーバーワークス）
- 出典: https://blog.serverworks.co.jp/notify-aws-cost-using-lambda-and-eventbridge
- EventBridge Scheduler（時刻指定で処理を起動するサービス）でLambdaを定時起動し、Cost Explorer API（コスト取得API）の結果をSlackへ通知する構成。月初からの累計に加え、前月比・直近1週間の日次推移・異常検知まで見られる点が特徴。

### Cost Anomaly Detection（コスト異常検知）× EventBridge
- 出典: https://docs.aws.amazon.com/cost-management/latest/userguide/cad-eventbridge.html
- 機械学習で「いつもと違う支出」を検知するサービス。検知結果をEventBridge（イベントを受けて処理へつなぐ仕組み）で受け取れるので、チャット通知やチケット起票を自動化できる。
- 補足: Budgetsは「しきい値超え」、Anomaly Detectionは「急な変化」に強く、併用が現実的。

## 2. セキュリティ・脆弱性管理の自動化

### Inspector検出 → Systems Managerで該当パッケージだけ自動パッチ（AWS公式ブログ）
- 出典: https://aws.amazon.com/blogs/mt/automate-vulnerability-management-and-remediation-in-aws-using-amazon-inspector-and-aws-systems-manager-part-1/
- Amazon Inspector（脆弱性スキャナ）の検出結果から、影響を受けるパッケージ（例: curl）だけをPatch Manager（パッチ適用機能）で更新する Automation runbook（自動化手順書）を紹介。Security Hubのカスタムアクションで手動起動する形で、**ワンクリックで対象を絞って修復**できる。
- 再起動あり/なしを選べ、メンテナンス時間まで再起動を遅らせる運用も可能。修復後、Inspector側が自動で finding（検出結果）を Closed にする。マルチアカウント・マルチリージョン対応。

### Inspectorの検出結果をEventBridgeでカスタム通知（AWS公式ドキュメント）
- 出典: https://docs.aws.amazon.com/ja_jp/inspector/latest/user/findings-managing-automating-responses.html
- `severity` が HIGH/CRITICAL かつ `status` が ACTIVE のイベントだけをSNSへ流すルールの作り方が日本語で解説されている。通知の乱立を避ける最初の一歩として有用。

### Automated Security Response on AWS（ASR・GitHub公開、Apache-2.0）
- 出典: https://github.com/aws-solutions/automated-security-response-on-aws ／ https://docs.aws.amazon.com/solutions/automated-security-response-on-aws/
- Security Hubの検出結果を、Systems Manager Automationの修復手順（Playbook）で自動/ワンクリック修復するAWS公式ソリューション。未使用アクセスキー、開放されたセキュリティグループ、公開S3バケット等に対応。CIS・FSBP・PCI DSS・NIST 800-53に準拠。
- Step Functionsで複数アカウントを横断し、実行ログ・SNS通知・Jira/ServiceNow連携も備える。取得時点でStar約486、最新リリース v3.1.7（2026-06-22）と保守は継続中。
- 導入のコツ: まず手動実行で検証し、非本番で確認後、個別の修復だけ自動化する。

## 3. IaC・CI/CD・SRE

### GitHub Actions + OIDCで「アクセスキーなし」のTerraform/CDKデプロイ
- 出典: https://stategraph.com/blog/ci-cd-pipeline-for-terraform ／ https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/optimize-multi-account-serverless-deployments.html
- OIDC（OpenID Connect、外部IDで一時権限を得る仕組み）により、長期のアクセスキーをGitHubに置かずに済む。信頼ポリシーの `sub` 条件でリポジトリ/ブランチ/環境を絞るのが肝。
- 実践ポイント: planは読み取り専用、applyは書き込み権限に分離／本番applyは手動承認／`id-token: write` を必要なジョブだけに付与。マルチアカウントでは中央ロール→CDK bootstrapロールの二段構えが公式パターン。

## 4. ベストプラクティス

### Well-Architectedに Digital Sovereignty Lens が追加
- 出典: https://aws.amazon.com/blogs/architecture/category/aws-well-architected/
- 主権（データ所在地・運用管理）を意識したワークロード設計の追加ガイダンス（Lens＝特定分野向けの観点集）。規制対応が必要な組織は目を通す価値あり。

## 今週のまとめ（実践のヒント）
- 修復は「手動ワンクリック → 一部自動化」と段階的に。いきなり全自動にしない。
- 通知は重大度で絞る（HIGH/CRITICALのみ等）。
- コストは「しきい値（Budgets）」と「異常検知」の二本立て。
- CI/CDの認証はOIDCで一時権限化し、鍵の漏えいリスクを根本から減らす。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
