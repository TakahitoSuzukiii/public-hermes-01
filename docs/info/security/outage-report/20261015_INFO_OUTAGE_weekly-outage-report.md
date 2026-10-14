作成日: 2026-10-15 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-10-09 〜 2026-10-15

# 週次システム障害まとめ(2026-10-09〜10-15)

専門用語は初出時に補足しています。前週(10/8版)と重複する障害(IDCフロンティア障害の発生自体など)は、新たな進展があるものだけ続報として扱います。

## 🌐 メガテック系

### 1. Microsoft 365: Global Secure Access(GSA)経由で Outlook/Teams 等に接続できず(10/13)
- 発生日: 2026-10-13(UTC 07:40〜18:31、約11時間)
- 対象: Outlook、OneDrive、SharePoint Online、Teams、Windows 365 Cloud PC
- 原因: GSA(Microsoft の SSE=Security Service Edge、社内通信をクラウド経由で守る仕組み)の一部インフラの性能低下と説明されています。
- 影響: 当初はドイツ・英国、後にドイツのみと範囲を修正。GSAを使っていないユーザーは対象外。回避策は「GSAを一時的に無効化」。
- 復旧: トラフィック迂回、再起動を経て解消。Microsoft は事後報告書(PIR)を予定。
- 出典: https://www.365fanatic.com/m365-status/MO1505952/ / https://blog.incidenthub.cloud/2026-10-14-microsoft-365-gsa-outage-oct-13-2026

### 2. Google Cloud Storage: us-central1 で書き込みエラー・遅延(10/8、報道は10/12)
- 発生日: 2026-10-08(UTC 11:00〜23:30、約12.5時間)※対象期間の直前ですが、事後解説の報道が期間内のため掲載
- 対象: Cloud Storage のアップロード/書き込み(一部の読み取りも)
- 原因: 公式ページでは詳細未確認(本調査では原因の記載を確認できず)
- 復旧: 解消済み
- 出典: https://blog.incidenthub.cloud/2026-10-12-google-cloud-storage-outage-oct-8-2026 / https://status.cloud.google.com/incidents/mSFVt6PiP557bjRyYsut

### 3. Cloudflare: 軽微な障害が複数(10/10〜10/14)
- 10/10: 管理画面・APIのエラー(日本時間11:12復旧)。
- 10/13〜14: 米国Ashburn拠点で第三者回線の保守作業に伴う速度低下(短時間)。
- 10/14: 新規作成・変更した Workers の Cron Trigger(定期実行)が動かない問題(日本時間0:18公表、9:09復旧)。監査ログの問題は継続。
- 出典: https://www.chasms.com/blog/daily-outage-brief-2026-10-13/ / https://funshitsu.com/status/

### 備考
- AWS: 10/8に短時間の計測上の断(約12分、HostTrackerの外形監視)のみ。AWSの「サーマルイベント(冷却障害)」を伝える記事(CRN)は日付を本調査で特定できず、今週分としては扱いません。
- 出典(参考): https://www.host-tracker.com/en/is-aws-down/incidents/2026-10-08-2143

## 🇯🇵 日系企業系

### 1. PayPay証券: 日本株・ETFの全銘柄で取引停止(10/13〜10/14)
- 発生日: 2026-10-13 10:15ごろ〜(昼に一時再開後、再停止)。14日9時に復旧発表。
- 対象: 日本株・ETF(ETF=上場投資信託)の全銘柄の取引。14日の予約注文も停止。
- 原因: 報道では外部接続先の障害とされています(詳細は未公表)。
- 影響: 取引不可。損失補填は規約上原則対象外と報じられています。
- 出典: https://k-tai.watch.impress.co.jp/docs/news/2147752.html / https://japan.cnet.com/article/35253508/ / https://funshitsu.com/status/

### 2. SBI証券: FX株券担保サービスで代用評価額が反映されず、誤ロスカット(10/12〜10/13)
- 発生日: 2026-10-12 取引開始時〜10/13 5:30(臨時メンテで復旧)
- 原因: 再委託先の運用担当者の作業誤り(10/10未明、遅延したファイルの取込み処理を再実行しなかった)。必要ファイルの揃い確認なしに後続処理が進む設計も要因。
- 影響: 779口座で本来不要なロスカット(強制決済)。ポジション復元など個別対応中。不正アクセス・情報流出はなし。
- 出典: https://www.sbigroup.co.jp/news/pdf/group/2026/1014_b.pdf

### 3. 防災情報配信サービス「SpeeCAN RAIDEN」(アルカディア)への不正アクセス(10/11〜継続)
- 発生日: 2026-10-11に不審な挙動を確認
- 影響: 約800自治体が利用。13日21時時点で36自治体が防災メール配信などを停止。住民のメールアドレス最大約313.6万件が漏洩した可能性。総務省が報告を要求。
- 出典: https://www.sankei.com/article/20261014-QDGM2FJYOROZRPMWIWAFYPNSDU/

### 4. IDCフロンティア(IDCFクラウド)不正アクセス障害の続報(10/7発生・10/14第5報)
- 内容: 影響4ゾーンの仮想サーバー内データの外部流出は確認されず。影響495企業・自治体のうち194社はスナップショット機能のバックアップ取り出しが可能と判明。ポータルで48社の登録情報への不正照会あり(外部持出しの痕跡なし)。
- 波及: ドコモ「あんしんフィルター」の一部機能が7日から停止継続(復旧未定)。
- 出典: https://www.idcf.jp/news/topics/20261014001 / https://funshitsu.com/status/

### 5. その他
- ドコモメール: 10/6に一部で不具合(18:26復旧)。期間外のため参考。 https://www.docomo.ne.jp/info/network/
- BroadLine(TOKAIコミュニケーションズ)通信障害: 10/13 8:53〜9:17。 https://funshitsu.com/status/

## 所感(今週の傾向)
- 日系は「外部委託・再委託先」起点の事故が目立ちました(SBI証券の再委託先ミス、PayPay証券の外部接続先、IDCF)。委託先管理と「前工程が完了したか検証して止める」設計が鍵です。
- 不正アクセス系(アルカディア、IDCF)が自治体サービスに波及し、長期化しています。
- メガテックは大規模停止はなく、M365のGSAのように「特定機能を使う利用者だけ」が長時間影響を受ける型でした。
- 検索回数の制約(12回)により網羅性には限りがあります。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
