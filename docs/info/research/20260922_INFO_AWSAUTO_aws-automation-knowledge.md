作成日: 2026-09-22 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-09-22

今週はAWS（Amazon Web Services、Amazonが提供するクラウドサービス群）の運用自動化ナレッジの中から、**Compute Optimizer（AIによるリソース最適化提案サービス）を使ったコスト削減の自動化**、**Amazon Inspector（脆弱性の静的スキャンサービス）とAWS Configの自動修復**、**Security Hub Central Configuration（複数アカウントのセキュリティ設定一元管理機能）**、**GitHub Actions × OIDC（パスワード不要の認証方式）によるキーレスCI/CD**、**次世代AWS Resilience Hub（回復性評価サービス）の生成AI障害分析**という5テーマを中心に、前週（9/15）・前々週（9/8）と重複しないサービス・切り口を厳選しました。

---

## 1. ITインフラ/サーバ運用保守の自動化（レポート・コスト・棚卸し生成）

### AWS Compute Optimizerで月次コスト削減を自動化する実装パターン
Untanbaby Blogの実践記事では、AWS Compute Optimizer（CloudWatch（監視サービス）のメトリクスを機械学習で分析し、EC2・Auto Scaling・EBS（ストレージ）・Lambda・ECS Fargate（コンテナ実行サービス）・RDS（データベース）・NAT Gatewayの各リソースに最適なサイズを推奨するサービス）を活用し、実際に月あたり大幅なコスト削減を達成した事例を紹介しています。別のガイド記事（aws-cert-lab）では、推奨事項を手動確認するだけでなく、指定した基準に合致した場合に自動でリソースサイズ変更を適用する「Automation」機能の設定手順も解説されており、「レコメンドを見て終わり」ではなく「適用まで自動化する」棚卸し運用の実装例として参考になります。
出典: https://untanbaby.com/blog/aws/aws-compute-optimizer-2600-mo5l35xu/ ／ 公式: https://docs.aws.amazon.com/ja_jp/compute-optimizer/latest/ug/automation.html

### AWS Backup Audit Managerでバックアップ監査レポートを自動生成
AWS公式ドキュメントによると、AWS Backup Audit Manager（バックアップ運用のコンプライアンス状況を自動監査する機能）は24時間ごとに新しいレポートを自動生成し、Amazon S3（オブジェクトストレージサービス）へ自動発行します。EC2はDLM（Data Lifecycle Manager）、RDSは自動バックアップ、S3はバージョニングとサービスごとに分散しがちなバックアップ設定を、AWS Backupで一元管理しつつ、定期的な監査レポート作成まで自動化できる点が、複数リソースを抱える現場での棚卸し業務に直結します。
出典: https://docs.aws.amazon.com/ja_jp/aws-backup/latest/devguide/aws-backup-audit-manager.html ／ 実践解説: https://qiita.com/OhkuboT/items/77be1e798244319bc9c0

---

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### Amazon Inspectorによる脆弱性の静的スキャンとGuardDutyとの役割分担
Zennの整理記事では、Amazon GuardDuty（脅威検知サービス）が「実行時の不審な挙動を動的に検知する」のに対し、Amazon Inspector（ワークロードを自動発見しソフトウェアの脆弱性や意図しないネットワーク露出を継続的にスキャンするサービス）は「静的にCVE（既知の脆弱性情報）を検出する」という役割分担が整理されています。有効化するだけで運用負荷なくEC2・ECR（コンテナイメージ）・Lambda関数のスキャンが自動的に走る仕組みのため、「動的検知（GuardDuty）」と「静的スキャン（Inspector）」を両輪で組み合わせることが、ゼロデイ対策の土台として推奨されています。
出典: https://zenn.dev/ncdc/articles/1c73366849d7d7 ／ 比較解説: https://tomodahinata.com/blog/aws-guardduty-vs-security-hub-detective-inspector-macie-comparison-guide

### AWS Configの自動修復：Lambda方式とSSM Automation方式の比較
NRIネットコムの技術ブログでは、AWS Config（AWSリソースの構成をポリシーに照らして評価するサービス）が非準拠と判定したリソースを自動修復する2つの方式――①Lambda関数を自作して修復ロジックを書く方式、②AWS標準のSSM Automation（Systems Managerの自動化手順書）を修復アクションとして紐づける方式――のメリット・デメリットを比較しています。「自由度は高いが保守コストがかかるLambda方式」と「コーディング不要だが柔軟性に制約があるSSM Automation方式」を使い分ける判断軸が実務的です。
出典: https://tech.nri-net.com/entry/security_notification_and_automatic_repair_function

### Security Hub Central Configurationでマルチアカウントのセキュリティ設定を一元化
カミナシのエンジニアブログでは、AWS Security Hub（セキュリティ検出結果の統合管理サービス）の「Central configuration（中央集権的な設定管理機能）」を使い、Organizations（複数アカウント管理サービス）配下の全アカウント・全リージョンに対して、標準の有効化やコントロールのパラメータを一括適用する運用を解説しています。これまではアカウントごとに個別設定が必要だった作業が、委任管理者アカウントからの一括操作で完結し、新規アカウント追加時も自動的に同じセキュリティ基準が適用される点が、組織全体のガバナンス自動化に直結します。
出典: https://kaminashi-developer.hatenablog.jp/entry/2024/04/09/090000 ／ 公式: https://docs.aws.amazon.com/securityhub/latest/userguide/central-configuration-intro.html

---

## 3. IaC・CI/CD・Lambda/EventBridge/Systems Managerによる運用自動化・SRE

### GitHub Actions × OIDCでアクセスキー不要のAWS CDKデプロイパイプラインを構築
複数の技術ブログ（クラスメソッド、KUDs Blog等）が2026年に公開した実装記事では、GitHub ActionsからAWSへデプロイする際、長期間有効なIAMアクセスキーを保存する代わりに、OIDC（OpenID Connect、外部サービスとAWSを短期トークンで安全に連携する認証方式）を使ったキーレス認証でAWS CDK（プログラミング言語でインフラを定義するIaCフレームワーク）のデプロイを自動化する手順を解説しています。「mainブランチへのpushで自動デプロイ」という基本形に加え、IAM IDプロバイダーの信頼ポリシー設定など、キー漏えいリスクを構造的になくす設計が今後のCI/CD運用の標準になりつつあります。
出典: https://dev.classmethod.jp/articles/github-actions-oidc-aws-cdk-deploy/ ／ 実践解説: https://kuds.blog/aws/github-actions-oidc-s3-deploy/

### 次世代AWS Resilience Hub：生成AIによる障害モード分析と組織横断レポート
AWS公式ブログ（2026年5月29日）によると、刷新された次世代版のAWS Resilience Hub（アプリケーションの回復性を定義・検証・追跡するサービス）は、新しいアプリケーションモデル、依存関係の自動発見、そして生成AIによる障害モード分析（Failure Mode Analysis）機能を搭載しました。従来は専門家が手作業で洗い出していた「このコンポーネントが落ちたら何が起きるか」という障害シナリオの洗い出しをAIが支援し、モジュール化された回復性ポリシーと組織全体のレポート機能で、SRE運用の可視化を効率化する狙いです。
出典: https://aws.amazon.com/blogs/aws/introducing-the-next-generation-of-aws-resilience-hub-for-generative-ai-based-sre-resilience-journey/

---

## 4. コミュニティ知見（GitHub）

### awesome-serverless-blueprints：AWSサーバーレス構成のベストプラクティス集
`ran-isenberg/awesome-serverless-blueprints`は、AWS Lambda・EventBridge・Step Functions等を使ったサーバーレスアーキテクチャの実装例（ブループリント）を、ベストプラクティスに沿ってまとめたcuratedリスト（厳選リンク集）です。個々のサービス単体の解説ではなく「実際に動くサーバーレス構成一式」を参照できるため、運用自動化の仕組みを新規に設計する際の出発点として有用です。
出典: https://github.com/ran-isenberg/awesome-serverless-blueprints

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
