作成日: 2026-11-19 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-11-12 〜 2026-11-19

# 週次システム障害まとめ(2026-11-12 〜 11-19)

> 用語: **障害** = サービスが使えない・使いづらい状態。**リージョン** = クラウドの物理的な拠点区分。**AZ(アベイラビリティーゾーン)** = リージョン内の独立した設備群。**5G SA(Standalone)** = 5G専用設備だけで動く通信方式。

## 🌐 メガテック系

### 1. Microsoft 365(Outlook / Teams / Copilot 等)世界規模の障害
- **発生日:** 2026-11-12(米国時間 木曜昼)〜11-14(約1日以上)
- **対象:** Exchange Online(Outlookメール)、Teams、SharePoint、Copilot、Defender XDR など
- **原因:** Microsoftは「以前のネットワーク容量増強の作業中に生じた問題が、その後のネットワーク変更で表面化した」と説明。多数のサーバーがヘルスチェックに失敗して使えなくなり、残りのサーバーに負荷が集中した。サイバー攻撃ではないとしている。
- **影響:** 70か国以上で報告。日本・シンガポール・豪州の政府業務にも影響。日本ではメール経由のワンタイムキー受信に影響した金融サービスもあった(楽天銀行が注意喚起、後に復旧)。
- **復旧:** 11-14(土)に完全復旧を発表。遅延メールの再送猶予は48時間に延長。詳細報告書は後日公表予定。
- **出典:** https://www.cnbc.com/2026/11/12/microsoft-outage-outlook-aws-google.html / https://apnews.com/article/microsoft-outage-outlook-email-365-recover-ca395c0f1e51af784b6d70afb6554f6a / https://www.rakuten-bank.co.jp/info/2026/261113.html

### 2. Apple(iCloud / Apple Pay / App Store 等)障害
- **発生日:** 2026-11-17(米国時間 火曜午前〜午後)
- **原因:** Appleは「内部アップデートが原因」と説明。サイバー攻撃ではない。
- **影響:** iCloud、Apple Pay、App Store、Apple Music、AppleCare など。米国のApple Storeでは店内ソフトが止まり決済・予約ができない例も。同日Gmailの報告も出たが、Googleは障害の証拠なしとしている。
- **復旧:** 同日夜(米東部時間18時)にステータスページ上は全て正常化。
- **出典:** https://www.nbcnews.com/business/corporations/apple-outages-working-get-systems-back-online-rcna609861 / https://www.theguardian.com/technology/2026/nov/17/gmail-apple-outage-major-disruption

### 3. AWS US-EAST-1(バージニア北部)接続障害
- **発生日:** 2026-11-15(UTC 12:38〜14:53、約2時間15分。AWS説明の影響時間帯は太平洋時間3:05〜6:10)
- **対象:** IAM Identity Center(社内SSOログイン基盤)のサインイン、AWSサインアップ、一部のNLB(ロードバランサー)
- **原因:** 公式の事後報告は未公表。
- **復旧:** 同日解消。失敗した要求は再試行を推奨。
- **出典:** https://www.epifive.com/blog/aws-us-east-1-outage-november-2026-what-to-do / https://statusgator.com/services/amazon-web-services/outage-history

### 4. AWS 東京(ap-northeast-1)API異常・インスタンス起動失敗
- **発生日:** 2026-11-11 15:40 UTC(日本時間 11-12 00:40頃)〜 約5.5時間
- **影響:** 単一AZ(apne1-az1)で新規インスタンス起動・ゲートウェイ等の作成に断続的な失敗。既存リソースの通信は影響なし。
- **復旧:** 同日解消(Minor)。
- **出典:** https://rewindex.com/company/aws/2026/11

### 参考: Cloudflare
11月は軽微(Minor)なインシデントが多数(インド・パリ・東京NRT等のネットワーク性能低下、R2エラー、11/18の日本向けR2ダウンロード遅延 約1時間18分など)。大規模障害の記録なし。出典: https://liveordown.com/cloudflare/outages/2026-11

### Google Cloud / Meta
今回の検索では大規模障害を確認できず。

## 🇯🇵 日系企業系

### 1. NTTドコモ 5G SA 通信障害(今月3回目)
- **発生日:** 2026-11-16 10:02〜15:58(約5時間56分)
- **対象:** 5G SA契約者の音声通話・データ通信・SMS(圏外表示になる場合あり)。全国。
- **原因:** 5G SA契約者を収容する交換機への通信集中。11/5・11/11と同じ原因。不正アクセスやサイバー攻撃の形跡は確認されていない。
- **影響範囲外:** MVNO、5G SA以外の5G/4G、緊急通報。
- **対処:** 暫定策として4Gを選択し再起動・機内モード切替で使える場合あり。復旧後は設定を戻す。
- **復旧:** 完全復旧済み。ただし同種障害の3度目で再発防止策が焦点。
- **出典:** https://japan.cnet.com/article/35254955/ / https://www.docomo.ne.jp/info/network/kanto/pages/261116_04_m.html / https://newsdig.tbs.co.jp/articles/-/3089125

### その他
銀行・決済(みずほ/三菱UFJ/PayPay等)で、今週新たに確認できた大規模障害はなし(11/6の信用金庫障害は前週記事で扱い済みのため割愛)。

## 所感(今週の傾向)
- 米国で「Microsoft→FAA・銀行→Apple」と大規模障害が連鎖したが、報道では相互の関連は確認されておらず、いずれも原因は内部変更・アップデート由来(サイバー攻撃ではない)。変更管理の重要性を再認識させる週でした。
- ドコモは同一原因で月3回。再発防止の実効性が問われます。
- メール依存の認証(ワンタイムキー)がメール基盤障害で止まる点は、利用者側の代替手段確保の観点で参考になります。
- 注意: 検索は12回の上限内(実施9回)で、報道ベースの確認です。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
