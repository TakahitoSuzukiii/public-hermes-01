作成日: 2026-10-21 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-10-14〜2026-10-21

# CISA・JPCERT/CC 週報（2026-10-14〜2026-10-21）

## 📌 今週の要点

- **KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は7件**（カタログ総数1748件）。ランサムウェア悪用の記載は**なし**（全件 Unknown）。
- 7件の対象は BeyondTrust Remote Support / Fortinet / Atlassian / Ahsay AhsayCBS（2件・連鎖利用可）/ Cisco Secure Email Gateway / Palo Alto PAN-OS。境界機器・管理系製品が中心。
- CISAは BeyondTrust Remote Support の重大な脆弱性への対応を個別にAlertで促している。
- 日本国内向けには、JPCERT/CC が SiteGuard Server Edition のOSコマンドインジェクション（CVE-2026-106931）と、10月のMicrosoft月例更新の注意喚起を発行。Weekly Reportでは「国内組織への不正アクセス相次ぐ」旨の注意喚起も掲載。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規 **7件**。出典: [CISA KEV JSON](https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json)

| CVE | ベンダー/製品 | 追加日 | 対処期限 | ランサム悪用 | 概要（要約） |
|---|---|---|---|---|---|
| [CVE-2026-102764](https://nvd.nist.gov/vuln/detail/CVE-2026-102764) | BeyondTrust / Remote Support | 10-16 | 10-19 | Unknown | なりすましによる認証回避。リモートから機器上でファイル操作が可能 |
| [CVE-2025-61624](https://nvd.nist.gov/vuln/detail/CVE-2025-61624) | Fortinet / FortiOS, FortiPAM, FortiProxy, FortiSwitchManager | 10-16 | 10-19 | Unknown | パストラバーサル。管理者権限の認証済み攻撃者がCLIで任意ファイルの書込/削除 |
| [CVE-2026-21589](https://nvd.nist.gov/vuln/detail/CVE-2026-21589) | Atlassian / Bitbucket, Confluence, Jira 等 Data Center系 | 10-15 | 10-18 | Unknown | 未認証でWebルート配下の特定ファイルにアクセスできる |
| [CVE-2026-105134](https://nvd.nist.gov/vuln/detail/CVE-2026-105134) | Ahsay / AhsayCBS | 10-14 | 10-17 | Unknown | コマンドインジェクション。OSコマンド実行が可能。CVE-2026-105133と連鎖可 |
| [CVE-2026-105133](https://nvd.nist.gov/vuln/detail/CVE-2026-105133) | Ahsay / AhsayCBS | 10-14 | 10-17 | Unknown | 認証不備による認証回避。CVE-2026-105134と連鎖可 |
| [CVE-2026-76519](https://nvd.nist.gov/vuln/detail/CVE-2026-76519) | Cisco / Secure Email Gateway | 10-14 | 10-17 | Unknown | 相対パストラバーサル。未認証でOS上に任意ファイル書込 |
| [CVE-2026-0322](https://nvd.nist.gov/vuln/detail/CVE-2026-0322) | Palo Alto Networks / PAN-OS | 10-14 | 10-17 | Unknown | コードインジェクション。認証済み攻撃者がroot権限で任意コード実行 |

> 注: 対処期限（dueDate）は米国連邦機関向けの期限だが、一般の組織でも優先度の目安になる。

## 🎯 CVSS・OWASPスコア

採点対象はKEV新規7件＋JPCERT注意喚起の1件（計8件、上限20件以内）。KEVやJPCERT/CISAの見出し・ラベルはCVSSではない。CISAアドバイザリ（ICS）掲載CVE約40件は今回**未採点**（優先度の都合。各アドバイザリ参照）。

### ① CVSS（共通脆弱性評価システム）公式値（NVD API取得）

Primary=NVD自身の採点、Secondary=CNA（CVE採番組織）の採点。版の違う値は比較不能。

| CVE | CVSS | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|
| CVE-2026-102764 | 9.8 (v3.1) | CRITICAL | Primary (NVD) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2025-61624 | 6.5 (v3.1) | MEDIUM | Primary (NVD) | AV:N/AC:L/PR:H/UI:N/S:U/C:N/I:H/A:H |
| CVE-2025-61624（参考） | 6.0 (v3.1) | MEDIUM | Secondary (Fortinet PSIRT) | AV:L/AC:L/PR:H/UI:N/S:U/C:N/I:H/A:H |
| CVE-2026-21589 | 7.5 (v3.1) | HIGH | Primary (NVD) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N |
| CVE-2026-105134 | 10.0 (v3.1) | CRITICAL | Secondary (VulDB CNA) | AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H |
| CVE-2026-105133 | 7.3 (v3.1) | HIGH | Secondary (VulDB CNA) | AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L |
| CVE-2026-76519 | 9.8 (v3.1) | CRITICAL | Secondary (Cisco PSIRT) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-0322 | 7.2 (v3.1) | HIGH | Primary (NVD) | AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-106931（JPCERT） | 7.8 (v3.0) / 8.5 (v4.0) | HIGH | Secondary (JPCERT/CC) | v3.0: AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H |

補足: v4.0の値（参考・v3.1と比較不可）— CVE-2026-102764: 9.3 / CVE-2026-21589: 9.3（Atlassian）/ CVE-2026-105134: 9.3 / CVE-2026-105133: 5.5 / CVE-2026-0322: 8.6（Palo Alto）。CVE-2026-76519 は v3.1のみ。

### ② OWASP Risk Rating（尤度×影響度）— **すべて推定**

CVSSベクタから機械換算（攻撃元区分・必要権限→opportunity、skill=5, motive=4, discovery=7, exploit=5, awareness=6, detection=3、追跡可能性=7を固定。KEV掲載は悪用実績ありだが換算値は固定のまま）。業務影響は環境依存のため採点せず、技術ベースの推定。

| CVE | 尤度 | 影響度 | 総合(推定) | 根拠（機密性,完全性,可用性,追跡性） |
|---|---|---|---|---|
| CVE-2026-102764 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 未認証・遠隔 |
| CVE-2025-61624 | 5.0 MEDIUM | 6.5 HIGH | High | 1,9,9,7 / 管理者権限が必要 |
| CVE-2026-21589 | 5.62 MEDIUM | 4.5 MEDIUM | Medium | 9,1,1,7 / 情報漏えいのみ |
| CVE-2026-105134 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 |
| CVE-2026-105133 | 5.62 MEDIUM | 4.25 MEDIUM | Medium | 2,3,5,7（C/I/A=Low換算）。ただし105134と連鎖で実質リスク上昇 |
| CVE-2026-76519 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 |
| CVE-2026-0322 | 5.0 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 要認証 |
| CVE-2026-106931 | 4.75 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / ローカル攻撃 |

### ③ OWASP Top 10:2025 対応（推定・CWE→カテゴリ）

Top 10はWebアプリ向け分類。無いものは「対象外」とし、無理に当てはめない。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-102764 | CWE-290（なりすましによる認証回避） | 対象外（公式Mapped CWEの掲載を今回確認できず。意味的にはA07近傍） |
| CVE-2025-61624 | CWE-22 | A01 Broken Access Control |
| CVE-2026-21589 | CWE-552 | 対象外（掲載を今回確認できず。意味的にはA01近傍） |
| CVE-2026-105134 | CWE-77（NVD）/ CWE-78（CISA） | A05 Injection |
| CVE-2026-105133 | CWE-287 | A07 Authentication Failures |
| CVE-2026-76519 | CWE-23 | A01 Broken Access Control（CWE-22の関連として推定） |
| CVE-2026-0322 | CWE-94 | A05 Injection |
| CVE-2026-106931 | CWE-78 | A05 Injection |

### ④ 今週の優先度の所見

- 最優先: **CVE-2026-102764（BeyondTrust）**。CVSS 9.8、未認証・遠隔、CISAが個別Alertで注意喚起。
- 次点: **AhsayCBS 2件（105133＋105134）**。連鎖で認証回避→OS命令実行となり実質は重大（CVSSは2件ともCNA採点）。**Cisco Secure Email Gateway（9.8）**も未認証で到達しうる。
- CVSSとOWASP推定は意味が異なり、単純な大小比較はしない。

## 🛰 CISAアドバイザリ

計16件: ICS(産業制御) 8 / ICS Medical 2 / Alert 4 / Advisory 2。出典: [CISA RSS](https://www.cisa.gov/cybersecurity-advisories/all.xml)

- **Alert**: KEV追加通知3件（10/14: 4件、10/15: 1件、10/16: 2件）、およびBeyondTrust Remote Supportの重大脆弱性への対応要請（10/16）。
- **Advisory**: 選挙・選挙運動関係者を狙う攻撃者の手口の解説、および「超知能（Super Intelligence）」の訓練・評価におけるインシデント対応の実践指針。
- **ICS（Industrial Control Systems＝産業制御システム）8件**: HMS Networks PEAK-System PCANドライバ、WAGO OS、Hitachi Energy（RTU500、MicroSCADA X SYS600）、Moxa（AIG-302 ThingsPro Edge）、Eclipse Foundation Eclipse Milo、Guangzhou Juan IoT EseeCloud、CISA Malcolm。
- **ICS Medical 2件**: J4Care dcm4che、Thermo Fisher Torrent Suite。

## 🇯🇵 JPCERT/CC 注意喚起

注意喚起（at）**2件**、Weekly Report項目18件（計20件）。出典: [JPCERT/CC RSS](https://www.jpcert.or.jp/rss/jpcert.rdf)

- [at260032](https://www.jpcert.or.jp/at/2026/at260032.html)（新規 10/14）: SiteGuard Server Edition のOSコマンドインジェクション（CVE-2026-106931、CVSS 7.8 v3.0 / Secondary、OWASP推定 High、Top10: A05）。
- [at260031](https://www.jpcert.or.jp/at/2026/at260031.html)（新規 10/14）: 2026年10月マイクロソフトセキュリティ更新プログラム。CVE個別はフィードに記載なし（未採点）。
- **Weekly Report（[wr261015](https://www.jpcert.or.jp/wr/2026/wr261015.html)）**: Drupal、Splunk、Cisco、Movable Type、Elastic、Veeam、WordPress、Chrome、SonicWall、Atlassian、Microsoft、MikroTik RouterOS、Citrix NetScaler、GitLab AI Gateway等の脆弱性情報と、国内組織での不正アクセス相次ぐ旨の注意喚起を掲載。

## ✅ 今週の対応の優先度（所見）

1. インターネットに公開している BeyondTrust / Cisco Secure Email Gateway / PAN-OS / FortiOS / AhsayCBS / Atlassian Data Center の利用有無とバージョンを確認し、ベンダー情報に従い修正・緩和を適用。KEVの期限は既に過ぎているため早急に。
2. Microsoft月例更新（JPCERT at260031）と、SiteGuard Server Editionの該当確認。
3. 管理画面・管理用CLIの公開範囲と、侵害有無（ログ・不審ファイル）の確認。

## 取得できなかった情報源

なし（3フィードとも取得成功）。

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
