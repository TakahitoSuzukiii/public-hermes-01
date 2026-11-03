作成日: 2026-11-04 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-10-28〜2026-11-04

# CISA・JPCERT/CC 週報（2026-10-28〜2026-11-04）

## 📌 今週の要点

- **KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は6件**（カタログ総数1766件）。ランサムウェア悪用の記載は**なし**（全件 Unknown）。
- 対象は **Ivanti Connect Secure（2件・連鎖利用が示唆）**、**GitLab CE/EE（未認証RCE）**、**Cisco Secure Firewall ASA/FTD（DoS）**、**Broadcom VMware ESX（ログ不備）**、**Linux カーネル**。Linuxカーネルの件は、PHPの脆弱性（先週のKEV）と連鎖させるとWebシェル設置→root権限でのコマンド実行に至る旨がCISAの概要に書かれている。
- 日本国内向けには、JPCERT/CCが **PHPの複数の脆弱性（at260033）を更新**（10/29）。ほかは Weekly Report（wr261028）のみで、新規の注意喚起（at）は無し。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規 **6件**。出典: [CISA KEV JSON](https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json)

| CVE | ベンダー/製品 | 追加日 | 対処期限 | ランサム悪用 | 概要（要約） |
|---|---|---|---|---|---|
| [CVE-2026-118527](https://nvd.nist.gov/vuln/detail/CVE-2026-118527) | Ivanti / Connect Secure | 10-30 | 11-13 | Unknown | 予測可能な識別子の生成。認証済みの遠隔攻撃者が既知の場所に任意内容のファイルを置ける。他の2件と連鎖利用可 |
| [CVE-2026-111357](https://nvd.nist.gov/vuln/detail/CVE-2026-111357) | Ivanti / Connect Secure | 10-30 | 11-02 | Unknown | 重要機能の認証欠如。ローカル認証済みの攻撃者が権限昇格できる |
| [CVE-2026-97229](https://nvd.nist.gov/vuln/detail/CVE-2026-97229) | GitLab / CE・EE | 10-29 | 11-01 | Unknown | 整数オーバーフロー。CI/CD設定内の細工した正規表現により、未認証でサーバ上のコード実行が可能 |
| [CVE-2026-76418](https://nvd.nist.gov/vuln/detail/CVE-2026-76418) | Cisco / Secure Firewall ASA・FTD | 10-29 | 11-01 | Unknown | 戻り値の未検査によるNULLポインタ参照。未認証の遠隔攻撃者が装置を再起動させDoS（サービス拒否）にできる |
| [CVE-2026-41709](https://nvd.nist.gov/vuln/detail/CVE-2026-41709) | Broadcom / VMware ESX | 10-28 | 11-11 | Unknown | ログ記録の不備。管理者権限を持つ者の一部操作が記録されない |
| [CVE-2026-46300](https://nvd.nist.gov/vuln/detail/CVE-2026-46300) | Linux / Kernel | 10-28 | 10-31 | Unknown | 変数の初期化漏れ。ソケットバッファ結合時にESP処理が共有領域をその場で復号し、ページキャッシュ上のデータが意図せず書き換わり得る |

> 注: 対処期限（dueDate）は米国連邦機関向けの期限だが、一般の組織でも優先度の目安になる。

## 🎯 CVSS・OWASPスコア

採点対象は、KEV新規6件＋JPCERT注意喚起のCVE2件（PHP）＋CISA ICSアドバイザリのCVE7件の計15件（上限20件以内）。KEV/JPCERT/CISAの見出し・ラベルはCVSSではない。

### ① CVSS（共通脆弱性評価システム）公式値（NVD API取得）

Primary=NVD自身の採点、Secondary=CNA（CVE採番組織）等の採点。版（v3.1/v4.0）が違う値は比較不能。

| CVE | 概要 | CVSS | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-118527 | Ivanti 予測可能ID／ファイル設置 | 4.3 (v3.1) | MEDIUM | Secondary (CNA) | AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:L/A:N |
| CVE-2026-111357 | Ivanti 認証欠如／権限昇格 | 7.0 (v3.1) | HIGH | Secondary (MITRE) | AV:L/AC:H/PR:L/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-97229 | GitLab 未認証RCE | 10.0 (v3.1) | CRITICAL | Secondary (GitLab) | AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H |
| CVE-2026-76418 | Cisco ASA/FTD DoS | 8.6 (v3.1) | HIGH | Secondary (Cisco PSIRT) | AV:N/AC:L/PR:N/UI:N/S:C/C:N/I:N/A:H |
| CVE-2026-41709 | VMware ESX ログ不備 | 2.7 (v3.1) | LOW | Secondary (VMware) | AV:N/AC:L/PR:H/UI:N/S:U/C:N/I:L/A:N |
| CVE-2026-46300 | Linux カーネル | 7.8 (v3.1) | HIGH | Primary (NVD)（Secondary 2件も同値） | AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-109618 | PHP（JPCERT at260033） | 9.8 (v3.1) | CRITICAL | Primary (NVD) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-109619 | PHP（JPCERT at260033） | 8.1 (v3.1) | HIGH | Primary (NVD) | AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-43284 | Hitachi Energy CoreTec（ICS） | 8.8 (v3.1) | HIGH | Secondary（同CVEにSecondary 7.8が2件） | AV:L/AC:L/PR:L/UI:N/S:C/C:H/I:H/A:H |
| CVE-2026-89209 | Siemens Mendix SAML（ICS） | 6.8 (v3.1) | MEDIUM | Secondary (Siemens) | AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:N |
| CVE-2026-13162 | Hitachi Energy CoreTec（ICS） | v3.1掲載なし | － | － | v4.0のみ: 7.7 HIGH (Secondary) |
| CVE-2026-10756 | Hitachi Energy TRO600（ICS） | v3.1掲載なし | － | － | v4.0のみ: 7.7 HIGH (Secondary) |
| CVE-2026-106087 | Hitachi Energy TRO600（ICS） | v3.1掲載なし | － | － | v4.0のみ: 8.7 HIGH (Secondary) |
| CVE-2026-63017 / 63774 | Subnet Solutions PowerSYSTEM Center（ICS） | **未取得**（NVDに未掲載） | － | － | － |

補足: PHP 2件のv4.0は9.2 CRITICAL（Secondary、PHP）、Siemens CVE-2026-89209のv4.0は7.6 HIGH（Secondary）。いずれもv3.1と比較不可。

### ② OWASP Risk Rating（尤度×影響度）— **すべて推定**

CVSSベクタから機械換算（skill=5, motive=4, size=6, discovery=7, exploit=5, awareness=6, detection=3、追跡可能性=7を固定。遠隔・未認証→opportunity=9、遠隔・低権限→7、ローカル／高権限／ユーザ操作要→4。影響は機密性・完全性・可用性のH=9、L=3、N=1）。業務影響は環境依存のため採点せず、技術ベースの推定。

| CVE | 尤度 | 影響度 | 総合(推定) | 根拠 |
|---|---|---|---|---|
| CVE-2026-118527 | 5.38 MEDIUM | 3.0 MEDIUM | Medium | 低権限の遠隔／完全性のみ低 |
| CVE-2026-111357 | 5.00 MEDIUM | 8.5 HIGH | High | ローカル・AC高／CIA全てH |
| CVE-2026-97229 | 5.62 MEDIUM | 8.5 HIGH | High | 未認証・遠隔／CIA全てH |
| CVE-2026-76418 | 5.62 MEDIUM | 4.5 MEDIUM | Medium | 未認証・遠隔／可用性のみH |
| CVE-2026-41709 | 5.00 MEDIUM | 3.0 MEDIUM | Medium | 管理者権限が必要。ただしログ欠落は追跡可能性に直結するため、調査時は過小評価に注意 |
| CVE-2026-46300 | 5.00 MEDIUM | 8.5 HIGH | High | ローカル低権限／CIA全てH |
| CVE-2026-109618 | 5.62 MEDIUM | 8.5 HIGH | High | 未認証・遠隔／CIA全てH |
| CVE-2026-109619 | 5.00 MEDIUM | 8.5 HIGH | High | 未認証だがAC高（尤度は低め見積り） |
| CVE-2026-43284 | 5.00 MEDIUM | 8.5 HIGH | High | ローカル低権限／CIA全てH |
| CVE-2026-89209 | 5.00 MEDIUM | 6.5 HIGH | High | ユーザ操作要・AC高／機密性・完全性H |
| CVE-2026-13162 | 5.38 MEDIUM | 8.5 HIGH | High | v4.0ベクタから換算（参考値） |
| CVE-2026-10756 | 5.38 MEDIUM | 8.5 HIGH | High | v4.0ベクタから換算（参考値） |
| CVE-2026-106087 | 5.62 MEDIUM | 4.5 MEDIUM | Medium | v4.0ベクタから換算（参考値）。機密性のみH |

### ③ OWASP Top 10:2025 対応（推定・CWE→カテゴリ）

NVD記載のCWEを各カテゴリ公式ページ（https://owasp.org/Top10/2025/）のMapped CWEsと照合。Top 10はWebアプリ向け分類のため、該当が無いものは「対象外」。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-118527 | CWE-340（予測可能な識別子） | A04 Cryptographic Failures |
| CVE-2026-111357 | CWE-829（NVD）。KEV側はCWE-306/862/345 | A08 Software or Data Integrity Failures（306はA07、862はA01にも該当） |
| CVE-2026-97229 | CWE-190（整数オーバーフロー） | 対象外 |
| CVE-2026-76418 | CWE-690（戻り値未検査） | 対象外 |
| CVE-2026-41709 | CWE-778（ログ不足） | A09 Security Logging and Alerting Failures |
| CVE-2026-46300 / 43284 | CWE-787/456/123 | 対象外（カーネルのメモリ関連） |
| CVE-2026-109618 / 109619 | CWE-416/755/824/1325 | A10 Mishandling of Exceptional Conditions（CWE-755が該当。他は対象外） |
| CVE-2026-13162 | CWE-78 | A05 Injection（先週の照合結果に準拠） |
| CVE-2026-10756 | CWE-923 | 対象外（今回の照合で一致せず） |
| CVE-2026-106087 | CWE-306 | A07 Authentication Failures |
| CVE-2026-89209 | CWE-294 | A07 Authentication Failures |

### ④ 今週の優先度の所見

- 最優先: **GitLab（CVE-2026-97229、CVSS 10.0）**。未認証でRCE、KEV期限は11/01で既に超過。
- 次点: **Linuxカーネル（CVE-2026-46300、7.8）**。CVSS単体は中程度だが、概要上はPHP RCE（CVE-2026-109618/109619）と連鎖してroot権限奪取に至るため、PHP環境と併せて確認したい。
- **Ivanti Connect Secure** 2件（4.3 / 7.0）は単体のスコアは高くないが、別CVE（CVE-2026-104935）を含む3件連鎖が示されており、スコアだけで優先度を下げない。CVE-2026-104935は今週のKEV新規ではないため未採点。
- CVSSとOWASP推定は意味が異なり、単純な大小比較はしない。

## 🛰 CISAアドバイザリ

計7件: ICS(産業制御) 4 / Alert 3。出典: [CISA RSS](https://www.cisa.gov/cybersecurity-advisories/all.xml)

- **Alert**: KEV追加通知3件（[10/28](https://www.cisa.gov/news-events/alerts/2026/10/28/cisa-adds-two-known-exploited-vulnerabilities-catalog)、[10/29](https://www.cisa.gov/news-events/alerts/2026/10/29/cisa-adds-two-known-exploited-vulnerabilities-catalog)、[10/30](https://www.cisa.gov/news-events/alerts/2026/10/30/cisa-adds-two-known-exploited-vulnerabilities-catalog)。各2件）。
- **ICS（Industrial Control Systems＝産業制御システム）4件**: Subnet Solutions PowerSYSTEM Center（[ICSA-26-307-01](https://www.cisa.gov/news-events/ics-advisories/icsa-26-307-01)）、Hitachi Energy CoreTec（[ICSA-26-302-03](https://www.cisa.gov/news-events/ics-advisories/icsa-26-302-03)）、Hitachi Energy TRO600（[ICSA-26-302-02](https://www.cisa.gov/news-events/ics-advisories/icsa-26-302-02)）、Siemens Mendix SAMLモジュール（[ICSA-26-302-01](https://www.cisa.gov/news-events/ics-advisories/icsa-26-302-01)）。
- Advisory / Analysis Report は今週なし。

## 🇯🇵 JPCERT/CC 注意喚起

注意喚起（at）**1件（更新）**、Weekly Report項目15件（計16件）。出典: [JPCERT/CC RSS](https://www.jpcert.or.jp/rss/jpcert.rdf)

- [at260033](https://www.jpcert.or.jp/at/2026/at260033.html)（**更新** 10/29）: PHPの複数の脆弱性（CVE-2026-109618、CVE-2026-109619）。スコアは上記①②③（CVSS 9.8／8.1、OWASP推定 High、Top10 A10）。
- **Weekly Report（[wr261028](https://www.jpcert.or.jp/wr/2026/wr261028.html)）**: VeloCloud Orchestrator（SQLインジェクション）、ISC BIND、Cisco製品、GitLab、Apache Tomcat、Chrome、Atlassian、Mozilla、Laravel TokenGuard（認証回避）、Roundcube、MOVEit Transfer、Oracle製品の脆弱性情報と、PHP注意喚起の再掲、脆弱性届出状況・四半期レポートの公開を掲載。個別CVEはPHPの2件のみ記載されているため、他は未採点。

## ✅ 今週の対応の優先度（所見）

1. GitLab（CE/EE）の利用有無とバージョン確認、修正版への更新。外部公開の範囲確認。
2. PHP環境とLinuxカーネルの更新状況確認。両者の連鎖攻撃が示されているため、Webサーバ基盤は両方を同時に点検。
3. Ivanti Connect Secure、Cisco ASA/FTD、VMware ESXの利用有無確認とベンダー情報に沿った対応。KEV期限（11/01〜11/13）の多くは既に過ぎている。

## 取得できなかった情報源

なし（3フィードとも取得成功）。NVDでCVE-2026-63017 / CVE-2026-63774は未掲載のため未取得。

## 出典

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA RSS: https://www.cisa.gov/cybersecurity-advisories/all.xml
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0
- OWASP Risk Rating: https://owasp.org/www-community/OWASP_Risk_Rating_Methodology / Top 10:2025: https://owasp.org/Top10/2025/

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
