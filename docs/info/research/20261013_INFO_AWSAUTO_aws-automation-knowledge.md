作成日: 2026-10-13 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-10-13

今週のテーマは「**IaCのドリフト検知（設定のズレの自動発見）**」「**Terraform×GitHub Actionsの安全なCI/CD**」「**Operational Excellence（運用の卓越性）の"運用をコード化"**」「**GuardDuty/Security Hubの自動対応サンプル集**」です。前週までのコスト通知・OIDC基礎・Patch Manager単体とは別角度を選びました。
※本記事は検索結果の概要情報をもとに自分の言葉で要約したものです。詳細は各出典をご確認ください。

## 1. ITインフラ/サーバ運用保守の自動化

### AWS Cloud Operations Best Practices：集中運用管理のパッチ管理ガイド
AWSのサンプル集（aws-samples）にある運用ベストプラクティス集です。Systems Manager Patch Manager（OSパッチ適用を自動化するサービス）を使った複数台の一括パッチ適用と、ゼロデイ（修正パッチ公開直後の緊急脆弱性）等、重大度が高い場合の考え方がまとまっています。社内手順書の下敷きに向きます。
出典: https://aws-samples.github.io/cloud-operations-best-practices/docs/guides/centralized-operations-management/patch-management/

### Systems Managerの用途別ベストプラクティス（AWS公式）
Systems Managerの各機能について、典型的な使い方と推奨設定、関連ブログへのリンクが一覧できます。「どの機能から導入するか」の地図として便利です。
出典: https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-best-practices.html

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### GuardDuty・Security Hubの検出結果をEventBridgeで自動処理（AWS公式）
GuardDuty（不審な挙動を見つける脅威検知サービス）やSecurity Hub（セキュリティ検出結果の集約サービス）の結果は、EventBridge（イベント振り分けサービス）に流せます。重大度ごとに通知だけ行う／Lambdaで自動対処する、と振り分けるのが基本形です。
出典: https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_eventbridge.html ／ https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cloudwatch-events.html

### GitHubの実装例：検知→隔離までをTerraformで構築（ToluGIT/aws-unified-threat-detection）
Security Hub・GuardDuty・Inspectorで検知し、EventBridge→Step Functions（処理の流れを組む仕組み）→Lambda→SNS通知、そして侵害されたEC2を隔離用セキュリティグループへ移すところまでをTerraformで定義した例（2026-07更新）。仕組み全体を学ぶ教材として有用です。ただし個人リポジトリなので、そのまま本番利用せず参考に留めるのが無難です（Star数等は未確認）。
出典: https://github.com/ToluGIT/aws-unified-threat-detection

## 3. IaC・CI/CD・SRE

### Terraform用CI/CD：PRでplan、mergeでapply、毎日ドリフト検知
- PR時に`terraform plan`の結果をコメント表示し、mainへのmerge時だけ`apply`する
- OIDC連携で長期アクセスキーを置かない。plan用ロールとapply用ロール（mainブランチ限定）を分け、悪意あるPRがapplyできないようにする
- `concurrency`で`cancel-in-progress: false`にし、apply中断による中途半端な状態を防ぐ
- 定期実行の`plan -detailed-exitcode`（終了コード2＝差分あり）でドリフトを検知し、GitHub Issueで通知。既存Issueを再利用して通知乱立を防ぐ
出典: https://syseng.io/blog/github-actions-terraform-cicd

### ドリフト検知付きIaCパイプライン（AWS Builder Center）
ドリフト（IaCの定義と実環境のズレ。コンソールでの手動変更が主因）に対し、EventBridge→Lambda/CodeBuildで定期plan、CloudTrailで「誰が変えたか」を特定、Slack通知までの閉ループを紹介。対処方針として「低リスクは自動復旧、IAM・ネットワーク・データ層は承認ステージ必須」というハイブリッド運用が現実的です。
出典: https://builder.aws.com/content/3GOTOCD3dE9YBkJW4rEyEXdRymE/cicd-pipeline-for-infrastructure-as-code-with-drift-detection-on-aws

### 最小構成のドリフト検知：GitHub Actions＋SES＋CloudWatch（seunayolu/terraform-drift-detection）
定期ワークフローでドリフトを検知し、SES（メール送信）とCloudWatch Logsに記録する小さな実装例。依存を増やしたくない場合の参考になります。
出典: https://github.com/seunayolu/terraform-drift-detection

## 4. ベストプラクティス・手順書

### Well-Architected：Operational Excellence（運用上の優秀性）の柱
設計原則の一つが「運用をコードとして実行する（Perform operations as code）」。Runbook（定型作業の手順書）とPlaybook（原因不明時の調査手順書）をSystems Manager Automationで自動化する考え方です。AWS公式ブログとハンズオン用のGitHubサンプルがあります。
出典: https://docs.aws.amazon.com/wellarchitected/latest/operational-excellence-pillar/welcome.html ／ https://aws.amazon.com/blogs/mt/achieving-operational-excellence-using-automated-playbook-and-runbook/ ／ https://github.com/aws-samples/achieving-operational-excellence-using-automated-playbook-and-runbook

## 今週のまとめ（実践のヒント）
- 「デプロイ自動化」だけでなく「ズレの検知」まで自動化して初めてIaCは完結する
- 自動復旧は低リスクに限定し、重要資源は人の承認を挟む（HITLの考え方と同じ）
- 検知結果は重大度で振り分け、通知の乱立を避ける
- 手順書は文章で終わらせず、Runbookとしてコード化する

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
