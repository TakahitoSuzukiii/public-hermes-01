作成日: 2026-11-11 / STATUS: INFO / TOPIC: CISAJPCERT / 対象期間: 2026-11-04〜2026-11-11

# CISA・JPCERT/CC 週報（2026-11-11）

## 📌 今週の要点

- **CISA KEV（Known Exploited Vulnerabilities＝悪用が確認された脆弱性）の新規は6件**。うち4件は11/9追加で、対処期限が11/12と非常に短い。
- **ランサムウェア悪用の確認は今週なし**（6件とも「Unknown＝不明」）。
- 認証回避系が目立つ：OpenSSH（Linux）、SonicWall SSLVPN（MFA回避）、GPUStack（認証なしで管理者操作）。
- 日本国内向けのJPCERT/CC注意喚起は、Weekly Report（週次まとめ）の1号（15項目）のみ。個別の緊急注意喚起（at始まり）は今週なし。Brotli（圧縮ライブラリ）の脆弱性に注意。

## 🔥 CISA KEV（悪用が確認された脆弱性）

新規件数：**6件**（カタログ総数1,773件、版 2026.11.09）

| CVE | ベンダー | 製品 | 追加日 | 対処期限 | ランサム悪用 | 概要（要約） |
|---|---|---|---|---|---|---|
| [CVE-2026-102895](https://nvd.nist.gov/vuln/detail/CVE-2026-102895) | GPUStack | GPUStack | 11/9 | 11/12 | Unknown | 認証不備により、未認証で管理者操作・APIキー作成・秘密情報の漏えい・コード実行が可能 |
| [CVE-2026-123158](https://nvd.nist.gov/vuln/detail/CVE-2026-123158) | OpenBSD | OpenSSH（Linux） | 11/9 | 11/12 | Unknown | 想定外の戻り値の扱いにより認証を回避できる可能性 |
| [CVE-2026-116779](https://nvd.nist.gov/vuln/detail/CVE-2026-116779) | SignalWire | FreeSwitch | 11/9 | 11/12 | Unknown | コードインジェクションにより設定・認証情報の漏えい、通話制御の乗っ取り、コマンド実行が可能 |
| [CVE-2026-123218](https://nvd.nist.gov/vuln/detail/CVE-2026-123218) | IBM | Aspera Faspex | 11/9 | 11/12 | Unknown | 認証済みユーザーが細工したメッセージで認可を回避し、権限昇格できる |
| [CVE-2026-19868](https://nvd.nist.gov/vuln/detail/CVE-2026-19868) | SonicWall | SonicOS SSLVPN | 11/6 | 11/20 | Unknown | 別方式の有効な認証情報があれば、SAML認証（MFA含む）を回避できる |
| [CVE-2024-27834](https://nvd.nist.gov/vuln/detail/CVE-2024-27834) | Apple | iOS/macOS等 複数 | 11/4 | 11/18 | Unknown | 任意の読み書き能力を持つ攻撃者がポインタ認証（PAC）を回避できる |

> 対処期限（dueDate）は米国連邦機関向けの期限だが、一般の組織でも優先度の目安になる。

## 🎯 CVSS・OWASPスコア

> **読み方の注意:** CVSS（共通脆弱性評価システム、0.0〜10.0）、OWASP Risk Rating（尤度×影響度の0〜9評価）、OWASP Top 10（Webアプリ向けリスク分類）は**別物の尺度**で、数値の大小は直接比較しない。KEVやJPCERTの見出し・重大度ラベルもCVSSではない。
> 取得状況：下記7件すべてNVD APIから取得済み（未取得0件）。20件上限の範囲内。

### ① CVSS v3.1（公式値、NVD API取得）

| CVE | 概要 | スコア | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-102895 | GPUStack 認証不備 | 9.8 | CRITICAL | Secondary（CNA: GitHub系 security-advisories） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-123158 | OpenSSH 認証回避 | 8.1 | HIGH | Secondary（CNA: MITRE） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-116779 | FreeSwitch コード注入 | 9.8 | CRITICAL | Secondary（CNA: security-advisories） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-123218 | Aspera Faspex 認可不備 | 9.8 | CRITICAL | Secondary（CNA: IBM PSIRT） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-19868 | SonicOS SSLVPN MFA回避 | 7.5 | HIGH | Secondary（CNA） | `AV:N/AC:H/PR:N/UI:N/S:C/C:H/I:L/A:N` |
| CVE-2024-27834 | Apple PAC回避 | 5.5 | MEDIUM | **Primary（NVD）**（CNAも同値） | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:H/A:N` |
| CVE-2026-111497 | Brotli 境界外書き込み | 9.8 | CRITICAL | **Primary（NVD）** | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |

補足：CVE-2026-111497にはCNA（Google）の CVSS v4.0 = 9.2 CRITICAL（Secondary）もあるが、v3.1とは比較不能のため上表はv3.1を掲載。

### ② OWASP Risk Rating（推定・技術影響ベース、業務影響は環境依存のため採点せず）

| CVE | 尤度 | 影響度 | 総合（推定） | 根拠（要因値） |
|---|---|---|---|---|
| CVE-2026-102895 | 7.12 HIGH | 8.0 HIGH | **Critical** | 未認証・悪用確認済み（opportunity 9, exploit 9）、機密/完全性9 |
| CVE-2026-123158 | 5.62 MEDIUM | 6.5 HIGH | **High** | 攻撃条件が高い（AC:H）ため発見・悪用難度は中程度 |
| CVE-2026-116779 | 7.12 HIGH | 8.0 HIGH | **Critical** | 外部から到達可能・コマンド実行（悪用確認済み） |
| CVE-2026-123218 | 5.88 MEDIUM | 6.5 HIGH | **High** | 認証済みユーザーが前提（opportunity 7）、権限昇格 |
| CVE-2026-19868 | 5.25 MEDIUM | 4.25 MEDIUM | **Medium** | 有効な認証情報が前提、影響は機密性中心 |
| CVE-2024-27834 | 4.5 MEDIUM | 5.25 MEDIUM | **Medium** | ローカル前提・他の脆弱性との連鎖が必要（完全性のみ） |
| CVE-2026-111497 | 5.62 MEDIUM | 8.0 HIGH | **High** | ライブラリ脆弱性で到達条件は利用側に依存、影響は大 |

### ③ OWASP Top 10:2025 対応

| CVE | CWE | カテゴリ |
|---|---|---|
| CVE-2026-102895 | CWE-287/290/346 | A07 Authentication Failures（認証の不備） |
| CVE-2026-123158 | CWE-394 | 対象外寄り（OpenSSHはWebアプリでない。強いて言えば A10 Mishandling of Exceptional Conditions、※推定） |
| CVE-2026-116779 | CWE-77/78/749 | A05 Injection（インジェクション） |
| CVE-2026-123218 | CWE-863 | A01 Broken Access Control（アクセス制御の不備） |
| CVE-2026-19868 | CWE-308 | A07 Authentication Failures |
| CVE-2024-27834 | CWE-287 | 対象外（OS/ブラウザ内部機構でWebアプリ向け分類のため） |
| CVE-2026-111497 | 今回CWE未確認 | 対象外（ライブラリのメモリ安全性問題のため） |

### ④ 今週の優先度の所見

- 最優先は **CVSS 9.8 かつ悪用確認済み**の GPUStack / FreeSwitch / Aspera Faspex（期限11/12）。ただしCVSSは理論上の深刻度で、「悪用が確認済み」というKEVの事実が優先度を押し上げる。
- OpenSSH（Linux）の認証回避はCVSSが8.1と相対的に低いが、SSHは広く公開されるため棚卸しの優先度は高い。
- SonicWall SSLVPNは「MFAを回避される」点が実害に直結しやすい。CVSS 7.5という数値以上に注意する。

## 🛰 CISAアドバイザリ

種別ごとの件数：Alert 3件 / Advisory 2件（Analysis Report・ICSは今週なし）

- **Alert**（KEV追加の通知）：[11/9 4件追加](https://www.cisa.gov/news-events/alerts/2026/11/09/cisa-adds-four-known-exploited-vulnerabilities-catalog) / [11/6 1件追加](https://www.cisa.gov/news-events/alerts/2026/11/06/cisa-adds-one-known-exploited-vulnerability-catalog) / [11/4 1件追加](https://www.cisa.gov/news-events/alerts/2026/11/04/cisa-adds-one-known-exploited-vulnerability-catalog)
- **Advisory**：
  - [Post-Quantum Questions to Ask Your Vendors](https://www.cisa.gov/resources-tools/resources/post-quantum-questions-ask-your-vendors)：量子コンピュータ時代の暗号移行について、ベンダーに確認すべき質問をまとめた資料。
  - [産業用冷凍・コールドチェーン監視システムの堅牢化](https://www.cisa.gov/resources-tools/resources/us-government-partners-urge-hardening-industrial-refrigeration-and-cold-chain-monitoring-systems)：米政府機関が連名で、冷凍・低温物流の監視システムの防御強化を促す資料。

## 🇯🇵 JPCERT/CC 注意喚起

- 対象期間のフィード項目は15件、すべて **Weekly Report（wr261105、11/5号）** の見出し。個別の緊急注意喚起（at始まり）は**0件**。
- Weekly Reportの主な項目：Microsoft Edge、Sophos UTM（任意コード実行）、Cisco Secure Firewall ASA/FTD（DoS）、Jenkins、WordPress、Adobe製品、ヤマハNWR100、WatchGuard、Veeam、Mozilla、Google Chrome、YOOtheme Pro（RCE）、Apple製品、Ruby ほか。
- 注目：**Brotli（C実装）の境界外書き込み（CVE-2026-111497）** に関する注意喚起が含まれる。Brotliは多くのソフトに組み込まれており、間接的に影響を受ける可能性がある。新規掲載（更新ではない）。
- 出典：https://www.jpcert.or.jp/wr/2026/wr261105.html

## ✅ 今週の対応の優先度（所見）

1. **11/12期限の4件**（GPUStack / OpenSSH / FreeSwitch / Aspera Faspex）：該当製品を使っているか資産を確認し、ベンダー指示の対処を適用。インターネットに公開されているかも併せて確認。
2. **VPN・認証系（SonicWall SSLVPN）**：対処後は、不審なログインがないかログを確認。
3. **Brotliなど組み込み型ライブラリ**：自社製品・コンテナ・依存関係（SBOM等）に含まれていないか確認し、修正版への更新計画を立てる。

## 取得できなかった情報源

なし（3フィードとも取得成功）。

## 出典

- CISA KEV JSON: https://www.cisa.gov/sites/default/files/feeds/known_exploited_vulnerabilities.json
- CISA アドバイザリRSS: https://www.cisa.gov/cybersecurity-advisories/all.xml
- JPCERT/CC RSS: https://www.jpcert.or.jp/rss/jpcert.rdf
- NVD API: https://services.nvd.nist.gov/rest/json/cves/2.0

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
