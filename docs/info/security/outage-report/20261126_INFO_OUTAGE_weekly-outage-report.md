作成日: 2026-11-26 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-11-19 〜 2026-11-26

# 週次システム障害まとめ(2026-11-19 〜 11-26)

※ 本記事は公開情報の要約です。時刻は特記なき限り日本時間(JST)。UTC は協定世界時(JST の9時間前)。

## 🌐 メガテック系

### 1. Cloudflare 複数の軽微な障害(11/18〜11/24)
Cloudflare(クラウドフレア)は CDN(Content Delivery Network、世界中に置いたサーバでWebを高速配信する仕組み)や DNS などを提供する企業です。今週は大規模停止ではなく、公式が「軽微(Minor)」とする障害が続きました。
- **11/18〜19 欧州〜アジア太平洋間の接続劣化**: Cache Reserve・D1・R2 等でエラー/遅延。約4時間53分で復旧。
- **11/19 Cloudflare Access の認証失敗(06:48〜08:56 UTC)**: 新しいリリースがサービストークン(JWT: 認証情報を載せた署名付きデータ)から `sub` 項目を消してしまい、厳密に検証するアプリで認証エラー。変更を取り消して世界展開し復旧(約2時間8分)。
- **11/19 Durable Objects / D1 のエラー増加(13:05〜13:37 UTC)**: 一部顧客でストレージ操作の失敗・遅延。約32分で復旧。
- **11/19 Observability の取り込み遅延・クエリ失敗(16:30〜21:55 UTC)**: 監視ログ/トレース機能のみの障害で、Workers 本体の実行停止ではない。原因の詳細は未公表。
- **11/24 フランスのEmail Routing 問題(13:38〜22:42 UTC)**: 地域限定の問題。
- 影響範囲: いずれも一部機能・一部顧客。
- 出典: https://www.cloudflarestatus.com/incidents/5pe5mb9fefi8 / https://cyberattack.ai/outages/cloudflare / https://www.host-tracker.com/en/is-cloudflare-down/incidents/2026-11-24-1338

### 2. 【続報】Microsoft 365 大規模障害(11/12〜13発生)の事後情報
先週の記事で取り上げた障害の続報です(新規障害ではありません)。
- Reuters(11/24付)によると、Microsoft は社内で「Code Red(最優先の緊急対応)」を宣言し、障害防止・復旧体制の見直しに着手。原因として7月に混入した Windows のスケーラビリティ(負荷増への耐性)不具合を挙げ、サイバー攻撃ではないとしている。今後は障害時に世界全体で1時間以内の解決を目標にするとのこと。
- 出典: https://www.investing.com/news/stock-market-news/exclusivemicrosoft-declares-code-red-after-historic-outage-internal-memos-show-5048702 / https://www.cnbc.com/2026/11/12/microsoft-outage-outlook-aws-google.html

### 参考
- Azure のステータスページに 11/25 時点で「複数の問題を検知」との表示がありましたが、詳細・影響範囲は今回の調査では確認できていません(未確認のため記事化せず)。
- AWS・Google Cloud(Workspace)・Meta・Apple は、今週新たに大きな障害の報道は確認できませんでした(AWS US-EAST-1 の 11/13・11/15 分は先週以前に該当)。

## 🇯🇵 日系企業系

### 1. 大雪・停電による携帯4社の通信障害(福島・長野・岐阜)
- **発生**: 11/20 夕方〜21日朝から(会社により開始時刻が異なる)。
- **対象**: NTTドコモ、au(KDDI)、ソフトバンク(ワイモバイル・LINEMO含む)、楽天モバイル、および各回線を使うMVNO(格安SIM)。ソフトバンクは Air・おうちのでんわにも影響。
- **原因**: 大雪・悪天候による停電と、基地局までの光回線(伝送路)の故障・断線。
- **影響**: 福島県・長野県・岐阜県の山間部の一部地域で通話・通信が不可または不安定。緊急通報も使いづらい状況があった。
- **対応**: 4社が JAPANローミング(災害時に他社回線を借りる仕組み、最大300kbps)を提供。発電機・臨時衛星回線で対応。
- **復旧**: 福島・長野は11/24までに復旧。ソフトバンクは岐阜も含め 11/25 16:43 に全面復旧を発表。他社の最終復旧状況は今回未確認。
- **出典**: https://www.softbank.jp/mobile/info/personal/important/20261121-01/ / https://topics.smt.docomo.ne.jp/article/itmedia_mobile/trend/itmedia_mobile-20261124_051 / https://chotto.news/mobile-outage-fukushima-nagano-gifu/

### 2. PayPay クレジット連携決済の障害(進行中)
- **発生**: 11/25 20:05頃〜(26日未明時点で復旧時刻は未公表)。
- **対象**: PayPayクレジット払い・同クレジットからのチャージ・三井住友カード払い・他社カード利用券購入。Yahoo!ショッピング等への波及報道もあり(二次情報)。
- **原因**: 調査中。PayPay は「サイバー攻撃や不正アクセスは現時点で確認されていない」と案内。
- **影響・対処**: PayPay残高とPayPayカードでの支払いは利用可。急ぎの場合はそちらへ切替。
- **復旧**: 本記事作成時点(26日 02:30頃)で未確認。続報要確認。
- **出典**: https://paypay.ne.jp/notice/20261125/m-01/ / https://news.web.nhk/newsweb/na/nd-20261125de81532 / https://www.yomiuri.co.jp/economy/20261126-GYT1T00023/

### 参考
- 銀行系では、11/6 のしんきん共同センター障害(信用金庫約半数でATM停止)は対象期間外のため割愛。今週の新規の銀行・証券の大規模障害は検索では確認できませんでした。

## 所感(今週の傾向)
- メガテックは「大規模停止」より、リリース(設定・コード変更)起因の軽微障害が散発する週でした。Cloudflare Access のように、変更の巻き戻しで直る型が目立ちます。
- Microsoft は障害後に組織レベルの見直しへ進んでおり、「復旧の速さ」が次の競争軸になりそうです。
- 日系は IT 自体の不具合より、災害(大雪・停電)による物理インフラ障害が主役でした。PayPay は現在進行形のため、続報を来週確認します。
- 注: 検索は9回で、網羅的調査ではありません。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
