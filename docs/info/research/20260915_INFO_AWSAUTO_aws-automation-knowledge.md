作成日: 2026-09-15 / STATUS: INFO / TOPIC: AWSAUTO

# AWSによる業務自動化ナレッジ（週次まとめ）2026-09-15

今週はAWS（Amazon Web Services、Amazonが提供するクラウドサービス群）の運用自動化ナレッジの中から、**Systems Managerによる定型運用の自動化**、**GuardDuty（脅威検知サービス）のLambda保護新機能**、**生成AIエージェントによるマルチエージェントSRE（Site Reliability Engineering）支援**、**組織全体のCloudTrail監査基盤とガバナンスドリフト検知**という4テーマを中心に、前週（9/8）・前々週（9/1）と重複しないサービス・切り口を厳選しました。

---

## 1. ITインフラ/サーバ運用保守の自動化（レポート・コスト・棚卸し生成）

### AWS Systems Manager運用自動化ガイド：パッチ・リモート接続・インベントリを一元化
SES BASEの実践解説記事では、AWS Systems Manager（サーバー運用管理を自動化するサービス）が持つ4つの機能――Session Manager（SSHレス・踏み台サーバー不要のリモート接続機能）、Patch Manager（OS・アプリのパッチ適用自動化機能）、Run Command（複数サーバーへの一括コマンド実行機能）、Parameter Store（設定値・シークレットの一元管理機能）――を組み合わせた現場向けの運用自動化フローを整理しています。個別サービスとしては目新しくありませんが、「SSH鍵管理をなくし、パッチ適用・インベントリ管理・設定配布までSystems Manager単体で完結させる」という統合運用の設計思想がまとまっている点が実務的です。
出典: https://ses-base.com/articles/aws-systems-manager-operations-guide/

### Amazon QuickがExcel・PowerPoint向けMicrosoft 365拡張機能を追加
AWS公式の発表（2026年4月30日）によると、生成AIを活用したワークフロー機能「Amazon Quick」が、Excel・PowerPoint・Word向けのMicrosoft 365拡張機能（プレビュー）を新たに公開しました。ユーザーが普段使うOffice環境の中から直接AWSのデータやワークフローを呼び出せるようになり、これまでLambdaやAPIで自作していた「コストレポートのPPT化」「棚卸し結果のExcel出力」といった定型レポート生成作業を、Office拡張機能経由でより簡単に実現できる可能性がある機能追加です。
出典: https://aws.amazon.com/jp/about-aws/whats-new/2026/04/amazon-quick-microsoft-excel/

### Cost Explorer API + Lambdaで「Budgetsだけでは足りない」コストレポートを自動化
Qiitaの実装記事では、AWS Budgets（予算超過アラート機能）だけではカバーしきれない、部署別・サービス別など粒度の細かいコストレポートを、Cost Explorer（コスト分析サービス）のAPIとLambdaを組み合わせて自動生成する手順を紹介しています。マネージドコンソールの標準機能では対応しきれない「独自の切り口でのコスト可視化」を、最小構成（Lambda単体）で実現する実践例として参考になります。
出典: https://qiita.com/shoyua/items/9b8c3f864cb1bbdb2359

---

## 2. セキュリティ/ゼロデイ対策・脆弱性管理の自動化

### GuardDutyがLambda関数の不審なネットワークアクティビティを検知する新機能に対応
クラスメソッドの記事とAWS公式ドキュメントによると、Amazon GuardDuty（脅威検知サービス）が新たに「Lambda Protection」機能に対応し、Lambda関数が呼び出された際の不審な通信（悪意あるIPへの通信等）を自動検知できるようになりました。これまでEC2やS3が中心だったGuardDutyの監視範囲がサーバーレス領域まで拡張されたことで、Lambda中心のサーバーレス構成でも「常時監視→自動アラート」の脅威検知パイプラインを追加コード無しで組み込めるようになります。
出典: https://dev.classmethod.jp/articles/update_guardduty_lambda_protection/ ／ 公式: https://docs.aws.amazon.com/ja_jp/guardduty/latest/ug/lambda-protection.html

### GuardDuty追加プロテクション機能の導入メリットとコスト最適化戦略
TerraSkyの技術記事では、GuardDutyの各種追加プロテクション機能（EKS Protection、RDS Protection、Malware Protectionなど）を導入する際の運用自動化のポイントと、検知範囲を広げるほど増加しがちなコストを最適化する戦略を整理しています。「機能を全部有効化する」のではなく、リソース構成に応じて必要な保護機能を選定し、EventBridge経由の自動対応と組み合わせて費用対効果を高める考え方が実務的です。
出典: https://www.terrasky-tech.co.jp/post/20260626-amazonguardduty

---

## 3. IaC・CI/CD・Lambda/EventBridge/Systems Managerによる運用自動化・SRE

### Amazon Bedrock AgentCoreでマルチエージェントSREアシスタントを構築
AWS公式の機械学習ブログ（2026年7月10日）では、Amazon Bedrock AgentCore（AIエージェントの実行基盤）とLangGraph（エージェント連携フレームワーク）、MCP（Model Context Protocol、AIとツールを接続する標準プロトコル）を組み合わせ、専門分野ごとに役割分担された複数のAIエージェントが協調して障害対応にあたる「マルチエージェントSREアシスタント」の構築方法を解説しています。単一のAIが全ての判断をする従来型のチャットボットではなく、「調査担当」「原因分析担当」など役割別エージェントを連携させることで、複雑なインシデント対応をより深く支援できる設計が特徴です。
出典: https://aws.amazon.com/blogs/machine-learning/build-multi-agent-site-reliability-engineering-assistants-with-amazon-bedrock-agentcore/

### Strands Agents + Amazon BedrockでMicrosoft製agent-sreを運用
クラスメソッドの記事では、AWSが開発した軽量AIエージェントフレームワーク「Strands Agents」とAmazon Bedrockを組み合わせて構築したAIエージェントを、Microsoft製のSRE運用フレームワーク「agent-sre」を使い、SLO（サービスレベル目標）監視・サーキットブレーカー（異常時の自動遮断機構）・コストガードといった運用ルールの下で動かす検証を紹介しています。AWSネイティブなエージェント基盤と、ベンダー横断のSRE運用フレームワークを組み合わせる実装例として、マルチクラウド前提の運用設計の参考になります。
出典: https://dev.classmethod.jp/articles/strands-bedrock-agent-sre/

---

## 4. ベストプラクティス（Well-Architected等）・ガバナンス

### AWS Organizationsで全社CloudTrail監査基盤を構築する2026年版ガイド
個人エンジニアによる技術ブログでは、AWS Organizations（複数AWSアカウントを一元管理するサービス）配下の全アカウントに対し、組織トレイル（Organization Trail）でCloudTrail（API操作の証跡ログ）を自動適用し、委任管理者（Delegated Administrator）による監査チーム運用、専用のログアーカイブアカウントへの集約、SCP（Service Control Policy、証跡ログの無効化を防ぐ抑止ポリシー）、Control Tower連携までを実コードとともに体系的に解説しています。個々のアカウントで証跡設定を手作業管理する運用から脱却し、「新規アカウントを作れば自動的に監査対象になる」ガバナンス基盤の設計として実務価値が高い内容です。
出典: https://tomodahinata.com/blog/aws-cloudtrail-organization-trail-multi-account-audit-guide

### AWS Control Towerのガバナンスドリフトを体系的に理解する
AWS公式ドキュメントでは、Control Tower（複数アカウント環境のガバナンスを自動適用するサービス）管理下で発生しうる「ガバナンスドリフト」――メンバーアカウントの移動・削除、SCPの予定外の変更、組織単位（OU）の変更など――の種類と検知方法が整理されています。手動でのコンソール操作による意図しない構成変更を継続的に検知し、ガバナンス基盤自体の健全性を保つための公式リファレンスとして、監査自動化の設計時に参照する価値があります。
出典: https://docs.aws.amazon.com/ja_jp/controltower/latest/userguide/governance-drift.html

---

## 5. コミュニティ知見（GitHub）

### awesome-devops：DevOps全般を俯瞰できるcuratedリスト
`wmariuss/awesome-devops`は、AWSを含むクラウドサービス、CI/CDツール、構成管理、コンテナオーケストレーション、監視・ログ管理、シークレット管理まで、DevOps（開発と運用を統合する文化・手法）関連ツールを幅広く網羅したcuratedリスト（厳選リンク集）です。AWS特化のawesome-awsとは異なり、AWSサービスを他のDevOpsツールチェーンの中でどう位置づけて組み合わせるかを俯瞰する際の参照先として有用です。
出典: https://github.com/wmariuss/awesome-devops

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
