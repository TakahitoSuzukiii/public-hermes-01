作成日: 2026-11-25 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-11-18〜2026-11-25

# CISA・JPCERT/CC 週報（2026-11-25）

## 📌 今週の要点

- **CISA KEV**（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規追加は **13件**（カタログ総数 1,795件）。先週の2件から大幅増。
- **ランサムウェア悪用が確認されたもの: 1件**（Synology DiskStation Manager の CVE-2024-10441）。残り12件は「Unknown＝不明」。
- 国内で特に注意: **Synology DSM**（ランサムウェア悪用済み・NAS＝ネットワーク接続ストレージ）、**VMware vCenter**（認証回避）、**Cisco Expressway**、**SAP NetWeaver**、**Drupal**（インストーラ経由のサイト乗っ取り）。JPCERT/CC は **PHP の脆弱性（CVE-2026-109618/109619）** の注意喚起を更新。
- KEV 13件のうち **9件の対処期限が既に過ぎている／数日以内**（米国連邦機関向け期限）。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規追加: **13件**（2026-11-18〜11-24 追加）

| CVE | ベンダー | 製品 | 追加日 | 対処期限 | ランサムウェア悪用 | 概要（要約） |
|---|---|---|---|---|---|---|
| [CVE-2026-132224](https://nvd.nist.gov/vuln/detail/CVE-2026-132224) | Optimizely | Web Experimentation | 11-24 | 11-27 | Unknown | アカウント登録処理で重要な状態データを外部から操作できる |
| [CVE-2026-131914](https://nvd.nist.gov/vuln/detail/CVE-2026-131914) | Idunno | AntiCsrf | 11-24 | 11-27 | Unknown | 信頼できないデータの復元（デシリアライズ）により、認証なしで任意コード実行。サポート終了製品の可能性あり |
| [CVE-2026-132165](https://nvd.nist.gov/vuln/detail/CVE-2026-132165) | Drupal | Core | 11-24 | 11-27 | Unknown | インストーラ（install.php）を悪用した再インストールで、サイト乗っ取り・任意コード実行の恐れ |
| [CVE-2026-133968](https://nvd.nist.gov/vuln/detail/CVE-2026-133968) | Project MONAI | MONAI Label | 11-23 | 11-26 | Unknown | パストラバーサルで、認証なしにサーバ上の任意の場所へファイルを書き込める |
| [CVE-2026-134624](https://nvd.nist.gov/vuln/detail/CVE-2026-134624) | N-able | MailAssure (SpamExperts) | 11-23 | 11-26 | Unknown | LDAP同期の接続確認機能にSSRF（サーバに内部へ通信させる攻撃）。認証済み攻撃者が対象 |
| [CVE-2026-129448](https://nvd.nist.gov/vuln/detail/CVE-2026-129448) | Apache | Roller | 11-20 | 11-23 | Unknown | デシリアライズ不備で、認証なしの任意コード実行 |
| [CVE-2026-123890](https://nvd.nist.gov/vuln/detail/CVE-2026-123890) | Broadcom | VMware vCenter | 11-20 | 11-23 | Unknown | Directory Service の代替経路を使った認証回避 |
| [CVE-2025-42884](https://nvd.nist.gov/vuln/detail/CVE-2025-42884) | SAP | NetWeaver | 11-20 | 11-23 | Unknown | Enterprise Portal のデータ照会ロジックで特殊文字の無害化が不十分（インジェクション） |
| [CVE-2026-76466](https://nvd.nist.gov/vuln/detail/CVE-2026-76466) | Cisco | Expressway Series | 11-20 | 11-23 | Unknown | ハードコードされた認証情報の利用。永続Cookieを持つ遠隔攻撃者が悪用可能 |
| [CVE-2024-10441](https://nvd.nist.gov/vuln/detail/CVE-2024-10441) | Synology | DiskStation Manager (DSM) | 11-18 | 11-21 | **Known（確認済み）** | システムプラグインデーモンの出力エスケープ不備（BeeStation OS含む） |
| [CVE-2026-40217](https://nvd.nist.gov/vuln/detail/CVE-2026-40217) | BerriAI | LiteLLM | 11-18 | 12-02 | Unknown | 保護されていない別経路により、バイトコード書き換えで遠隔コード実行 |
| [CVE-2026-90817](https://nvd.nist.gov/vuln/detail/CVE-2026-90817) | Vanderbilt Univ. | REDCap | 11-18 | 11-21 | Unknown | コードインジェクションで、認証なしの攻撃者がコード実行の恐れ |
| [CVE-2026-90436](https://nvd.nist.gov/vuln/detail/CVE-2026-90436) | Apache | Axis | 11-18 | 11-21 | Unknown | 安全でないリフレクション。細工したSOAPリクエストで任意コード実行 |

> ※対処期限（dueDate）は **米国連邦機関向けの期限** だが、一般の組織でも優先度の目安になる。

## 🎯 CVSS・OWASPスコア

> 📌 KEVやJPCERTの見出し・重大度ラベルは **CVSSではなく別物** です。CVSS（Common Vulnerability Scoring System＝共通脆弱性評価システム、0.0〜10.0）は NVD（米国の脆弱性DB）の値。出所の *Primary* は NVD自身の採点、*Secondary* は発行元(CNA＝CVE採番機関)の採点です。v3.1とv4.0は数値が比較できません。

採点対象: KEV新規13件＋JPCERT注意喚起のCVE 2件＝15件（上限20件以内）。

### ① CVSS（NVD取得値）

| CVE | 概要 | スコア | 深刻度 | 版 / 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-132224 | Optimizely 状態データ操作 | **8.7** | HIGH | v3.1 / Primary（NVD） | `AV:N/AC:L/PR:L/UI:R/S:C/C:H/I:H/A:N` |
| CVE-2026-131914 | AntiCsrf デシリアライズ | **9.3** | CRITICAL | v4.0 / Secondary（Mandiant）※v3.1は未掲載（NVDは受付中） | `AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:H/VA:H` |
| CVE-2026-132165 | Drupal Core | **未取得** | – | NVD未掲載（取得時点） | – |
| CVE-2026-133968 | MONAI Label パストラバーサル | **9.8** | CRITICAL | v3.1 / Secondary（MITRE） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-134624 | N-able MailAssure SSRF | **8.7** | HIGH | v3.1 / Primary（NVD） | `AV:N/AC:L/PR:H/UI:N/S:C/C:H/I:H/A:N` |
| CVE-2026-129448 | Apache Roller | **9.8** | CRITICAL | v3.1 / Secondary（Apache） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-123890 | VMware vCenter 認証回避 | **9.8** | CRITICAL | v3.1 / Secondary（VMware） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2025-42884 | SAP NetWeaver | **6.5** | MEDIUM | v3.1 / Secondary（SAP） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N` |
| CVE-2026-76466 | Cisco Expressway | **9.8** | CRITICAL | v3.1 / Secondary（Cisco） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2024-10441 | Synology DSM | **9.8** | CRITICAL | v3.1 / Secondary（Synology） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-40217 | LiteLLM | **8.8** | HIGH | v3.1 / Secondary（MITRE ほか） | `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-90817 | REDCap | **9.8** | CRITICAL | v3.1 / Secondary（Securifera） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-90436 | Apache Axis | **9.8** | CRITICAL | v3.1 / Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-109618 | PHP（JPCERT注意喚起） | **9.8** | CRITICAL | v3.1 / Primary（NVD）。v4.0は9.2（PHP Secondary） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-109619 | PHP（JPCERT注意喚起） | **8.1** | HIGH | v3.1 / Primary（NVD）。v4.0は9.2（PHP Secondary） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |

- 補足: CVE-2026-131914 のv3.1が未掲載のため、参考の**推定**（`AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`＝認証不要の遠隔コード実行を想定）は **9.8 CRITICAL（推定、公式値ではない）**。
- CVE-2026-132165 は取得時点でNVDに未掲載のため数値は付けていません（創作しない）。

### ② OWASP Risk Rating（推定）

「起きやすさ（尤度）×被害の大きさ（影響度）」を0〜9で評価（LOW<3 / MEDIUM 3〜<6 / HIGH 6〜9）。**公式値ではなく技術面のみの推定**（業務影響は未採点）。KEVは悪用実績があるため動機(motive)を高めに置いた。

| タイプ（該当CVE） | 尤度 | 影響度 | 総合（推定） | 根拠 |
|---|---|---|---|---|
| 認証不要の遠隔コード実行・認証回避（131914, 132165, 133968, 129448, 123890, 90817, 90436, 40217※, 76466） | 7.25 HIGH | 7.0 HIGH | **Critical** | ネットワーク経由・認証不要・悪用実績あり。影響は機密性/完全性/可用性とも高い（※40217は認証要で一段低いが同区分に近似） |
| Synology DSM（10441） | 7.25 HIGH | 7.0 HIGH | **Critical** | 上記同様＋ランサムウェア悪用済み |
| MONAI Label 任意ファイル書込（133968） | 7.25 HIGH | 6.5 HIGH | **Critical** | 書込中心で可用性影響をやや低く評価 |
| N-able MailAssure SSRF（134624） | 6.5 HIGH | 5.0 MEDIUM | **High** | 認証済み攻撃者が前提。可用性影響は小 |
| Optimizely（132224） | 6.62 HIGH | 5.5 MEDIUM | **High** | ユーザ操作が必要（UI:R）、可用性影響なし |
| SAP NetWeaver（42884） | 7.25 HIGH | 4.25 MEDIUM | **High** | 悪用は容易だが機密性・完全性の影響は限定的 |
| PHP（109618/109619） | 5.62 MEDIUM | 7.0 HIGH | **High** | 悪用に複雑な条件（AC:H等）が必要なため尤度は中程度。KEV未掲載 |

### ③ OWASP Top 10:2025 対応

Top 10はWebアプリ向け分類。以下は **推定**で、公式ページのMapped CWEsとの完全照合までは行っていない目安です。

| CVE | CWE | カテゴリ（推定） |
|---|---|---|
| 132224 | CWE-642（重要な状態データの外部制御） | A06 Insecure Design（推定） |
| 131914 / 129448 | CWE-502（信頼できないデータのデシリアライズ） | A08 Software or Data Integrity Failures |
| 132165 | CWE-636（安全に失敗しない） | A10 Mishandling of Exceptional Conditions（推定） |
| 133968 | CWE-24（パストラバーサル） | A01 Broken Access Control |
| 134624 | CWE-918（SSRF） | A01 Broken Access Control |
| 123890 | CWE-288（代替経路による認証回避） | A07 Authentication Failures |
| 42884 | CWE-943（データ照会ロジックのインジェクション） | A05 Injection |
| 76466 | CWE-798（ハードコード認証情報） | A07 Authentication Failures |
| 10441 | CWE-116（出力の不適切なエンコード） | A05 Injection（推定） |
| 40217 | CWE-420 / CWE-94 | A05 Injection（CWE-94、推定） |
| 90817 | CWE-73 / CWE-94 | A05 Injection（CWE-94、推定） |
| 90436 | CWE-470（安全でないリフレクション） | A05 Injection（推定） |
| 109618 / 109619 | CWE-416（解放後メモリ使用） | 対象外（メモリ破壊系でWebアプリ向け分類に非該当） |

### ④ 今週の優先度の所見

- 13件中 **9件がCVSS 9.8近辺の「認証不要の遠隔攻撃」型**。数値の差より「自組織で当該製品を使っているか」「インターネットに公開しているか」が先。
- **Synology DSM** はランサムウェア悪用が確認済みで最優先。**VMware vCenter** と **Cisco Expressway** は管理・境界の要で、侵害時の波及が大きい。
- SAPの6.5 MEDIUMはCVSS上は低めだが、KEV掲載＝悪用実績ありのため軽視しない。CVSS（理論上の深刻さ）とKEV（実際の悪用）は別軸。
- PHP（109618/109619）はKEV未掲載だが、CVSS 9.8とJPCERTの注意喚起が出ており、先手の更新確認が望ましい。

## 🛰 CISAアドバイザリ

合計9件 / 内訳: ICS（産業制御システム）6件、Alert 3件。Advisory・Analysis Reportは今週なし。

- **Alert（3件）:** KEV追加の告知（11-18に4件、11-20に4件、11-23に2件）。内容は上記KEV表と同一。
- **ICS（6件）:** Schneider Electric（EcoStruxure Power Build Rapsody）、Danfoss（AK-SM 8xxA）、AutomationDirect（C-More EA9）、Elecbrakes（EB2/VM1/ELBC2000）、Autonomy Logic（OpenPLC Runtime）、libumqtt。ICSのCVEは今回採点対象外（上限と優先度の都合で未採点）。

## 🇯🇵 JPCERT/CC 注意喚起

- **注意喚起（at260033、更新）:** PHPの複数の脆弱性（CVE-2026-109618、CVE-2026-109619）。2026-11-20に更新。PHPを使うWebサーバ・アプリは、修正版への更新確認を促す内容。https://www.jpcert.or.jp/at/2026/at260033.html
- **Weekly Report（wr261118、25項目）:** N-able N-central、ImageMagick、Synology DSM、Apple製品、PostgreSQL、Apache HTTP Server、Intel、Movable Type、OpenSSL、React Server Components、Node.js、MongoDB、Palo Alto、Confluence Data Center、Git、Adobe、Ivanti、Mozilla、Fortinet、Chrome、Microsoft製品などの脆弱性情報と、JPCERT/CCの「インシデント調査報告書チェックリスト」公開をまとめて掲載。https://www.jpcert.or.jp/wr/2026/wr261118.html

## ✅ 今週の対応の優先度（所見）

1. **KEV該当製品の棚卸し:** Synology DSM、VMware vCenter、Cisco Expressway、SAP NetWeaver、Drupal、Apache Roller/Axis などを利用していないか確認し、ベンダーの修正情報に従って更新。インターネット公開機器を優先。
2. **PHPの更新確認:** JPCERT/CCの更新された注意喚起を基に、利用中のPHPバージョンを確認。
3. **Weekly Reportの利用製品照合:** Chrome、Microsoft、OpenSSL、Node.js、Fortinet など広く使われる製品の更新状況を確認。

## 出典

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリ RSS: https://www.cisa.gov/ （公式RSSフィード）
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0

取得できなかった情報源: なし（ただし CVE-2026-132165 のNVD値は未掲載のため未取得）

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
