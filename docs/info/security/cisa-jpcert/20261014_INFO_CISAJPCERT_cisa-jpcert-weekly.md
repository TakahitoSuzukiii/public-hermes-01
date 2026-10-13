作成日: 2026-10-14 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-10-07〜2026-10-14

# CISA・JPCERT/CC 週報（2026-10-14）

## 📌 今週の要点

- **CISA KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は6件**（Ivanti Connect Secure、ISC BIND、Apache Struts、Strapi、ONLYOFFICE Docs、ProFTPD）。カタログ総数は1,740件。
- **ランサムウェア（身代金要求型マルウェア）での悪用は6件とも「Unknown（不明）」**。確認された、という記載はありません。
- 6件中5件は2015〜2023年公開の**古いCVE**で、同じ日（10-08）に追加。CISAの助言 AA26-281A（中国政府関連の攻撃者による情報窃取）が、これらを攻撃に使われたCVEとして挙げています。古い製品の放置が狙われています。
- 唯一の新しいCVEは **Ivanti Connect Secure（VPN機器）の認証回避**（CVE-2026-104935、対処期限 10-16）。境界機器の担当者は優先確認を。
- 日本国内では、JPCERT/CCが**「国内組織における不正アクセスに関する注意喚起」(at260030) を更新**（10-09）。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規 **6件**（カタログ総数 1,740件）。

| CVE | ベンダー | 製品 | 追加日 | 対処期限 | ランサムウェア悪用 | 概要（要約） |
|---|---|---|---|---|---|---|
| [CVE-2026-104935](https://nvd.nist.gov/vuln/detail/CVE-2026-104935) | Ivanti | Connect Secure | 10-13 | 10-16 | Unknown | なりすましによる認証回避で、未認証の遠隔攻撃者が任意コマンドを実行できる |
| [CVE-2015-5477](https://nvd.nist.gov/vuln/detail/CVE-2015-5477) | ISC | BIND | 10-08 | 10-11 | Unknown | TKEYクエリの処理不備で、遠隔からサービス拒否（DoS＝サービス停止）を起こせる |
| [CVE-2016-3081](https://nvd.nist.gov/vuln/detail/CVE-2016-3081) | Apache | Struts | 10-08 | 10-11 | Unknown | Dynamic Method Invocation有効時、method:prefix経由でコマンドインジェクション（任意コード実行） |
| [CVE-2023-22894](https://nvd.nist.gov/vuln/detail/CVE-2023-22894) | Strapi | Strapi | 10-08 | 10-11 | Unknown | 管理画面アクセス権を持つ者が、クエリフィルタ経由で機密情報（平文保存）を取得できる。サポート終了版の可能性。CVE-2023-22621と連鎖しRCEに至り得る |
| [CVE-2021-3199](https://nvd.nist.gov/vuln/detail/CVE-2021-3199) | ONLYOFFICE | Docs | 10-08 | 10-11 | Unknown | JWT利用時、画像アップロードのパラメータ経由のパストラバーサルでリモートコード実行に至り得る |
| [CVE-2015-3306](https://nvd.nist.gov/vuln/detail/CVE-2015-3306) | ProFTPD | ProFTPD | 10-08 | 10-11 | Unknown | site cpfr/cpto コマンドの不適切なアクセス制御で、任意ファイルの読み書きができる |

> ※ 対処期限（dueDate）は**米国連邦機関向けの期限**ですが、一般の組織でも対応優先度の目安になります。

## 🎯 CVSS・OWASPスコア

> 📌 **読み方の注意:** KEVやJPCERTの見出し・ラベルは **CVSS（Common Vulnerability Scoring System＝共通脆弱性評価システム、深刻度を0.0〜10.0で表す国際基準）ではありません**。CVSSはNVD（米国国立標準技術研究所の脆弱性DB）から取得した **v3.1の公式値** です。出所が *Primary* ならNVD自身の採点、*Secondary* なら **CNA（CVE採番機関＝発行元）の採点**です。採点対象は KEV新規6件＋CISA助言 AA26-281A に載る未採点の3件（計9件、上限20件以内）です。JPCERT注意喚起 at260030 にはCVE記載がありません。

### ① CVSS v3.1（公式値）

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ（攻撃条件） |
|---|---|---|---|---|---|
| CVE-2026-104935 | Ivanti Connect Secure 認証回避 | **8.6** | HIGH | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:L` |
| CVE-2015-5477 | BIND TKEY DoS | **7.5** | HIGH | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2016-3081 | Struts コマンドインジェクション | **8.1** | HIGH | Primary（NVD） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2023-22894 | Strapi 平文保存 | **4.9** | MEDIUM | Primary（NVD）※CNA値は7.2 HIGH | `AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:N/A:N` |
| CVE-2021-3199 | ONLYOFFICE パストラバーサル | **9.8** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2015-3306 | ProFTPD アクセス制御不備 | **10.0** | CRITICAL | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H` |
| CVE-2014-6278（AA26-281A記載） | Bash（Shellshock）コマンド実行 | **8.8** | HIGH | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2019-11510（AA26-281A記載） | Pulse Secure 任意ファイル読取 | **10.0** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H` |
| CVE-2021-22205（AA26-281A記載） | GitLab ExifTool RCE | **10.0** | CRITICAL | Primary（NVD） | `AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H` |

- `AV:N`＝ネットワーク経由で攻撃可、`PR:N`＝事前権限不要、`AC:H`＝攻撃条件が厳しい、`S:C`＝影響が他コンポーネントに波及。
- CVE-2014-6278 と CVE-2015-3306 のNVD出所はSecondaryのみ（NVD自身の採点は未取得／未掲載）。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology（OWASPのリスク評価手法）は **尤度（起きやすさ）× 影響度（被害の大きさ）** を0〜9で評価します。**以下は公式値ではなく、公開情報から見積もった「推定値」**です。業務への影響は環境依存のため採点せず、技術面のみです。KEV掲載のため悪用容易性(exploit)は9としています。

| CVE | 尤度 | 影響度（技術面） | 総合（推定） | 根拠のひとこと |
|---|---|---|---|---|
| CVE-2026-104935 | 6.12 HIGH | 6.5 HIGH | **Critical** | 未認証・遠隔でコマンド実行。機密性への影響大 |
| CVE-2015-5477 | 6.12 HIGH | 4.25 MEDIUM | **High** | 未認証・遠隔だが影響は可用性（停止）中心 |
| CVE-2016-3081 | 5.88 MEDIUM | 7.0 HIGH | **High** | 設定（DMI有効）が前提で尤度はやや低い。成功時の被害は大 |
| CVE-2023-22894 | 5.25 MEDIUM | 3.75 MEDIUM | **Medium** | 管理者権限が前提。単独では情報漏えい中心（連鎖でRCE） |
| CVE-2021-3199 | 6.12 HIGH | 7.5 HIGH | **Critical** | 未認証・遠隔でRCE |
| CVE-2015-3306 | 6.12 HIGH | 7.5 HIGH | **Critical** | 未認証・遠隔で任意ファイル読み書き |

要因値（推定）: skill 5／motive 4／opportunity 9（未認証）・7（前提あり）・4（管理者権限要）／size 6（4）／discovery 7／exploit 9／awareness 6／detection 3。影響は機密性・完全性・可用性・追跡可能性を脆弱性ごとに見積り。AA26-281A記載の3件（CVE-2014-6278／2019-11510／2021-22205）は**OWASP推定を行っていません（未採点）**。

### ③ OWASP Top 10:2025 との対応

Top 10は **Webアプリ向け** の分類です。NVDのCWE（弱点の種類の識別子）を元に対応づけました。**CWE-22のA01のみ前回記事でOWASP公式ページ照合済み**で、他は**今回公式ページ未照合の推定**です。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-104935 | CWE-290（なりすまし認証回避） | A07 Authentication Failures（推定） |
| CVE-2015-5477 | CWE-19／CWE-617 | **対象外**（Webアプリ向け分類に該当せず） |
| CVE-2016-3081 | CWE-77（コマンドインジェクション） | A05 Injection（推定） |
| CVE-2023-22894 | CWE-312（平文保存） | A04 Cryptographic Failures（推定） |
| CVE-2021-3199 | CWE-22（パストラバーサル） | A01 Broken Access Control（照合済み） |
| CVE-2015-3306 | CWE-284（不適切なアクセス制御） | A01 Broken Access Control（推定） |

### ④ 今週の優先度の所見

- **最優先は Ivanti Connect Secure（CVE-2026-104935、CVSS 8.6／OWASP推定Critical）**。VPN機器は外部公開されがちで、期限も10-16と近い。なおCVSSはCNA提供値です。
- **ONLYOFFICE Docs（9.8）・ProFTPD（10.0）**は数値が高く未認証で悪用可能。ただし**公開から5〜10年の古い脆弱性**で、パッチ未適用の古い環境が狙われています。
- Strapi は単独では4.9（NVD）だが、CNAは7.2としており**評価が割れる**。連鎖（CVE-2023-22621）に注意。
- CVSSとOWASPは意味が違い、数値の大小を単純比較できません。

## 🛰 CISAアドバイザリ

計5件: **Advisory 1件**、**ICS（Industrial Control Systems＝産業制御システム）4件**。Alert／Analysis Reportは今週なし。

- **Advisory（1件）AA26-281A（10-08）:** 中国政府関連とされる攻撃者が、自動化ツールと手動の侵入手法を組み合わせて機密データを窃取する、という内容。KEV今回追加の5件を含む複数の古いCVE（Shellshock、Pulse Secure、GitLabなど）が列挙されています。
- **ICS（4件）:** Swann Communications（SWIFI-SE2KIC）、Satel（Netco Design）、Grid Protection Alliance（openPDC／openHistorian）、Red Lion Controls（N-Tron 700 Series）。ICS分のCVE（計18件）は優先度の都合で今回**未採点**です。

## 🇯🇵 JPCERT/CC 注意喚起

- **注意喚起（at始まり）: 1件（更新）**
  - **at260030（10-09更新）:** 直近で相次ぐ国内組織への不正アクセスに関する注意喚起。**新規ではなく更新**。CVE番号は取得できず、詳細は原文を参照してください。
- **Weekly Report（wr261007、10-07号）:** 15項目。Chrome、Apache HTTP Server 2.4、FortiMail、Mozilla、Cisco SD-WAN Manager、OpenSSL、WatchGuard、HPE、Pgpool-II、Apple、Elastic、NetScaler等の脆弱性情報と、NCO法令Q&Aハンドブック、NICTER観測統計、早期警戒パートナーシップガイドライン2026年版の紹介。※前週にも取り上げた号です。

## ✅ 今週の対応の優先度（所見）

1. **Ivanti Connect Secure** を使っている場合は、ベンダー手順に従い緩和策／修正を最優先で適用し、侵害の痕跡も確認。
2. **古い製品の棚卸し**: Struts、BIND、ProFTPD、ONLYOFFICE Docs、Strapi など、サポート切れ・長期放置の公開サービスがないか確認（外部公開しているものを優先）。
3. 国内組織向け不正アクセスの更新注意喚起(at260030)を一読し、認証ログやVPN機器のログ確認体制を見直す。

## 取得できなかった情報源

なし（KEV JSON／CISA RSS／JPCERT RSS すべて取得成功）。ICS分CVEと、AA26-281A記載の3件のOWASP推定は未実施。

## 出典

- CISA KEV カタログ（JSON）: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリ RSS: https://www.cisa.gov/news-events/cybersecurity-advisories
- CISA AA26-281A: https://www.cisa.gov/news-events/cybersecurity-advisories/aa26-281a
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- JPCERT/CC 注意喚起 at260030: https://www.jpcert.or.jp/at/2026/at260030.html
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0
- OWASP Top 10:2025: https://owasp.org/Top10/2025/

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
