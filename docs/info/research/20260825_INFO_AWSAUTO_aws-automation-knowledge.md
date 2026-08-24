作成日: 2026-08-25 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ 週次まとめ（2026-08-25）

今週は「Lambdaによるリソース棚卸しExcelレポート自動生成」「Security Hub自動化ルール（新機能）による検出結果の自動振り分け」「AWS Config適合パック（Conformance Pack）による準拠状態の自動修復」「GuardDutyマルチアカウント脅威検知とEventBridge連携」「Systems Manager Automationランブックによる定型作業の自動化」「AWS CDKでのEventBridge×Lambdaバッチ構築」「コミュニティ知見（awesome-aws）」の7テーマを中心に収集しました。前週（2026-08-18）はCost Explorer APIでのコスト通知やInspector SBOM、StackSetsを扱ったため、今週はSecurity Hubの新しい自動化ルール機能やConfig適合パック、CDKでのバッチ構築など、別のサービス・切り口を優先しています。

## 1. ITインフラ/サーバ運用保守の自動化（レポート・棚卸し生成）

### Lambda + boto3でAWSリソース情報を一括収集しExcel出力
AWS環境を運用していると、リソースの棚卸しや構成管理のために定期的にAWSリソース情報を集めたい場面があります。Lambda（サーバー管理不要でコードを実行できるサービス）関数からboto3（AWSをPythonで操作するためのSDK＝ソフトウェア開発キット）を使ってEC2やS3などのリソース情報を収集し、openpyxl（PythonでExcelファイルを操作するライブラリ）でExcelファイルとして出力する手順が紹介されています。手作業でのマネジメントコンソール確認を、定期実行のバッチ処理に置き換える典型的な自動化パターンです。
出典: https://persol-serverworks.co.jp/blog/lambda/lambdaaws-lambda.html

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### AWS Security Hub 新自動化ルールで検出結果を大規模に振り分け
2026年1月に一般提供が始まった新しいAWS Security Hub（複数のセキュリティサービスの検出結果を集約するサービス）では、検出結果（Finding）を条件に基づいて自動的にフィルタリング・優先度付け・担当チームへのルーティングを行う「自動化ルール」機能が強化されました。重大な検出結果を確実に適切なチームへ迅速に届け、手作業での仕分けや対応時間を減らしつつ、一貫した修復プロセスを維持できる点が特徴です。複数アカウント・複数リージョンにまたがるセキュリティ運用の負荷軽減に直結する機能です。
出典: https://aws.amazon.com/blogs/security/streamline-security-response-at-scale-with-aws-security-hub-automation/

### GuardDutyのマルチアカウント脅威検知とEventBridgeによる自動対応
Amazon GuardDuty（脅威検知サービス）をAWS Organizations（複数アカウントを一元管理する仕組み）と連携させ、委任管理者アカウントから全アカウントの検出結果を集約する構成と、EventBridge（イベント駆動でサービス間を連携させる仕組み）を使って検出結果に応じたカスタム自動対応（例: 疑わしいインスタンスの隔離、通知）を組み立てる手順が整理されています。新規アカウントを自動的に監視対象へ組み込む設定も含まれ、組織全体のセキュリティ自動化基盤として参考になります。
出典: https://tomodahinata.com/blog/aws-guardduty-threat-detection-multi-account-terraform-eventbridge-guide

### AWS Config適合パック（Conformance Pack）による準拠状態の自動修復
AWS Config（リソースの構成変更を記録・評価するサービス）の適合パックは、複数のConfigルールと自動修復アクションをテンプレート化してまとめて展開できる仕組みです。CloudFormation（AWSリソースをコードで定義・展開する仕組み）テンプレートでS3バケットの暗号化ルールなどを定義し、非準拠と評価されたリソースをSSM Automation（後述）やLambdaで自動修復する構成が解説されています。組織のセキュリティ基準を「決めたら終わり」ではなく「守られ続ける状態」に保つための自動化として実務的です。
出典: https://blog.serverworks.co.jp/config/conformance-pack

## 3. IaC・CI/CD・Lambda/EventBridge/Systems Managerによる運用自動化・SRE

### AWS CDKでEventBridge×Lambdaのバッチ処理を構築
AWS CDK（Cloud Development Kit、プログラミング言語でIaC＝Infrastructure as Codeを記述できるツール）を使い、EventBridgeのスケジュールルールとLambda関数を組み合わせて定期バッチ処理を構築する手順がTypeScriptのコード例とともに紹介されています。CloudFormationテンプレートを直接書く場合に比べ、型チェックや再利用可能なコンストラクト（部品化された構成要素）でIaCの保守性を高められる点がポイントです。
出典: https://dev.classmethod.jp/articles/cdk-event-bridge-lambda-batch/

### Systems Manager Automationランブックによる開閉局（起動・停止）自動化
AWS Systems Manager（サーバー群を一元管理するサービス）のAutomation機能を使い、独自のランブック（自動化手順書）を定義してサーバーの「開局（起動）」「閉局（停止）」処理を自動化した実装例が紹介されています。事前定義された標準ランブックだけでなく、自社の運用フローに合わせて複数ステップのワークフローを自作できる点が、定型的な運用作業の標準化・自動化に役立ちます。
出典: https://qiita.com/tyskJ/items/f5e2335ff6912a375c89

## 4. ベストプラクティス（Well-Architected等）

### AWS Well-Architected Framework「運用上の優秀性」の観点から自動化を評価する
AWS Well-Architected Framework（信頼性・セキュリティ・コストなど複数の観点でクラウド設計を評価する公式フレームワーク）の6つの柱のひとつである「運用上の優秀性（Operational Excellence）」は、変更管理やインシデント対応の自動化、手順書（ランブック・プレイブック）の整備を重視しています。今週紹介したSecurity Hub自動化ルールやConfig適合パック、SSM Automationランブックといった個別施策は、いずれもこの柱が掲げる「反復可能な手順を自動化し、人的ミスと対応時間を減らす」考え方に沿ったものです。単発ツールの導入で終わらせず、この観点に立ち返って自社の運用自動化の抜け漏れを点検することが推奨されます。
出典: https://docs.aws.amazon.com/wellarchitected/latest/framework/operational-excellence.html

## 5. コミュニティ知見（awesome-aws等）

### awesome-aws（AWS関連の定番キュレーションリスト）
`donnemartin/awesome-aws`は、AWSのライブラリ、OSS（オープンソースソフトウェア）リポジトリ、ガイド、ブログなどを体系的にまとめた定番のキュレーションリストです。多数のフォークが存在するほど広く参照されており、自動化ツールやIaC関連リポジトリを横断的に探す起点として有用です。
出典: https://github.com/donnemartin/awesome-aws

## 今後のウォッチポイント

- Security Hub新自動化ルールが、複数アカウント環境での実運用（誤検知の抑制やSLA順守）にどこまで効果を発揮するか。
- Config適合パックによる自動修復と、SSM Automationランブックとの連携パターンがどこまで標準化されていくか。
- CDKベースのEventBridge×Lambdaバッチ構築が、今後CloudFormation直書きに代わる主流パターンとして定着するか継続観察。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
