作成日: 2026-11-03 / STATUS: INFO / TOPIC: AWSAUTO

# AWS業務自動化ナレッジ（週次 2026-11-03号）

今週のテーマは「**守る・戻す・壊して確かめる**」です。先週まではコスト監視やSecurity Hubの修復が中心だったため、今回は **バックアップ×マルウェア対策**、**障害注入（カオスエンジニアリング）**、**パッチ運用の標準化**、**Lambdaの新しいワークフロー機能** など、別ジャンルを選びました。出典は各リンク先で、要約は自分の言葉で書いています。

## 1. ITインフラ/サーバ運用保守の自動化

### Systems Manager Automationで「自己修復ランブック」を作る
- ランブック（runbook）＝運用手順を自動実行できる形にした手順書。SSM Automationは、EC2の再起動やスナップショット取得などを手順化し、アラームから自動で呼び出せる。
- 2026-10-24付の AWS Builder Center 記事が、障害時の復旧を自動化する設計を解説。
- 出典: https://builder.aws.com/content/3L8JfyBpo3a1Sn6XZHyBc9vH8B4/aws-systems-manager-automation-build-self-healing-devops-runbooks-for-aws
- 公式の定義済みランブック一覧: https://docs.aws.amazon.com/systems-manager/latest/userguide/automation-documents-reference.html

### Patch Managerによる段階的パッチ適用の手順書
- Patch Manager＝OSパッチの適用・準拠状況の確認を自動化するSSMの機能。
- 少数のサーバで先に試し、問題なければ本番へ広げる「段階展開」、適用前のスナップショット取得、準拠状況を証跡として残す流れを初心者向けにまとめた実践手順（2026-07、サードパーティ記事）。
- 出典: https://www.kbytechnologies.com/graduate/cloud-infrastructure-and-operations/automated-ec2-patch-compliance-with-aws-systems-manager
- 補足（2026-04、AWS Builder Center）: https://builder.aws.com/content/3CpaUa4eWYvZrjLtRtLi8dky4UO/automating-patch-management-with-aws-systems-manager

## 2. セキュリティ・脆弱性管理の自動化

### GuardDuty Malware Protection for AWS Backup：S3連続バックアップに対応（2026-05-26）
- バックアップの中身をマルウェアスキャンし、「どの時点に戻せば安全か」を判定できる。ランサムウェア（身代金要求型マルウェア）対策として有効。
- 新API `GetPITRMalwareScanResults` で、復元前に特定時点が安全か確認できる（PITR＝Point-In-Time Recovery、任意の時点への復元）。
- 出典: https://aws.amazon.com/about-aws/whats-new/2026/05/amazon-guardduty-aws-backup-s3-continuous/

### 感染した復旧ポイントの復元を自動でブロックする構成
- 検出（THREATS_FOUND）→ EventBridgeがLambdaを起動 → 復旧ポイントに `ScanStatus: INFECTED` タグ付与 → SCP（Service Control Policy、組織全体の権限制限）で `backup:StartRestoreJob` を拒否、という流れ。タグ削除も拒否して回避を防ぐのがポイント。SNS通知とフォレンジック用アカウントへのコピーも任意で可能。
- 出典: https://aws.amazon.com/blogs/storage/orchestrate-automated-response-for-amazon-guardduty-malware-protection-for-aws-backup-at-scale/

### FSx for Windowsのファイルをマルウェアスキャン（GuardDuty for S3流用）
- FSxの変更をLambdaでS3に同期し、GuardDuty S3保護でスキャン。脅威検出時は隔離フォルダへ移動しSNS通知。失敗時はDLQ（処理失敗メッセージの退避キュー）で再試行。
- 出典: https://aws.amazon.com/blogs/storage/automated-malware-scanning-for-amazon-fsx-for-windows-file-server-with-guardduty-protection-for-amazon-s3/

## 3. IaC・CI/CD・SRE

### Resilience Hubの「推奨レジリエンステスト」（FISベース）
- Fault Injection Service（FIS）＝わざと障害を起こして耐性を検証する仕組み。次世代Resilience Hubが、AZ障害・依存先の障害・マルチリージョン分離/復旧のテストを自動生成し、RTO（目標復旧時間）に対して合否と報告書を出す。
- 四半期ごとなど定期実行が可能。最初は単一の「ソフト依存」から始めるのが推奨。
- 出典: https://aws.amazon.com/blogs/architecture/recommended-resilience-testing-in-the-next-generation-of-aws-resilience-hub/
- Well-Architected信頼性の柱の考え方（CI/CDに組み込み回帰テスト化）: https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/rel_testing_resiliency_failure_injection_resiliency.html

### Lambda durable functionsの上限緩和（2026-10-13）
- durable functions＝最大1年続く多段階処理を、チェックポイント付きでLambda内に書ける機能。待機中は課金されない。
- 1実行あたりの操作数が3,000→30,000、チェックポイントが256KB→1MBに拡大。ポーリングや失敗時のロールバック処理を持つ運用ワークフローが組みやすくなった。
- 出典: https://aws.amazon.com/about-aws/whats-new/2026/10/aws-lambda-durable-gen-limit-increase/
- 使い分け（durable／Step Functions／EventBridge）: https://docs.aws.amazon.com/lambda/latest/dg/workflow-event-management.html

## 4. ベストプラクティス・手順書

### Control Tower × Config適合パックで組織全体にガードレールを展開
- Control Towerの検出ガードレールを適合パックとして組織レベルで一括配布でき、除外アカウント指定も可能。`put-organization-conformance-pack` コマンドで実施。
- 出典: https://aws.amazon.com/blogs/mt/extend-aws-control-tower-governance-using-aws-config-conformance-packs/
- サンプルテンプレート集（AI/ML基盤向けなど新カテゴリ有り）: https://docs.aws.amazon.com/config/latest/developerguide/conformancepack-sample-templates.html

### AWS Backup Audit Managerでバックアップ運用を監査自動化
- バックアップが基準（頻度・保持期間・暗号化等）を満たすかを継続評価し、日次の監査レポートを自動生成。
- 出典: https://docs.aws.amazon.com/ja_jp/aws-backup/latest/devguide/aws-backup-audit-manager.html

## 今週のまとめ（実践のヒント）
1. 「バックアップがあるから安心」ではなく、**安全な時点か**を自動検査する層（GuardDuty×Backup）を足す。
2. 障害対応は手順書→SSMランブック化→FISで定期的に試験、の順で成熟させる。
3. 組織全体のルール配布は適合パック、監査はBackup Audit Managerなど、既存機能の組み合わせで追加コストを抑える。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
