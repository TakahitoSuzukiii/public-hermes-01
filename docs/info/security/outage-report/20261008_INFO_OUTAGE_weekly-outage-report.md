作成日: 2026-10-08 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-10-01〜2026-10-08

# 週次まとめ：メガテック企業・日系IT大手のシステム障害

※出典は各記事の要約です(自分の言葉で整理)。一部は二次情報(監視サイト等)で、原因が未確定のものはその旨を明記しています。

## 🌐 メガテック系

### 1. Microsoft Azure 広域ネットワーク障害(9/30 20:30 UTC〜10/1 02:15 UTC)
- 対象: ExpressRoute(企業の専用線接続)、VPN Gateway、Azure Firewall、Application Gateway、Azure VMware Solution 等。日本西を含む約18〜19リージョン。
- 原因: Microsoft公式によると、リージョンのゲートウェイ管理サービスへの変更と、OS更新作業(メンテナンス)が重なり負荷が急増、自動スケールが追いつかなかったため。変更を元に戻して復旧。
- 影響: 接続の劣化・断、管理操作の失敗や遅延。
- 復旧: 10/1 02:15 UTCに緩和を確認。再発防止策は調査中。
- 出典: https://azure.status.microsoft/en-us/status/history/?trackingId=7Q30-010 / https://finance.biggo.com/news/d9307983-5b75-4692-bb05-adbebd020274

### 2. AWS スペイン(EU-SOUTH-2)の単一AZでパケットロス(10/4〜10/6報道)
- 対象: EC2、RDS、S3、DynamoDB、ELB等、同一AZ(Availability Zone=データセンターの区画)に依存する多数サービス。
- 原因: ネットワーク基盤の障害と報じられているが、AWS側の根本原因の公式発表は未確認(報道間で時刻や詳細に食い違いあり)。
- 影響: API遅延・エラー、接続のタイムアウト。1つのAZに限定。
- 復旧: 数時間で改善と報道(正確な復旧時刻は報道により異なる)。
- 出典: https://uptimerobot.com/is-it-down/aws-amazon-web-services/2026-10-04/ / https://uxc.news/p/aws-reports-two-hour-packet-loss-outage-in-spain-s-eu-south-2-availability-zone

### 3. Cloudflare 複数の軽微〜中規模障害(10/1〜10/6)
- 10/1: Durable Objects/R2のエラー増(約20分)。
- 10/5: キャッシュ配信の遅延、API ShieldのJWT検証エラー(対称鍵構成、約11時間)、北米東部のDurable Objects可用性低下(約5時間)。
- 10/6: 一部Keyless SSL(RSA鍵)でTLSハンドシェイク失敗(約40分)。
- 原因: 多くは未公表。いずれも復旧済み。全面停止ではなく機能・地域限定。
- 出典: https://uptimerobot.com/is-it-down/cloudflare/2026-10-05/ / https://www.isinternetup.com/outages

### 4. Microsoft 365 / Teams の継続的な不具合(10/6時点)
- Teamsの連絡先・Speed Dialが空白になる問題(原因特定、修正を検証中)、Citrix VDI上のTeams最適化が切れる問題、PowerPoint Live録画の欠落(復旧済み)。
- 全面障害ではなく機能限定。
- 出典: https://www.chasms.com/blog/daily-outage-brief-2026-10-06-evening/

### 補足(参考)
- AWSの中東データセンターが3月の攻撃で損傷し、データを復旧できないと9月に公表された件が10/4〜10/7にも報じられています(新規障害ではなく既報の続報のため件数に含めず)。 https://ettayeb.fr/en/cloud/aws-middle-east-data-loss-2026/
- Google Cloud: 今週は公式の障害報告なし(最終は9/1)。Meta: 10/7に利用者報告はあるが、公式確認はされておらず詳細不明。

## 🇯🇵 日系企業系

### 1. IDCフロンティア(IDCF Cloud)障害による国内Web多数停止(10/7 3:40頃〜継続)
- 対象: IDCF Cloud上のサイト・サービス。茨城県・小平市などの自治体、Jリーグクラブ、eラーニング「LearnO」、機械翻訳サービス等。
- 原因: 利用企業(クロスランゲージ)の発表では、データセンターが第三者による不正アクセスを受けたことに起因するとされ、被害拡大防止のためネットワーク遮断と対象エリアの全マシン停止を実施。ただし他の自治体・企業の原因が同一かはITmedia記事時点で不明。
- 影響: 多数のWebサイトが閲覧不能。
- 復旧: 見通し立たず(10/7夜時点)。
- 出典: https://www.itmedia.co.jp/news/article/2610/07/2000002085/ / https://www.crosslanguage.co.jp/news/networkoutage20261007/ / https://learno.jp/newslist/15569

### 2. 大阪公立大学 大規模システム障害(10/2未明〜)
- 対象: 情報基盤システム全般(メール含む)。
- 原因: 同大は10/5の会見でランサムウェア(身代金要求型マルウェア)攻撃によるものと説明。
- 影響: 報道によると約500台のサーバが停止、バックアップの多くも暗号化。約13万人分の個人情報の流出有無を調査中。10/8まで全学部で授業休講。
- 復旧: 継続中。
- 出典: https://www.sbbit.jp/article/cont1/187311 / https://www.fnn.jp/articles/-/1126928 / https://piyolog.hatenadiary.jp/entry/2026/10/07/095650

### 3. イオン系決済(イオンカード・AEON Pay・WAON)障害(10/1 4:25〜9:44)
- 一部店舗で上記決済が利用不可。原因は未確認。復旧済み。
- 出典: https://funshitsu.com/status/

### 4. 国保オンライン請求システム ログイン不具合(〜10/6復旧)
- ログインできない問題が10/5夜の改修後、10/6から正常化。請求期間は国保分のみ10/13 21時まで延長。原因詳細は未確認。
- 出典: https://funshitsu.com/status/

※通信キャリア(ドコモ/au/ソフトバンク)・メガバンクの大規模障害は、今回の検索範囲では確認できませんでした。

## 所感
- クラウド事業者自身の変更・メンテナンスが障害の引き金になる例(Azure)が目立ち、単一AZ障害(AWS)も含め「冗長化の設計」が改めて重要です。
- 国内ではIDCFの障害が自治体など多数のサイトに波及し、委託先1社の障害が広範囲に影響する典型例でした。ランサムウェア被害(大阪公立大)と合わせ、サイバー攻撃起因の停止が増えています。
- 本週は検索回数の制約(12回)のため、網羅性には限りがあります。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
