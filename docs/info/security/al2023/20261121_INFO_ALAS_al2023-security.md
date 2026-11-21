# AL2023 セキュリティアドバイザリ週次レポート（2026-11-21）

作成日: 2026-11-21 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 4 |
| Important | 40 |
| Medium | 8 |
| Low | 0 |

対象期間: 2026-11-14 〜 2026-11-21（新規 計52件）

> ⚠️ reportable（Critical+Important）44件のうち、詳細取得には上限があり、先頭30件のみ詳細を取得しています（`reportableTruncated=true`）。残り14件は未取得です。

---

## 注目アドバイザリ（重大度順）

### 1. PHP 一式（Critical・4件）
- ALAS: [ALAS2023-2026-3504](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3504.html)（php8.2）／[3505](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3505.html)（php8.3）／[3506](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3506.html)（php8.5）／[3507](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3507.html)（php8.4）
- **重大度:** Critical（緊急）
- **関連 CVE:** 各版 13〜19件（共通: CVE-2026-115560, CVE-2026-126714, CVE-2026-127960, CVE-2026-128064, CVE-2026-128090, CVE-2026-129289 ほか）
- **概要:** PHP のセッションアップロード進捗機能が、ある形式で書いた攻撃者制御データを別形式で読み戻すため、デコーダ不一致により内容が誤解釈される（デシリアライズ＝データの復元処理の脆弱性、CVE-2026-115560）。ほか TOCTOU（チェック時と使用時の競合）の問題（CVE-2026-126714）など。

### 2. nginx（Important）
- [ALAS2023-2026-3494](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3494.html) / CVE-2026-113425 ほか9件
- メールプロキシ構成の nginx で、特定のトラフィックにより use-after-free（解放済みメモリの再利用）が起き、条件次第でコード実行の恐れ。

### 3. Mozilla 系ライブラリ（firefox 名義・Important）
- [ALAS2023-2026-3508](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3508.html)（CVE 85件、概要は libexpat の DoS：エンティティ増幅＝billion laughs の検知遅れ）

### 4. Ruby（Important・3件）
- [3509](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3509.html)（ruby3.4）／[3510](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3510.html)（ruby4.0）／[3511](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3511.html)（ruby3.2）/ CVE-2026-132825
- 大文字小文字変換時にヒープバッファオーバーフロー（1バイトの範囲外書き込み）。

### 5. PostgreSQL（Important・4件）
- [3482](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3482.html)（18）／[3485](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3485.html)（17）／[3486](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3486.html)（16）／[3487](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3487.html)（15）。CVE 42〜54件
- 型変換で、EXECUTE 権限が無いユーザでもキャスト関数を実行できる認可漏れ（CVE-2026-116303 ほか）。

### 6. その他の Important（詳細取得済み分）
- python-oauthlib（[3483](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3483.html)）、python-tornado（[3484](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3484.html)）、tomcat11（[3488](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3488.html)、JNDI realm の認証不備）、ImageMagick（[3490](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3490.html)、CVE 63件）、gstreamer1-plugins-base（[3491](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3491.html)）、gstreamer1（[3492](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3492.html)）、python-dulwich（[3495](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3495.html)）、aws-nitro-enclaves-cli（[3496](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3496.html)）、java-1.8.0 / java-11 amazon-corretto（[3497](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3497.html)・[3498](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3498.html)）、aardvark-dns（[3499](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3499.html)）、libfontenc（[3500](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3500.html)）、swiftlang（[3502](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3502.html)）、rclone（[3503](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3503.html)）、ghostscript（[3460](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3460.html)）、rsync（[3462](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3462.html)）、runfinch-finch（[3464](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3464.html)）

### 対処方法
`sudo dnf check-release-update` で新リリースの有無を確認し、`sudo dnf update <パッケージ名>`（例: `sudo dnf update php8.3`）で更新します（AWS公式 ALAS の案内に準拠）。これらは sudo（管理者権限）が必要なため、本タスクでは実行していません。適用は管理者権限を持つ方が実施してください。

出典: https://alas.aws.amazon.com/alas2023.html

---

## 🎯 CVSS・OWASPスコア

> 📌 **読み方の注意:** 「Critical / Important」は Amazon Linux 独自の重大度ラベルで、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム：0.0〜10.0）とは**別物**です。CVE が1パッケージあたり数十〜数百あるため、**各アドバイザリの代表CVE**でスコアを示します（全CVEは各ALASページ参照）。CVSS は NVD API から取得した公式値、OWASP は推定値です。**v3.1 と v4.0 は数値が比較できません。**

### ① CVSS（NVD公式値）

| 代表CVE | 対象 / 概要 | CVSS | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-115560 | PHP / セッション復元の不整合（デシリアライズ） | **9.2** (v4.0) | CRITICAL | Secondary（CNA: PHP） | `AV:N/AC:H/AT:P/PR:N/UI:N/VC:H/VI:H/VA:H` |
| CVE-2026-126714 | PHP / TOCTOU競合 | **9.2** (v4.0) | CRITICAL | Secondary（CNA: PHP） | `AV:N/AC:L/AT:P/PR:N/UI:N/VC:H/VI:H/VA:H` |
| CVE-2026-113425 | nginx / メールプロキシのUAF | **8.1** (v3.1) / 9.2 (v4.0) | HIGH / CRITICAL | Secondary（CNA: F5） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-132825 | Ruby / ヒープバッファオーバーフロー | **7.4** (v3.1) | HIGH | Secondary（CNA: MITRE） | `AV:L/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-103119 | Tomcat / 範囲外読み取り | **9.1** (v3.1) | CRITICAL | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:H` |
| CVE-2026-116303 | PostgreSQL / 認可漏れ(キャスト関数) | **3.1** (v3.1) | LOW | Secondary（CNA） | `AV:N/AC:H/PR:L/UI:N/S:U/C:L/I:N/A:N` |
| CVE-2026-118669 | python-oauthlib / 認可の誤り | **8.4** (v4.0) | HIGH | Secondary（CNA: GitHub） | `AV:N/AC:L/AT:N/PR:L/UI:N/VC:N/VI:H/VA:N/SC:H/SI:H` |
| CVE-2026-115927 | python-tornado / チャンク処理のDoS | **5.3** (v3.1) | MEDIUM | Secondary（CNA: GitHub） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:L` |
| CVE-2026-102635 | ImageMagick / 未初期化メモリ開示 | **5.3** (v3.1) | MEDIUM | **Primary（NVD採点）**（CNA値は3.7 LOW） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N` |
| CVE-2026-125704 | gstreamer1 / use-after-free | **7.5** (v3.1) | HIGH | Secondary（CNA: Red Hat） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-122299 | python-dulwich / コミット解析の不整合 | **8.8** (v3.1) / 8.6 (v4.0) | HIGH | Secondary（CNA: VulnCheck） | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-109908 | libfontenc / ヒープ範囲外書き込み | **7.8** (v3.1) | HIGH | Secondary（CNA: SUSE） | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-119741 | rsync / DoS | **7.5** (v3.1) / 8.7 (v4.0) | HIGH | Secondary（CNA: VulnCheck） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-110133 | ghostscript / ヒープ溢れ | **5.8** (v3.1) | MEDIUM | Secondary（CNA: Red Hat） | `AV:L/AC:L/PR:H/UI:R/S:U/C:H/I:H/A:N` |

- 上記以外の CVE（firefox 85件、postgresql の残り、ImageMagick の残り等）は今回**未取得**（NVDのレート制限と件数の多さのため）。数値の創作はしていません。
- `AV:N`＝ネットワーク経由で攻撃可、`AV:L`＝端末上での操作が必要、`PR`＝必要権限、`AC:H`＝攻撃条件が難しい。v4.0 の `AT:P`＝攻撃に前提条件あり。
- NVD自身の採点（Primary）が付いていたのは CVE-2026-102635 のみで、他は発行元（CNA）採点です。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology（尤度＝起きやすさ × 影響度、0〜9）。公式値は存在せず、**公開情報から私が見積もった推定値**です。業務影響（ビジネス）は環境依存のため採点せず、技術面のみで評価しています。

| 代表CVE | 尤度 | 影響度 | 総合（推定） | 根拠 |
|---|---|---|---|---|
| CVE-2026-115560（PHP） | 5.38 MEDIUM | 6.5 HIGH | **High** | 外部公開のWebで広く使われ、機密性・完全性への被害が大。攻撃には前提条件あり |
| CVE-2026-113425（nginx） | 5.38 MEDIUM | 7.0 HIGH | **High** | コード実行の恐れ。ただしメールプロキシ構成のみ |
| CVE-2026-132825（Ruby） | 4.62 MEDIUM | 6.0 HIGH | **High** | 1バイト書き込み。悪用は難しい |
| CVE-2026-109908（libfontenc） | 4.5 MEDIUM | 7.0 HIGH | **High** | ローカル権限が前提 |
| CVE-2026-122299（dulwich） | 4.5 MEDIUM | 6.5 HIGH | **High** | 悪意あるリポジトリを扱わせる必要 |
| CVE-2026-103119（Tomcat） | 5.0 MEDIUM | 5.0 MEDIUM | **Medium** | JNDI SASL構成のみ該当 |
| CVE-2026-118669（oauthlib） | 5.0 MEDIUM | 5.25 MEDIUM | **Medium** | 認可の誤りだが特定ハンドラ限定 |
| CVE-2026-125704（gstreamer1） | 5.0 MEDIUM | 4.0 MEDIUM | **Medium** | 主に可用性への影響 |
| CVE-2026-119741（rsync） | 5.62 MEDIUM | 4.0 MEDIUM | **Medium** | 可用性（DoS）のみ |
| CVE-2026-115927（tornado） | 5.25 MEDIUM | 3.5 MEDIUM | **Medium** | DoSのみ |
| CVE-2026-116303（PostgreSQL） | 4.5 MEDIUM | 3.75 MEDIUM | **Medium** | DBユーザ権限が前提、機密性への軽微な影響 |

### ③ OWASP Top 10:2025 との対応

Top 10 は **Webアプリ向け**の分類です。NVDのCWE（弱点の種類）を元に当てはめました。公式ページとの個別照合は今回行っておらず、**既知の対応（CWE-862/863/367→A01、CWE-502→A08）による暫定対応**です。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-115560（PHP） | CWE-20, CWE-502 | A08 Software or Data Integrity Failures（暫定）※CWE-20は対象外扱い |
| CVE-2026-126714（PHP） | CWE-367, CWE-662 | A01 Broken Access Control（暫定、CWE-367） |
| CVE-2026-116303（PostgreSQL） | CWE-862 | A01 Broken Access Control |
| CVE-2026-118669（oauthlib） | CWE-863 | A01 Broken Access Control |
| CVE-2026-113425 / 132825 / 109908 / 110133 / 125704（メモリ破壊系 CWE-416/122） | CWE-416, CWE-122 | 対象外（メモリ安全性の問題でWebアプリ向け分類に該当しない） |
| CVE-2026-103119（Tomcat） | CWE-127 | 対象外 |
| CVE-2026-115927（tornado） | CWE-400, CWE-770 | 対象外 |
| CVE-2026-119741（rsync） | CWE-407 | 対象外 |
| CVE-2026-102635（ImageMagick） | CWE-908 | 対象外 |
| CVE-2026-122299（dulwich） | CWE-115, CWE-1250 | 対象外（未照合） |

### 今週の優先度（所見）

1. **最優先: PHP 一式（Critical・CVSS v4.0 9.2）** — Webサーバで広く使う上、デシリアライズ系で影響大。PHPを稼働させている環境は早めに更新。
2. **nginx（v3.1 8.1）** — メールプロキシ機能を使っている場合のみ該当。HTTPのみなら影響は限定的。
3. **PostgreSQL / Ruby / Tomcat** — 件数は多いが、代表CVEは前提条件（特定構成・ローカル権限）が必要。Tomcat は JNDI realm+SASL利用時のみ。
4. Critical と付いても **v3.1 と v4.0 の数値は直接比較できない**点に注意。

> 📚 出典: NVD API（https://nvd.nist.gov/）、AWS ALAS（https://alas.aws.amazon.com/alas2023.html）、OWASP Risk Rating Methodology（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）

---

## その他

- Medium: 8件 / Low: 0件（件数のみ記録。例: amazon-ecr-credential-helper, gstreamer1-plugins-bad-free, libXfont2 ほか）
- 一覧の切り詰め（truncated）: あり。詳細取得は先頭30件まで。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
