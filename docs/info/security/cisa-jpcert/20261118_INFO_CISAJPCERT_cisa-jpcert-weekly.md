作成日: 2026-11-18 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-11-11〜2026-11-18

# CISA・JPCERT/CC 週報（2026-11-18）

## 📌 今週の要点

- **CISA KEV**（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規追加は **2件**（UnrealIRCd、Check Point）。カタログ総数は1,781件。
- **ランサムウェア悪用**の確認は **なし**（2件とも「Unknown＝不明」）。
- JPCERT/CC の **注意喚起は1件**（2026年11月マイクロソフトセキュリティ更新プログラム）。他に Weekly Report（週次まとめ）が1本。
- CISAアドバイザリは17件（ICS＝Industrial Control Systems＝産業制御システム向けが16件、Siemens製品が中心）。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規追加: **2件**（追加日はいずれも 2026-11-13）

| CVE | ベンダー | 製品 | 追加日 | 対処期限 | ランサムウェア悪用 | 概要（要約） |
|---|---|---|---|---|---|---|
| [CVE-2026-114713](https://nvd.nist.gov/vuln/detail/CVE-2026-114713) | UnrealIRCd | UnrealIRCd | 2026-11-13 | 2026-11-16 | Unknown（不明） | IRCサーバ。labeled-responseモジュールがメッセージタグを無害化せず、2台以上のサーバが連携する環境で任意のユーザがサーバ間コマンドを注入し、サーバ権限で実行させられる（6.2.7.1未満が対象） |
| [CVE-2026-123039](https://nvd.nist.gov/vuln/detail/CVE-2026-123039) | Check Point | Multiple Products（Firewall / Security Gateway / Management Server 等） | 2026-11-13 | 2026-11-16 | Unknown（不明） | Gaia OSのDynamicCLIデーモンがroot権限で動作し、誰でも書き込める（world-writable）ローカルソケットを認証なしで待ち受け。認証済みローカルユーザがroot権限でコマンドを実行できる |

> ※対処期限（dueDate）は **米国連邦機関向けの期限** だが、一般の組織でも優先度の目安になる。今回は両件とも期限（11-16）が既に過ぎている。

## 🎯 CVSS・OWASPスコア

> 📌 KEVやJPCERTの見出し・重大度ラベルは **CVSSではなく別物** です。CVSS（Common Vulnerability Scoring System＝共通脆弱性評価システム、0.0〜10.0）は NVD（米国の脆弱性DB）の **v3.1** 公式値。出所の *Primary* は NVD自身の採点、*Secondary* は発行元(CNA)の採点です。

### ① CVSS v3.1（公式値）

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-114713 | UnrealIRCd サーバ間コマンド注入 | **7.7** | HIGH | Primary（NVD） | `AV:N/AC:L/PR:L/UI:N/S:C/C:N/I:H/A:N` |
| CVE-2026-114713 | 同上 | **8.6** | HIGH | Secondary（CNA: MITRE） | `AV:N/AC:L/PR:N/UI:N/S:C/C:N/I:H/A:N` |
| CVE-2026-123039 | Check Point Gaia OS 権限昇格 | **7.8** | HIGH | Secondary（CNA: Check Point） | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |

- CVE-2026-123039 はNVD自身（Primary）の採点が **今回の取得時点では未掲載**。上記はCNAの値のみ。
- 今週の対象は KEV新規2件のみ（JPCERT注意喚起にCVE番号の記載なし、ICSアドバイザリのCVEは上限内で採点せず＝**今回は未採点**）。

### ② OWASP Risk Rating（推定）

「起きやすさ（尤度）×被害の大きさ（影響度）」を0〜9で評価（LOW<3 / MEDIUM 3〜<6 / HIGH 6〜9）。**公式値ではなく技術面のみの推定**（業務影響は未採点）。

| CVE | 尤度 | 影響度 | 総合（推定） | 根拠 |
|---|---|---|---|---|
| CVE-2026-114713 | 6.38 HIGH | 5.25 MEDIUM | **High** | ネットワーク経由・低難度で悪用実績あり。ただし複数サーバ連携環境が前提で、影響は完全性（命令実行）が中心 |
| CVE-2026-123039 | 5.38 MEDIUM | 7.0 HIGH | **High** | ローカル認証済みユーザが前提で尤度は中程度。成功時はroot権限で影響大 |

### ③ OWASP Top 10:2025 対応

| CVE | CWE | カテゴリ |
|---|---|---|
| CVE-2026-114713 | CWE-140（区切り文字の不適切な無害化） | A05 Injection（推定。インジェクション系だがWebアプリ以外のため参考扱い） |
| CVE-2026-123039 | CWE-732（重要リソースへの不適切な権限付与）/ CWE-862（認可の欠如） | A01 Broken Access Control（推定。OS製品のため参考扱い） |

※Top 10はWebアプリ向け分類のため、ファイアウォールOSやIRCサーバへの当てはめは目安です。

### ④ 今週の優先度の所見

- 両件とも **悪用確認済み（KEV）** のため、スコアの大小より「該当製品を使っているか」の確認が先。
- CVSSは推定の尤度と一致せず（片方はネットワーク型、片方はローカル型）、数値の単純比較は不可。Check Pointは境界防御機器でroot奪取に繋がるため、実質的な重みは大きい。

## 🛰 CISAアドバイザリ

合計17件 / 内訳: ICS（産業制御）16件、Alert 1件。Advisory・Analysis Reportは今週なし。

- **Alert:** 「CISA Adds Two Known Exploited Vulnerabilities to Catalog」— 上記KEV2件の追加告知。（[リンク](https://www.cisa.gov/news-events/alerts/2026/11/13/cisa-adds-two-known-exploited-vulnerabilities-catalog)）
- **ICS（16件）:** Siemens製品が15件（Mendix Studio Pro、SIMATIC、WinCC、RUGGEDCOM APE1808、Desigo、Industrial Edge Management など）、Dorsett Controls（InfoScan）が1件。

## 🇯🇵 JPCERT/CC 注意喚起

- **注意喚起（at260035）:** 2026年11月マイクロソフトセキュリティ更新プログラムに関する注意喚起（**新規公開**、2026-11-11）。Windows・Office等の月例更新の適用を促す内容。CVE番号はフィード上に記載なし。 https://www.jpcert.or.jp/at/2026/at260035.html
- **Weekly Report（wr261111、1本）:** XenServer、Puppet Server/OpenVox、Airbyte、Firefox、ManageEngine、Zyxel、Microsoft Edge、Absolute Security、Elastic、Google Chrome、Android、Barracuda、PostgreSQL向けツール等の脆弱性情報をまとめて掲載。 https://www.jpcert.or.jp/wr/2026/wr261111.html

## ✅ 今週の対応の優先度（所見）

1. **KEV該当の確認:** UnrealIRCd（6.2.7.1未満）、Check Point Gaia OS（Jumbo Hotfixが古い版）を利用していないか棚卸し。該当するなら各ベンダーの修正情報に従い対応。
2. **11月のMicrosoft月例更新:** JPCERT/CCが注意喚起。適用計画の確認を。
3. **ブラウザ・Android等の更新:** Weekly Reportに載った Chrome / Firefox / Edge / Android は一般利用者への影響が広いため、更新状況を確認。

## 出典

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリ RSS: https://www.cisa.gov/ （公式RSSフィード）
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0

取得できなかった情報源: なし

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
