作成日: 2026-08-27 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-08-20〜2026-08-27

# 週次まとめ: メガテック企業・日系IT大手のシステム障害

## 🌐 メガテック系

### 1. Microsoft Teams「複数機能」の障害
- **発生日:** 2026年8月26日
- **対象サービス:** Microsoft Teams（マイクロソフトが提供するビジネスチャット・Web会議ツール）。会議の作成・参加、画面共有など複数機能に影響
- **原因:** メンテナンス関連作業が意図しない影響を与えたとMicrosoftが説明。作業停止後、標準的な可用性に戻ったと案内
- **影響範囲:** 日本を含むアジア太平洋地域のユーザーで、会議に接続しにくい・作成が進まない等の報告
- **復旧状況:** ほぼ収束（"largely mitigated"）と報道
- **出典:** https://cybersecuritynews.com/microsoft-teams-outage-multiple-features/ , https://funshitsu.com/status/

### 2. Microsoft 365 障害（8月24日）
- **発生日:** 2026年8月24日
- **対象サービス:** Microsoft 365（Outlook / Fabric / Viva / Defender 等を含む統合オフィスサービス群）
- **原因:** 現時点で詳細未確認。報道時点ではユーザーからのアクセス障害報告が中心
- **影響範囲:** 一部サービスへのアクセスに問題が発生したと利用者が報告
- **復旧状況:** 報道確認時点で継続調査中との情報あり。公式ポストモーテム（事後報告書）は本記事作成時点で未確認
- **出典:** https://tech.sportskeeda.com/laptops/news-is-microsoft-365-right-now-august-24-2026-outage-status-explored

### 3. Google Cloud 障害（AlloyDB / IAM等、複数サービス）
- **発生日:** 2026年8月20日 08:40〜12:20（米国太平洋時間）
- **対象サービス:** Google Cloud の AlloyDB for PostgreSQL（マネージド型データベースサービス）、Identity and Access Management（IAM、権限管理機能）、Managed Service for Apache Kafka、Persistent Disk（永続ディスク）等、複数コンポーネントに影響
- **原因:** 本記事作成時点で公式インシデントページ上の詳細な根本原因は未確認
- **影響範囲:** 上記サービスを利用する一部プロジェクトに影響（対象期間の起点にあたる8/20発生のため、規模・利用者数の全体像は限定的にしか確認できず）
- **復旧状況:** 同日中に復旧（12:20 PT終了）
- **出典:** https://status.cloud.google.com/incidents/utF3FMFdQfwBzJcGG6vf

### 参考: GitHub障害（8月17日発生、対象期間外）
- 2026年8月17日に約7時間47分にわたる大規模障害（github.com、ログイン、Actions、API、Pull Request、Issues、Copilotに影響）が報じられていますが、発生日が本記事の対象期間（8/20〜8/27）より前のため、詳細掲載は見送ります。関心があれば https://statusgator.com/blog/github-outage-on-august-17-2026-seven-hours-of-unicorn-errors-and-copilot-failures/ をご確認ください。

## 🇯🇵 日系企業系

今週（2026年8月20日〜27日）については、通信キャリア（NTTドコモ・au・ソフトバンク）や大手銀行（みずほ・三菱UFJ等）で対象期間内に発生したと確認できる新規の重大障害情報は、検索範囲内では見つかりませんでした。

決済関連では、収納代行サービス「ウィズ」が2026年8月25日にコンビニ支払・インターネットバンキング支払で利用できない障害を報告し、同日17時時点で一部利用可能に回復したとの情報がありましたが、詳細な原因・完全復旧時刻等の一次情報までは裏取りできませんでした（出典: https://www.wise-pds.jp/news/2026/news2026082501.htm ）。参考情報として付記します。

## 所感

今週はメガテック側でMicrosoft関連（Teams・365）の障害が2件続けて報じられており、いずれもメンテナンス作業に起因する短時間の機能低下という共通点が見られました。Google Cloudも対象期間の起点で複数コンポーネントにまたがるインシデントが発生しており、大手クラウド事業者では「メンテナンス由来の一時的な機能低下」が繰り返し発生している印象です。日系企業側は大規模な通信・金融障害の新規報道は確認されず、決済代行の一部障害が目立った程度で、前週に続き比較的落ち着いた週でした。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
