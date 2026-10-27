作成日: 2026-10-28 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-10-21〜2026-10-28

# CISA・JPCERT/CC 週報（2026-10-21〜2026-10-28）

## 📌 今週の要点

- **KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は4件**（カタログ総数1758件）。ランサムウェア悪用の記載は**なし**（全件 Unknown）。
- 対象は **PHP本体（2件）**、**Arista VeloCloud Orchestrator**（SQLインジェクション）、**Collabora Online Built-in CODE Server**（OSコマンドインジェクション）。PHPの2件は未認証でのリモートコード実行（RCE）で、CISAが個別Alertでも即時パッチ適用を求めている。
- 日本国内向けには、JPCERT/CCが **PHP（at260033、更新）**、**Brotli C実装の境界外書き込み（at260034、新規）**、**国内組織への不正アクセス相次ぐ件（at260030、更新）** の注意喚起を出している。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規 **4件**。出典: [CISA KEV JSON](https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json)

| CVE | ベンダー/製品 | 追加日 | 対処期限 | ランサム悪用 | 概要（要約） |
|---|---|---|---|---|---|
| [CVE-2026-109618](https://nvd.nist.gov/vuln/detail/CVE-2026-109618) | PHP Group / PHP | 10-26 | 10-29 | Unknown | メモリ不足に起因するメモリ破壊。未認証でリモートコード実行が可能 |
| [CVE-2026-109619](https://nvd.nist.gov/vuln/detail/CVE-2026-109619) | PHP Group / PHP | 10-26 | 10-29 | Unknown | 内部リクエスト状態が古いまま残る不具合。未認証でリモートコード実行が可能 |
| [CVE-2026-114625](https://nvd.nist.gov/vuln/detail/CVE-2026-114625) | Arista / VeloCloud Orchestrator（オンプレ版） | 10-23 | 10-26 | Unknown | SQLインジェクション。内部の特権機能へ到達しホストに影響し得る |
| [CVE-2026-110447](https://nvd.nist.gov/vuln/detail/CVE-2026-110447) | Collabora / Collabora Online Built-in CODE Server（Nextcloud利用時） | 10-23 | 10-26 | Unknown | OSコマンドインジェクション。CODEサーバ非稼働時にリモートコード実行が可能 |

> 注: 対処期限（dueDate）は米国連邦機関向けの期限だが、一般の組織でも優先度の目安になる。

## 🎯 CVSS・OWASPスコア

採点対象はKEV新規4件＋JPCERT注意喚起の1件（CVE-2026-111497）の計5件（上限20件以内）。KEV/JPCERT/CISAの見出し・ラベルはCVSSではない。CISAアドバイザリ（ICS）掲載CVEは今回**未採点**。

### ① CVSS（共通脆弱性評価システム）公式値（NVD API取得）

Primary=NVD自身の採点、Secondary=CNA（CVE採番組織）の採点。版（v3.1/v4.0）の違う値は比較不能。

| CVE | CVSS | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|
| CVE-2026-109618 | 9.8 (v3.1) | CRITICAL | Primary (NVD) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-109619 | 8.1 (v3.1) | HIGH | Primary (NVD) | AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-114625 | 9.9 (v3.1) | CRITICAL | Secondary (Arista PSIRT) | AV:N/AC:L/PR:L/UI:N/S:C/C:H/I:H/A:H |
| CVE-2026-110447 | 9.8 (v3.1) | CRITICAL | Primary (NVD) | AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H |
| CVE-2026-111497（JPCERT） | v3.1 未取得（NVD: Awaiting Analysis、v3.1の掲載なし） | － | － | v4.0のみ（下記） |

補足: v4.0の値（参考・v3.1と比較不可、全てSecondary）— CVE-2026-109618/109619: 9.2（PHP）/ CVE-2026-114625: 9.4（Arista）/ CVE-2026-110447: 9.2（MITRE）/ CVE-2026-111497: 9.2 CRITICAL（Google）。

### ② OWASP Risk Rating（尤度×影響度）— **すべて推定**

CVSSベクタから機械換算（skill=5, motive=4, size=6, discovery=7, exploit=5, awareness=6, detection=3、追跡可能性=7を固定。未認証・遠隔→opportunity=9、低権限が必要→7）。KEV掲載は悪用実績ありだが換算値は固定のまま。業務影響は環境依存のため採点せず、技術ベースの推定。

| CVE | 尤度 | 影響度 | 総合(推定) | 根拠（機密性,完全性,可用性,追跡性） |
|---|---|---|---|---|
| CVE-2026-109618 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 未認証・遠隔 |
| CVE-2026-109619 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 未認証だが攻撃条件が複雑（AC:H）。尤度は上限寄りの見積り |
| CVE-2026-114625 | 5.38 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 低権限が必要 |
| CVE-2026-110447 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / 未認証・遠隔 |
| CVE-2026-111497 | 5.62 MEDIUM | 8.5 HIGH | High | 9,9,9,7 / v4.0ベクタ（AV:N/PR:N）とNVD説明文から換算。v3.1未取得のため参考値 |

### ③ OWASP Top 10:2025 対応（推定・CWE→カテゴリ）

Top 10はWebアプリ向け分類。無いものは「対象外」とし、無理に当てはめない。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-109618 / 109619 | CWE-416（解放後メモリ使用）ほか | 対象外（言語処理系のメモリ安全性の問題でWebアプリ向け分類の範囲外） |
| CVE-2026-114625 | CWE-89 | A05 Injection |
| CVE-2026-110447 | CWE-78 | A05 Injection |
| CVE-2026-111497 | CWE-787（境界外書き込み）/ CWE-252 | 対象外（ライブラリのメモリ安全性の問題） |

### ④ 今週の優先度の所見

- 最優先: **PHP（CVE-2026-109618、CVSS 9.8）**。未認証RCE、KEV対処期限は10/29、CISAが個別Alertでも即時パッチを要請。109619（8.1）も同時対応が前提。
- 次点: **Arista VeloCloud Orchestrator（9.9）** と **Collabora CODE Server（9.8）**。いずれも既に対処期限が過ぎている。
- Brotli（CVE-2026-111497）はKEV未掲載で公式v3.1が無い（NVD解析待ち）。ただしライブラリなので組込み製品の洗い出しが要る。
- CVSSとOWASP推定は意味が異なり、単純な大小比較はしない。

## 🛰 CISAアドバイザリ

計26件: ICS(産業制御) 20 / Alert 4 / Advisory 1 / ICS Medical 1。出典: [CISA RSS](https://www.cisa.gov/cybersecurity-advisories/all.xml)

- **Alert**: KEV追加通知3件（10/23: 1件×2、10/26: 2件）と、[PHPの重大な脆弱性にパッチ適用を求めるAlert](https://www.cisa.gov/news-events/alerts/2026/10/21/critical-vulnerabilities-php-require-immediate-patching)（10/21）。
- **Advisory**: 「[AIトークン消費の管理と運用レジリエンス](https://www.cisa.gov/resources-tools/resources/managing-ai-token-consumption-operational-resilience)」（10/22）。AI利用コストの暴走が事業継続に及ぼす影響への備えを説く資料。
- **ICS（Industrial Control Systems＝産業制御システム）20件**: 主要ベンダーはSiemens（17件）。ほかMitsubishi、EPICS、InterSystems、Kiloview各1件。
- **ICS Medical 1件**: 医療関連機器・ソフトに関する勧告。

## 🇯🇵 JPCERT/CC 注意喚起

注意喚起（at）**3件**、Weekly Report項目24件（計27件）。出典: [JPCERT/CC RSS](https://www.jpcert.or.jp/rss/jpcert.rdf)

- [at260034](https://www.jpcert.or.jp/at/2026/at260034.html)（新規 10/26）: Brotli C実装の境界外書き込み（CVE-2026-111497。CVSS v4.0 9.2 CRITICAL / Secondary、v3.1は未取得。OWASP推定 High、Top10: 対象外）。
- [at260033](https://www.jpcert.or.jp/at/2026/at260033.html)（更新 10/26）: PHPの複数の脆弱性（CVE-2026-109618、CVE-2026-109619。スコアは上記①②③）。KEV追加を受けた更新とみられる。
- [at260030](https://www.jpcert.or.jp/at/2026/at260030.html)（更新 10/23）: 直近で相次ぐ国内組織への不正アクセスに関する注意喚起。CVE個別記載なし（未採点）。
- **Weekly Report（wr261021）**: Microsoft（Edge含む）、Chrome、Mozilla、Adobe、Fortinet、Palo Alto、Ivanti Connect Secure、Cisco Secure Email Gateway、GitLab、Next.js、NGINX、Juniper、SAP、Zoom、Drupal等の脆弱性情報と、「連続不正アクセス事案の攻撃手法に関する調査」の公開を掲載。

## ✅ 今週の対応の優先度（所見）

1. PHPを利用する環境（Webサーバ・CMS・フレームワーク基盤）のバージョン確認と、ベンダー/配布元の修正版への更新。KEV期限は10/29。
2. Arista VeloCloud Orchestrator（オンプレ）および Nextcloud＋Collabora CODE Server の利用有無確認と修正適用。管理画面の公開範囲の見直し。
3. Brotliを組み込む製品・ライブラリ（バンドル含む）の洗い出しと、各ベンダーの対応情報の確認。

## 取得できなかった情報源

なし（3フィードとも取得成功）。NVDでCVE-2026-111497はv3.1未掲載（解析待ち）。

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
