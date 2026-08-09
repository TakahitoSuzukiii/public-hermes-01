作成日: 2026-08-09 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）

今週は「コスト・棚卸し系の運用自動化」「セキュリティ/脆弱性管理の自動化（Security Hub・Inspector）」「IaC（Infrastructure as Code、インフラをコードで管理する手法）とCI/CD（継続的インテグレーション/継続的デリバリー）」「Well-Architected（AWS推奨のベストプラクティス集）」の4テーマで、実務者のブログやAWS公式情報を中心に収集しました。個別サイトの全文転載はせず、要点をOptimus自身の言葉で要約しています。

---

## 1. ITインフラ/サーバ運用保守の自動化（コスト・棚卸しレポート）

### AWS Budgetsだけでは足りない？Cost Explorer API + Lambdaでコスト監視を自動化
- 出典: Qiita（shoyua氏） https://qiita.com/shoyua/items/9b8c3f864cb1bbdb2359
- 要約: AWS Budgets（予算超過をメールなどで通知する標準機能）だけではサービス別・タグ別の詳細な内訳が見えづらいという課題に対し、Cost Explorer API（利用料金データをプログラムから取得できるAPI）とLambda（サーバー管理不要でコードを実行できる仕組み）を組み合わせ、任意の粒度でコストレポートを自動生成する方法を紹介。定期実行と組み合わせれば、毎朝のコストサマリー通知のような運用が組めます。

### EventBridge・Lambda・Cost Explorer APIでAWSコストレポートを自動化
- 出典: AWS Builder Center（Automate AWS Cost report） https://builder.aws.com/content/2dKeNrWeMj8E1Yh6CXITS7Hg0cU/automate-aws-cost-report-using-eventbridge-lambda-cost-explorer-api
- 要約: EventBridge（時刻やイベントをトリガーに処理を起動するスケジューラ/イベントバス）でLambdaを定期起動し、Cost Explorer APIから取得したコストデータをレポート化して配信する構成をAWS公式ビルダーコミュニティが解説。前述のQiita記事と組み合わせると、コストレポート自動化の「型」がつかみやすい内容です。

### 新規作成したAWSリソースへの自動タグ付け処理（棚卸し自動化）
- 出典: スカイ365ブログ https://sky365.co.jp/blog/aws-resource-auto-tagging/
- 要約: リソース作成をトリガーにLambda（Boto3というPython用AWS操作ライブラリを使用）が起動し、所有者やコスト按分用のタグを自動付与する仕組みを紹介。タグ付けが徹底されるとコスト按分レポートやリソース棚卸しの精度が上がるため、コスト自動化と組み合わせて導入する価値がある内容です。

---

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### Security Hub CSPMから何が変わった？新しいSecurity Hubの全体像
- 出典: Zenn（cscloud_blog） https://zenn.dev/cscloud_blog/articles/securityhub-v2-overview
- 要約: Security Hub（複数のセキュリティサービスの検出結果を一元管理するAWSサービス）がCSPM（Cloud Security Posture Management、クラウド環境の設定不備を継続的に検出する仕組み）として刷新された点を整理。GuardDuty（不審な通信や不正アクセスの兆候を検知するサービス）、AWS Config（リソース設定の変更履歴を記録するサービス）、Inspector（OSやアプリの脆弱性を自動スキャンするサービス）の検出結果を統合的に見られるようになった経緯がわかります。

### 大幅に進化したAWS Security Hub(Advanced)の紹介
- 出典: TechHarmonyブログ（usize-tech） https://blog.usize-tech.com/aws-securityhub-advanced/
- 要約: 2025年のAWS re:Inforce（AWSのセキュリティ専門イベント）で発表された強化版Security Hubについて解説。Inspectorの脆弱性検出結果を含む複数シグナルを組み合わせたリスクの可視化が強化され、優先度付けの自動化が進んでいる点がポイントです。

### Amazon Inspector + EventBridgeでSBOM自動出力
- 出典: iret.media（クラスメソッド系メディア） https://iret.media/151685
- 要約: Inspectorが生成するSBOM（Software Bill of Materials、ソフトウェアの構成部品一覧）をEventBridge経由で自動的にS3へ出力する構成を紹介。S3・KMS（鍵管理サービス）への最小権限ポリシー設計も示されており、脆弱性管理の証跡保存を自動化したい場合の実装例として参考になります。

---

## 3. IaC・CI/CD・Lambda/EventBridge/Systems Managerによる運用自動化・SRE

### AWS CDKでEventBridge Scheduler利用時のIAMワイルドカード問題を解決
- 出典: DevelopersIO（クラスメソッド） https://dev.classmethod.jp/articles/aws-cdk-eventbridge-scheduler-target-universal-iam-control/
- 要約: CDK（AWS Cloud Development Kit、プログラミング言語でインフラを定義するIaCツール）でEventBridge SchedulerのUniversal Targetを使うと、IAM（権限管理サービス）ポリシーに意図しないワイルドカード（*）権限が自動付与される問題への対処法を解説。最小権限運用を徹底したいセキュリティ意識の高いチーム向けの実践的な内容です。

### Amazon EventBridgeスケジューラ用AWS CDKコンストラクトライブラリが一般提供開始
- 出典: AWS公式 What's New https://aws.amazon.com/jp/about-aws/whats-new/2025/04/aws-cdk-construct-library-eventbridge-scheduler/
- 要約: EventBridge Scheduler専用のCDKコンストラクト（再利用可能な設定部品）が正式リリースされたとのAWS公式アナウンス。従来より少ないコード量で定期実行ジョブの構築が可能になり、運用自動化のコードをシンプルに保てます。

### TerraformでAWSリソースを更新する際のCI/CDをGitHub Actionsで構築
- 出典: DevelopersIO（クラスメソウド） https://dev.classmethod.jp/articles/terraform-aws-ci-cd-github-actions/
- 要約: これまでWebコンソールで手作業設定していたAWS環境をTerraform（HashiCorp社のIaCツール）でコード化し、GitHub Actions（GitHub純正のCI/CDサービス）でplan/applyを自動実行するパイプラインの構築事例。手作業運用からIaC化への移行ステップが具体的に書かれており、着手のハードルが下がる内容です。

### Systems Manager Automationによるパッチ適用の自動化（DOP-C02試験範囲の整理）
- 出典: ExamRoll https://examroll.com/ja/posts/dop-c02-ssm-automation/
- 要約: AWS認定試験の学習記事ですが、Systems Manager（サーバーの管理・自動化を行うAWSサービス）のAutomationドキュメント（AWS-RunPatchBaseline）を使い、パッチのスキャンと適用を自動化する仕組みが簡潔に整理されています。運用保守の自動化を体系的に理解したい場合の入門資料として有用です。

---

## 4. ベストプラクティス（Well-Architected等）

### AWSベストプラクティス実践ガイド｜Well-Architected 6つの柱と導入方法
- 出典: cloudpackコラム https://cloudpack.jp/column/operations/aws-well-architected-best-practices.html
- 要約: Well-Architected Framework（AWSが提唱する設計・運用の指針）の6つの柱（運用上の優秀性、セキュリティ、信頼性、パフォーマンス効率、コスト最適化、持続可能性）について、それぞれの具体的な実践方法を解説。特に「運用上の優秀性」の柱では、運用手順の文書化・変更管理プロセスの確立・インシデント対応フローの整備が自動化の土台として強調されています。

---

## 今後のウォッチポイント
- Security Hub Advanced／新Security Hub CSPMは今後も機能拡張が続く見込みのため、次回以降も継続的に追跡予定。
- EventBridge Scheduler用CDKコンストラクトはリリース初期のため、実運用でのハマりどころ（IAM権限周り等）の情報が今後増えると予想されます。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
