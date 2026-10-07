作成日: 2026-10-07 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-09-30〜2026-10-07

# CISA・JPCERT/CC 週報（2026-10-07）

## 📌 今週の要点

- **CISA KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は5件**（Citrix NetScaler、Zammad×2、Fortinet FortiMail、Cisco Catalyst SD-WAN Manager）。カタログ総数は1,734件。
- **ランサムウェア（身代金要求型マルウェア）での悪用は、5件とも「Unknown（不明）」**。確認された、という記載はありません。
- 5件中4件は**認証なしで外部から攻撃できる**タイプ（NetScaler、FortiMail、SD-WAN Manager、Zammadの一部）。境界機器・メール基盤の担当者は優先確認を。
- 日本国内では、JPCERT/CCが**NetScaler ADC/Gatewayの注意喚起を更新**（at260029）。同製品は今週KEVにも追加されており、同一製品群に対する動きが重なっています。
- JPCERT/CC週報（2026-10-07号）にも、FortiMail・Cisco SD-WAN Managerなど、KEV追加と同じ製品が掲載されています。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規 **5件**（カタログ総数 1,734件）。

| CVE | ベンダー | 製品 | 追加日 | 対処期限 | ランサムウェア悪用 | 概要（要約） |
|---|---|---|---|---|---|---|
| [CVE-2026-88779](https://nvd.nist.gov/vuln/detail/CVE-2026-88779) | Citrix | NetScaler ADC / Gateway | 10-04 | 10-07 | Unknown | メモリ領域の境界チェック不備により、サービス拒否（DoS＝サービス停止）を起こされ得る |
| [CVE-2026-102490](https://nvd.nist.gov/vuln/detail/CVE-2026-102490) | Zammad GmbH | Zammad | 10-02 | 10-05 | Unknown | 権限管理の不備で、ローカルの zammad ユーザが root へ権限昇格できる。CVE-2026-102489 と連鎖可能 |
| [CVE-2026-102489](https://nvd.nist.gov/vuln/detail/CVE-2026-102489) | Zammad GmbH | Zammad | 10-02 | 10-05 | Unknown | セッション固定（Session Fixation）により、zammad ユーザ権限でのリモートコード実行に至り得る |
| [CVE-2026-104286](https://nvd.nist.gov/vuln/detail/CVE-2026-104286) | Fortinet | FortiMail | 10-01 | 10-04 | Unknown | パストラバーサルとNULLバイト処理不備により、未認証の攻撃者が細工したHTTP(S)リクエストで任意ファイルを書き込める |
| [CVE-2026-76504](https://nvd.nist.gov/vuln/detail/CVE-2026-76504) | Cisco | Catalyst SD-WAN Manager | 09-30 | 10-03 | Unknown | URIの16進エンコード処理不備により、未認証の遠隔攻撃者が管理者権限でアクセスできる |

> ※ 対処期限（dueDate）は**米国連邦機関向けの期限**ですが、一般の組織でも対応優先度の目安になります。今週の5件はいずれも期限が作成日以前に到来済みです。

## 🎯 CVSS・OWASPスコア

> 📌 **読み方の注意:** KEVやJPCERTの見出し・ラベルは **CVSS（Common Vulnerability Scoring System＝共通脆弱性評価システム、深刻度を0.0〜10.0で表す国際基準）ではありません**。CVSSはNVD（米国国立標準技術研究所の脆弱性DB）から取得した **v3.1の公式値** を載せます。出所が *Primary* ならNVD自身の採点、*Secondary* なら **CNA（CVE採番機関＝発行元）の採点**です。採点対象は KEV新規5件＋JPCERT注意喚起の2件（計7件、上限20件以内）です。

### ① CVSS v3.1（公式値）

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ（攻撃条件） |
|---|---|---|---|---|---|
| CVE-2026-88779 | NetScaler のバッファ境界不備（DoS） | **7.5** | HIGH | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-102490 | Zammad の権限昇格（root化） | **9.8** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-102489 | Zammad のセッション固定→RCE | **9.8** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-104286 | FortiMail のパストラバーサル（任意ファイル書込） | **9.8** | CRITICAL | Secondary（CNA: Fortinet） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-76504 | Cisco SD-WAN Manager の認証回避 | **9.8** | CRITICAL | Secondary（CNA: Cisco） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-88771 | NetScaler の脆弱性（JPCERT注意喚起） | **9.8** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-88772 | NetScaler の脆弱性（JPCERT注意喚起） | **8.1** | HIGH | Primary（NVD） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |

- **CVSS v4.0** の値も併記されているものがあります（CVE-2026-88779: 8.7、CVE-2026-102489/102490: 9.4、CVE-2026-88771/88772: 9.5。いずれもCNA提供のSecondary）。**v3.1とv4.0は採点方式が違い、数値は比べられません**。
- `AV:N`＝ネットワーク経由で攻撃可、`PR:N`＝事前の権限不要、`AC:H`＝攻撃条件が厳しい。
- CVE-2026-88771/88772 は、JPCERT注意喚起の表題とNVDのスコアのみ確認しており、個別の技術詳細までは今回確認していません。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology（OWASPのリスク評価手法）は **尤度（起きやすさ）× 影響度（被害の大きさ）** を0〜9で評価します。**以下は公式値ではなく、公開情報から見積もった「推定値」**です。業務への影響（ビジネスインパクト）は環境依存のため採点せず、技術面のみです。

| CVE | 尤度 | 影響度（技術面） | 総合（推定） | 根拠のひとこと |
|---|---|---|---|---|
| CVE-2026-88779 | 6.0 HIGH | 4.25 MEDIUM | **High** | 未認証・遠隔で尤度は高いが、影響は可用性（停止）が中心 |
| CVE-2026-102490 | 5.38 MEDIUM | 6.5 HIGH | **High** | ローカル権限が前提で尤度は中。root化で影響は大 |
| CVE-2026-102489 | 6.0 HIGH | 7.0 HIGH | **Critical** | 遠隔でRCEに至り得る。上記と連鎖すると被害が拡大 |
| CVE-2026-104286 | 6.0 HIGH | 6.5 HIGH | **Critical** | 未認証で任意ファイル書込。完全性への被害が大きい |
| CVE-2026-76504 | 6.0 HIGH | 8.5 HIGH | **Critical** | 未認証で管理者権限を取得。機密性・完全性の被害が大きい |
| CVE-2026-88771 | 5.75 MEDIUM | 8.5 HIGH | **High** | 攻撃に前提条件あり。成功時の被害は大 |
| CVE-2026-88772 | 5.0 MEDIUM | 8.5 HIGH | **High** | 攻撃条件が厳しい（AC:H）が、成功時の被害は大 |

採用要因の基本値（尤度）: skill 5／motive 4／opportunity 9（未認証）または7・4（前提あり）／size 9または6／discovery 7／exploit 5（未確認は3）／awareness 6／detection 3。CVE毎の細かな差は上表の根拠のとおりで、すべて推定です。

### ③ OWASP Top 10:2025 との対応

Top 10は **Webアプリ向け** の分類です。CWE（弱点の種類の識別子）をOWASP公式の各カテゴリページ（`owasp.org/Top10/2025/`）の対応CWE一覧と照合しました。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-88779 | CWE-119（バッファ境界不備） | **対象外**（Webアプリ向け分類に該当せず） |
| CVE-2026-102490 | CWE-269（不適切な権限管理） | **A06:2025 Insecure Design** ※公式ページでCWE-269掲載を確認 |
| CVE-2026-102489 | CWE-384（セッション固定） | **A07:2025 Authentication Failures** ※CWE-384掲載を確認 |
| CVE-2026-104286 | CWE-22（パストラバーサル）、CWE-158（NULLバイト） | **A01:2025 Broken Access Control**（CWE-22掲載を確認）。CWE-158は対応表で確認できず |
| CVE-2026-76504 | CWE-177（URLエンコード処理不備） | **対象外**（対応表で確認できず） |
| CVE-2026-88771 / 88772 | 未取得 | **未取得**（CWE情報を取得していないため判定せず） |

### ④ 今週の優先度の所見

- 悪用が確認済み（KEV）かつ未認証・遠隔の **FortiMail（CVE-2026-104286）・Cisco SD-WAN Manager（CVE-2026-76504）** は、CVSS 9.8／OWASP推定Criticalで最優先です。ただし両者のCVSSは**CNA提供値**（NVD自身の採点ではない）です。
- **Zammad の2件は連鎖（RCE→root化）** します。単独評価より危険度が上がる点に注意してください。
- NetScaler は KEV分のDoS（7.5）と、JPCERT注意喚起分（9.8/8.1）で性質が違います。**別の脆弱性として切り分けて**確認してください。
- CVSSとOWASPは意味が違い、数値の大小を単純比較できません。

## 🛰 CISAアドバイザリ

計17件: **Alert 4件**、**ICS（Industrial Control Systems＝産業制御システム）13件**。Advisory／Analysis Reportは今週なし。

- **Alert（4件）:** いずれもKEV追加の通知（09-30 Cisco、10-01 FortiMail、10-02 Zammad×2、10-04 NetScaler）。上記KEV節と同内容です。
- **ICS（13件）:** 主要ベンダーは Hitachi Energy（REB500、Asset Suite、SOI、RTU500）、Johnson Controls（EasyIO FG／Neo系）、ABB（PCM600）、Armatura、Meari、Monta、Savannah（lwIP SMTPクライアント）など。CISA自身の製品 Malcolm も1件。ICS分のCVEは採点していません（優先度の都合で未採点）。

## 🇯🇵 JPCERT/CC 注意喚起

- **注意喚起（at始まり）: 1件（更新）**
  - **at260029（10-02更新）**: NetScaler ADC／Gateway の複数の脆弱性（CVE-2026-88771、CVE-2026-88772 等）。**新規ではなく更新**です。
- **Weekly Report（wr261007、10-07号）**: 15項目。脆弱性関連は Google Chrome、Apache HTTP Server 2.4、FortiMail（未認証でのリモートコード実行）、Mozilla製品、Cisco SD-WAN Manager（認証回避）、OpenSSL、WatchGuard、HPE、Pgpool-II、Apple、Elastic、NetScaler。その他、NCOの法令Q&Aハンドブック、NICTER観測統計、早期警戒パートナーシップガイドライン2026年版の公開紹介。
- 週報の各項目からはCVE番号が抽出できなかったため、週報分のCVE採点は行っていません。

## ✅ 今週の対応の優先度（所見）

1. **KEVの製品（FortiMail、Cisco SD-WAN Manager、NetScaler、Zammad）の利用有無を確認**し、ベンダー公式の対処（修正版適用・緩和策）を最優先で実施。インターネットに公開している機器は特に。
2. **NetScaler ADC/Gateway** は、KEV（DoS）とJPCERT更新注意喚起（複数脆弱性）の両方が出ているため、バージョンを確認し両方の対処状況を見る。
3. **Zammad** は2件が連鎖するため、片方だけの対応で終わらせない。あわせてブラウザ（Chrome／Mozilla／Apple）、Apache、OpenSSL等の汎用ソフトも週報のとおり更新状況を確認。

## 取得できなかった情報源

なし（KEV JSON／CISA RSS／JPCERT RSS すべて取得成功）。ただしCVE-2026-88771/88772のCWEは取得・照合していません。

## 出典

- CISA KEV カタログ（JSON）: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリ RSS: https://www.cisa.gov/news-events/cybersecurity-advisories
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- JPCERT/CC 注意喚起 at260029: https://www.jpcert.or.jp/at/2026/at260029.html
- JPCERT/CC Weekly Report 2026-10-07: https://www.jpcert.or.jp/wr/2026/wr261007.html
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0
- OWASP Top 10:2025: https://owasp.org/Top10/2025/

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
