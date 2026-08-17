# AWS サービス学習メモ・リンク集

各AWSサービスの概要・特徴・実装ノウハウをまとめたものです。実装コード・設定値は一般的なパラメータ名のみで、アカウントID等の機密値は含まれていません。

## 共通・全般
- Awesome: [Awesome AWS](https://github.com/donnemartin/awesome-aws), [Awesome AWS ECS](https://github.com/nathanpeck/awesome-ecs), [Awesome AWS Amplify](https://github.com/dabit3/awesome-aws-amplify)
- ロードマップ: [Roadmap AWS Best Practices](https://roadmap.sh/best-practices/aws)
- classmethod記事: [2023年AWS全サービスまとめ](https://dev.classmethod.jp/articles/aws-summary-2023/)、[AWS再入門2024記事一覧](https://dev.classmethod.jp/referencecat/aws-re-introduction-2024/)、[CloudFormation入門](https://dev.classmethod.jp/articles/sainyumon-cloudformation/)、[AWS CDKベストプラクティス](https://aws.amazon.com/jp/blogs/news/best-practices-for-developing-cloud-applications-with-aws-cdk)
- アプリケーション統合サービス:
  - **Amazon EventBridge**: イベント駆動型アーキテクチャを構築できるサーバーレスイベントバスサービス
  - **Amazon SNS**: フルマネージドなプッシュ型メッセージングサービス。サブスクライバー: HTTP/HTTPS, Email, SMS, SQS, Lambda, Kinesis Data Firehose, モバイルアプリ等。スタンダードトピック/FIFOトピック対応
  - **Amazon SQS**: フルマネージドなプル型メッセージキューイングサービス
- メトリクス監視: [CloudWatch Metrics監視の基本](https://zenn.dev/tatsuo48/articles/8f436c4a057961)、[パーセンタイル(公式)](https://docs.aws.amazon.com/ja_jp/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Percentiles)、[EC2インスタンスメトリクス](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html#ec2-cloudwatch-metrics)、[ALBメトリクス](https://docs.aws.amazon.com/ja_jp/elasticloadbalancing/latest/application/load-balancer-cloudwatch-metrics.html)、[ECS Container Insights](https://docs.aws.amazon.com/ja_jp/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-ECS.html)、[Auroraメトリクス](https://docs.aws.amazon.com/ja_jp/AmazonRDS/latest/AuroraUserGuide/Aurora.AuroraMonitoring.Metrics.html)
- サンプルコード: [AWS Samples(GitHub)](https://github.com/aws-samples)
- 資格: [約1ヶ月でAWS認定資格10個取得した学習法](https://dev.classmethod.jp/articles/aws-certifications-study-methods/)

## Auto Scaling
- AWS Auto Scalingは対象リソースをスケーリングし、コスト削減とパフォーマンス最適化を行うサービス(無料)
- 対象リソース: EC2 Auto Scalingグループ、ECSサービス、EC2スポットフリート、DynamoDB、Auroraレプリカ
- スケーリングプラン: タグ指定・EC2 Auto Scalingグループ選択・CloudFormationスタックから検索対象を選定
- スケーリング戦略: 可用性優先の最適化、コスト優先の最適化、可用性とコストのバランス、カスタム
- 類似サービスとの違い: **AWS Auto Scaling**は複数サービスを横断管理する上位サービス。個別のスケジュールベース/ステップスケーリングポリシーが必要な場合は**Amazon EC2 Auto Scaling**を直接使う
- 参考: [AWS再入門2022 Auto Scaling編](https://dev.classmethod.jp/articles/re-introduction-2022-aws-auto-scaling/)、[FAQ(AWS公式)](https://aws.amazon.com/jp/autoscaling/faqs/)

## Bedrock
- 生成AI基盤サービス。参考: [AWS入門ブログリレー2024 Bedrock編](https://dev.classmethod.jp/articles/introduction-2024-aws-bedrock/)、[Bedrock Knowledge bases編](https://dev.classmethod.jp/articles/introduction-2024-amazon-bedrock-knowledge-bases/)、[Bedrock Guardrails編](https://dev.classmethod.jp/articles/introduction-2024-amazon-bedrock-guardrails/)

## CloudFormation
- IaCサービス。参考(入門シリーズ、Qiita simonritchie氏): [#1 EC2とYAML復習編](https://qiita.com/simonritchie/items/330391e741f394897550)、[#2 セキュリティグループ編](https://qiita.com/simonritchie/items/a1922199a5b6d131dca9)、[#3 EC2とパラメータ編](https://qiita.com/simonritchie/items/8b1c3046474ca7c6863c)、[#4 組み込み関数編](https://qiita.com/simonritchie/items/5163abaf516902a55f30)、[#5 条件設定編](https://qiita.com/simonritchie/items/45f53b1f3b67303a751d)、[#6 出力とエクスポート編](https://qiita.com/simonritchie/items/2dc2b581f50a823861e9)

## Cognito
- ユーザー認証・認可基盤。1ユーザーに複数メール/パスワードは設定不可だが、複数SAML IdPの設定は可能
- 関連基礎知識: [OAuthの説明](https://qiita.com/TakahikoKawasaki/items/e37caf50776e00e733be)、[OpenID Connectの説明](https://qiita.com/TakahikoKawasaki/items/498ca08bbfcc341691fe)
- API: [Welcome(公式)](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/Welcome.html)、[AdminSetUserPassword](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_AdminSetUserPassword.html)、[GlobalSignOut](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_GlobalSignOut.html)、[ChangePassword](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_ChangePassword.html)、[ForgotPassword](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_ForgotPassword.html)、[ConfirmForgotPassword](https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_ConfirmForgotPassword.html)
- .NET SDK: [AmazonCognitoIdentityProviderClient](https://docs.aws.amazon.com/sdkfornet/v3/apidocs/items/CognitoIdentityProvider/TCognitoIdentityProviderClient.html)
- 参考記事: [AWS再入門2022 Cognito編](https://dev.classmethod.jp/articles/re-introduction-2022-amazon-cognito/)、[よくわかる認証と認可](https://dev.classmethod.jp/articles/authentication-and-authorization/)

## DocumentDB / DynamoDB
- DocumentDB: [AWS入門ブログリレー2024 DocumentDB編](https://dev.classmethod.jp/articles/introduction-2024-amazon-documentdb/)
- DynamoDB: [AWS入門ブログリレー2024 DynamoDB編](https://dev.classmethod.jp/articles/introduction-2024-amazon-dynamodb/)

## EC2 / ECS
- EC2: [AWS入門ブログリレー2024 EC2編](https://dev.classmethod.jp/articles/introduction-2024-amazon-ec2/)
- ECS: [AWS入門ブログリレー2024 ECS編](https://dev.classmethod.jp/articles/introduction-2024-amazon-ecs/)

## IAM
- [AWS入門ブログリレー2024 IAM編](https://dev.classmethod.jp/articles/introduction-2024-aws-iam/)、[IAM Identity Center編](https://dev.classmethod.jp/articles/introduction-2024-aws-iam-identity-center/)

## Kendra(全文検索)
- [AWS入門ブログリレー2024 Kendra編](https://dev.classmethod.jp/articles/introduction-2024-amazon-kendra/)
- [PowerPoint/Excel/Wordの全文検索を試す](https://dev.classmethod.jp/articles/full-text-search-of-powerpoint-excel-and-word-with-amazon-kendra/)
- SharePoint連携: [Kendraエディション(Developer/Enterprise)比較](https://dev.classmethod.jp/articles/kendra-edition/)、[SharePointデータソース実装](https://dev.classmethod.jp/articles/kendra-sharepoint-connector/)、[ユーザーアクセス権限に基づく検索](https://dev.classmethod.jp/articles/kendra-sharepoint-usercontextfilter/)

## RDS
- [RDS Blue/Greenデプロイ対応(データ無損失)](https://dev.classmethod.jp/articles/rds-bg-deploy/)
- ゼロETL: [Aurora×Redshiftゼロ ETL統合(プレビュー)](https://dev.classmethod.jp/articles/amazon-aurora-zero-etl-integration-with-amazon-redshift/) — サービス間統合によりETLなしで分析・機械学習を実現。Redshift/Athenaでフェデレートクエリが可能

## S3
- [AWS入門ブログリレー2024 S3編](https://dev.classmethod.jp/articles/introduction-2024-amazon-s3/)

## WAF
- [AWS入門ブログリレー2024 WAF編](https://dev.classmethod.jp/articles/introduction-2024-aws-waf/)

## Elastic Beanstalk
Java/.NET/PHP/Node.js/Python/Ruby/Go/DockerアプリをApache/Nginx/Passenger/IIS等使い慣れたサーバーでデプロイ・スケーリングするPaaSサービス。

- 特徴: 多様なデプロイ選択肢、統一UIでのモニタリング・管理、プラットフォーム自動更新、ELB+Auto Scalingによる自動スケール、スポット/EC2インスタンスタイプの最適選択
- 環境タイプ: ウェブサーバー環境／ワーカー環境
- 構成要素: **アプリケーション**(バージョン管理・アップロード管理)と**環境**(実際の稼働環境)
- 作成フロー: ①アプリケーション名/説明を入力し作成 → ②環境タイプ選択・環境名/ドメイン/説明入力 → ③プラットフォーム選択・アプリ選択・詳細設定(ソフトウェア/インスタンス/容量/ロードバランサー/デプロイ/セキュリティ/モニタリング/更新/通知/ネットワーク/データベース/タグの各項目)
- ローリング更新とデプロイ方式: 全部同時(All at once)／ローリング(Rolling)／追加バッチ付きローリング／変更不可(Immutable)／トラフィック分割(ALBのみ対応、NLB/CLB不可)。ユーザー影響とデプロイ速度のトレードオフで選定。参考: [デプロイポリシー解説](https://dev.classmethod.jp/articles/elastic-beanstalk-deploy-policy/)
- ブルーグリーンデプロイ: 「環境URLのスワップ」機能で実現(デプロイポリシーとは別機能)
- ヘルスレポート色分け: グレー(更新中)／グリーン(正常、最低1インスタンス稼働)／イエロー(一部ヘルスチェック失格、一部リクエスト失敗)／レッド(3つ以上失格またはリソース使用不可、リクエスト一貫して失敗)
- デプロイフロー: ①バージョンラベル入力・war/zipアップロード → ②バージョン選択・環境指定してデプロイ
- ツール: EB CLI(専用コマンドラインツール。AWS CLI/SDKも利用可)
- サンプル: [elastic-beanstalk-samples](https://github.com/awsdocs/elastic-beanstalk-samples), [aws-cognito-angular-quickstart](https://github.com/amazon-archives/aws-cognito-angular-quickstart), [go-beanstalk-gin](https://github.com/sudo-suhas/go-beanstalk-gin)
- 参考: [AWS再入門2022 Elastic Beanstalk編](https://dev.classmethod.jp/articles/2022_elasticbeanstalk_introduction/)

### Auto Scaling(Elastic Beanstalk関連補足)
- Auto Scalingグループ: 複数EC2インスタンスをグループ化し動的に増減管理
  - 起動設定/起動テンプレート: AMI・インスタンスタイプ・セキュリティグループ・ユーザーデータ等
  - 最小/最大/希望サイズ: グループが保持するインスタンス数の範囲と目標値
- スケーリングトリガー: スケールアウト(CPU利用率やネットワークトラフィックが閾値超過で新規インスタンス追加)／スケールイン(閾値未満でインスタンス削減)

---
*出典: docsリポジトリ(TakahitoSuzukiii/docs) pages/60_cloud/aws配下、2026-08-18時点の内容を再構成。アカウントID等の機密情報は元より含まれていません。*
