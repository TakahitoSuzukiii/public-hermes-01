作成日: 2026-09-29 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-09-29

今週はAWS（Amazon Web Services、Amazonが提供するクラウドサービス群）の運用自動化ナレッジの中から、**AWS Cost Anomaly Detection（コスト異常検知サービス）とChatbot連携による異常通知の自動化**、**AWS Config Conformance Pack（適合パック）による組織横断ガバナンス**、**Automated Security Response on ASWへのAIツールキット追加**、**AWS Systems Manager Patch Manager（パッチ適用自動化）**、**CDK Pipelinesのマルチアカウント対応CI/CD**、**AWS Well-Architected Agent（生成AIによる環境診断エージェント）**という6テーマを中心に、前週（9/22）・前々週（9/15、9/8）と重複しないサービス・切り口を厳選しました。

---

## 1. ITインフラ/サーバ運用保守の自動化（レポート・コスト・棚卸し生成）

### AWS Cost Anomaly DetectionをAWS Chatbot経由でSlack通知する構成をTerraformで自動化
クラスメソッドの実践記事では、AWS Cost Anomaly Detection（機械学習でコストの異常な増加を自動検知するサービス）が検知した異常を、AWS Chatbot（AWSの通知をSlack等のチャットツールへ橋渡しするサービス）経由でSlackチャンネルへ自動通知する一式のリソースを、Terraform（構成をコードで宣言的に管理するIaCツール）でまとめて構築する手順を紹介しています。閾値を固定するのではなく機械学習ベースで「いつもと違う支出」を検知できるため、想定外のコスト急増（設定ミスによるリソース起動しっぱなし等）に即座に気づける棚卸し・監視の自動化事例です。
出典: https://dev.classmethod.jp/articles/cost-anomaly-detection-slack-terraform/ ／ 解説: https://zenn.dev/cureapp/articles/cost-anomaly-detection

### AWS Config Conformance Packで組織全体のガバナンスルールを一括配布
AWS公式ブログとサーバーワークスの技術ブログでは、AWS Config（AWSリソースの構成をポリシーに照らして評価するサービス）のConformance Pack（複数のConfig RuleとRemediation（自動修復設定）をまとめてテンプレート化した機能）を使い、Organizations（複数アカウント管理サービス）配下の全アカウントへガバナンスルールを一括デプロイする運用を解説しています。1アカウントずつルールを設定する手間をなくし、新規アカウント追加時にも同じ基準が自動適用される点が、複数環境を抱える現場の構成棚卸しに直結します。
出典: https://aws.amazon.com/jp/blogs/news/aws-config-conformance-packs/ ／ 実践解説: https://blog.serverworks.co.jp/config/conformance-pack

---

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### Automated Security Response on AWSにカスタム修復用のAIツールキットが追加
AWS公式の「What's New」（2026年8月）によると、AWSが提供するソリューション「Automated Security Response on AWS」（Security Hubの検出結果を自動修復する定型ソリューション）に、カスタム修復ロジックの作成を支援するAIツールキットが追加されました。これにより、Amazon Inspector（脆弱性の継続スキャンサービス）・Amazon GuardDuty（脅威検知サービス）・Amazon Macie（機密データ検出サービス）の検出結果に対し、アカウント／組織単位（OU）／リージョン／リソースタグ単位で自動修復の適用範囲を絞り込みつつ、強化されたWebコンソールから一元設定できるようになりました。「検知はできるが修復ロジックを書く余力がない」という現場の負担を、AI支援によって下げる狙いです。
出典: https://aws.amazon.com/jp/about-aws/whats-new/2026/08/automated-security-response-adds-AI-toolkit/ ／ 詳細: https://docs.aws.amazon.com/solutions/latest/automated-security-response-on-aws/multi-service-remediation.html

### GuardDuty・Inspector・Config・Security Hubを組み合わせた検知〜自動対応フローの全体設計
Acrovisionの技術記事では、Amazon GuardDuty単体では「万全ではない」という前提のもと、AWS Config（構成管理・証跡）、Amazon Inspector（脆弱性評価）、AWS Security Hub（一元集約）、Amazon EventBridge（イベント連携）を組み合わせ、検知後に手動対応・自動対応いずれのフローにも接続できる設計思想を整理しています。個々のサービスを単発で導入するのではなく「検知→集約→対応」という一連のパイプラインとして設計する重要性が、ゼロデイ対策の実務観点でまとめられています。
出典: https://www.acrovision.jp/service/aws/amazon-guardduty-aws-cloudwatch/

---

## 3. IaC・CI/CD・Lambda/EventBridge/Systems Managerによる運用自動化・SRE

### AWS Systems Manager Patch Managerによるパッチ適用の自動化
Qiitaおよびusize-techの技術ブログでは、AWS Systems Manager Patch Manager（OS・アプリケーションのパッチ適用を自動化する機能）を使い、EC2インスタンス群へのセキュリティパッチ適用をスケジュール実行する手順を解説しています。パッチベースライン（適用するパッチの承認ルール）を定義し、メンテナンスウィンドウ（保守作業を許可する時間帯）と組み合わせることで、「手作業でサーバーに順番にログインしてパッチを当てる」運用から「定義したポリシー通りに自動適用される」運用へ移行できる点が、AWS Well-Architected Labsのオペレーショナルエクセレンス（運用の卓越性）分野の実践例としても紹介されています。
出典: https://blog.usize-tech.com/aws-ssm-patch-manager/ ／ 実践解説: https://qiita.com/chanhama/items/3945831a8278e34ee358

### CDK Pipelines 2026年版：マルチアカウント対応のCI/CD構築
Untanbaby Blogの解説記事では、AWS CDK（プログラミング言語でインフラを定義するIaCフレームワーク）のCDK Pipelines機能を使い、単一のGitリポジトリからクロスアカウント・クロスリージョンへのデプロイを自動化するマルチアカウント構成の構築手順をまとめています。開発・検証・本番といった複数のAWSアカウントにまたがるデプロイを、CloudFormation CDK v2.130.0以降の最新機能セットで一本化できる点が、CI/CDパイプラインの拡張パターンとして参考になります。
出典: https://untanbaby.com/blog/cdk-pipelines-2026-ci-cd-mo5nmg6o

---

## 4. ベストプラクティス（Well-Architected等）

### AWS Well-Architected Agent（プレビュー）：生成AIによる環境診断エージェント
クラスメソッドの記事では、プレビュー公開されたAWS Well-Architected Agent（AWS環境を分析し、コスト・セキュリティ・パフォーマンス・回復性にまたがる優先順位付き改善提案を生成AIが自動作成するサービス）を紹介しています。これまでは人手でチェックリスト（Well-Architected Framework）に沿って環境をレビューしていた作業を、生成AIエージェントが実環境の構成を読み取って自動診断する点が新しく、「レビューの自動化」がAIエージェントの領域に広がってきていることを示す事例です。
出典: https://dev.classmethod.jp/articles/aws-wa-agent-preview/

---

## 5. コミュニティ知見（GitHub）

### sebastianmarines/awesome-aws：本家停止後を引き継ぐコミュニティ維持フォーク
定番のcuratedリスト（厳選リンク集）`donnemartin/awesome-aws`が2023年5月以降更新停止となったのを受け、`sebastianmarines/awesome-aws`がコミュニティメンテナンスとして情報の正確性維持・レビューを引き継いでいます。AWSライブラリ・OSSリポジトリ・ガイド・ブログ等の情報源を探す際、リンク切れや古い情報が少ない継続更新版として参照する価値があります。
出典: https://github.com/sebastianmarines/awesome-aws

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
