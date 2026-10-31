# AL2023 セキュリティアドバイザリ週次レポート（2026-10-31）

作成日: 2026-10-31 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果です（現行環境は WSL/Ubuntu のため実運用対象ではありません）。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 0 |
| Important | 105 |
| Medium | 34 |
| Low | 1 |

対象期間: 2026-10-24 〜 2026-10-31

> 注意: reportable（Critical+Important）105件のうち、詳細取得（概要・CVE一覧）は先頭30件までです（truncated）。残り75件は件数のみの把握です。

---

## 注目アドバイザリ（詳細取得30件の一覧）

| ALAS ID | 対象パッケージ | 関連CVE数 |
|---|---|---|
| [ALAS2023-2026-3338](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3338.html) | emacs | 2 |
| [ALAS2023-2026-3340](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3340.html) | perl-Text-CSV_XS | 8 |
| [ALAS2023-2026-3350](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3350.html) | amazon-cloudwatch-agent | 4 |
| [ALAS2023-2026-3352](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3352.html) | perl-Cpanel-JSON-XS | 9 |
| [ALAS2023-2026-3353](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3353.html) | gstreamer1-plugins-good | 4 |
| [ALAS2023-2026-3357](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3357.html) | python-dns | 1 |
| [ALAS2023-2026-3365](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3365.html) | kernel | 1 |
| [ALAS2023-2026-3366](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3366.html) | dotnet10.0 | 24 |
| [ALAS2023-2026-3367](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3367.html) | dotnet8.0 | 25 |
| [ALAS2023-2026-3368](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3368.html) | java-27-amazon-corretto | 1 |
| [ALAS2023-2026-3369](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3369.html) | java-25-amazon-corretto | 1 |
| [ALAS2023-2026-3370](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3370.html) | java-21-amazon-corretto | 1 |
| [ALAS2023-2026-3371](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3371.html) | java-17-amazon-corretto | 1 |
| [ALAS2023-2026-3372](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3372.html) | java-11-amazon-corretto | 1 |
| [ALAS2023-2026-3373](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3373.html) | java-1.8.0-amazon-corretto | 1 |
| [ALAS2023-2026-3374](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3374.html) | dotnet9.0 | 2 |
| [ALAS2023-2026-3342](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3342.html) | freerdp | 4 |
| [ALAS2023NVIDIA-2026-314](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-314.html) | NVIDIA系(13パッケージ共通) | 80 |
| [ALAS2023NVIDIA-2026-315](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-315.html) | nvidia-kmod-common | 80 |
| [ALAS2023NVIDIA-2026-316](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-316.html) | cuda-drivers | 80 |
| [ALAS2023NVIDIA-2026-317](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-317.html) | kmod-nvidia-open-dkms | 80 |
| [ALAS2023NVIDIA-2026-318](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-318.html) | libnvidia-nscq | 80 |
| [ALAS2023NVIDIA-2026-319](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-319.html) | nvidia-fabricmanager | 80 |
| [ALAS2023NVIDIA-2026-320](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-320.html) | nvidia-modprobe | 80 |
| [ALAS2023NVIDIA-2026-321](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-321.html) | libnvsdm | 80 |
| [ALAS2023NVIDIA-2026-322](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-322.html) | kmod-nvidia-latest-dkms | 80 |
| [ALAS2023NVIDIA-2026-323](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-323.html) | nvidia-xconfig | 80 |
| [ALAS2023NVIDIA-2026-324](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-324.html) | nvidia-imex | 80 |
| [ALAS2023NVIDIA-2026-325](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-325.html) | nvlink5 | 80 |
| [ALAS2023NVIDIA-2026-326](https://alas.aws.amazon.com/AL2023/ALAS2023NVIDIA-2026-326.html) | nvidia-driver | 80 |

> **読み方:** 「Important」は Amazon Linux 独自の重大度ラベルで、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム）とは別物です。今週は Critical ラベルは 0 件ですが、CVSS 9.8 の CVE が複数含まれます。

### 主な内容

- **ALAS2023-2026-3365（kernel）:** Linux カーネルの IPv4 処理で、オプション情報（inet_opt / ireq_opt）の解放処理に関する修正（CVE-2026-98432）。
- **ALAS2023-2026-3353（gstreamer1-plugins-good）:** GStreamer（動画・音声処理フレームワーク）の rtpL16depay でヒープ（動的メモリ）バッファオーバーフロー、rtpsbcdepay で UAF（Use-After-Free、解放済みメモリの再利用）など4件。
- **ALAS2023-2026-3340 / 3352（Perl の Text::CSV_XS / Cpanel::JSON::XS）:** Perl の CSV・JSON 解析モジュールのメモリ枯渇・UAF・レコード分割など、計17件。
- **ALAS2023-2026-3366 / 3367 / 3374（dotnet 10.0 / 8.0 / 9.0）:** .NET / ASP.NET Core の多数の修正（DoS、コードインジェクション、デシリアライズ等）。dotnet8.0 は Brotli デコーダのバッファオーバーフロー（CVE-2026-111497）を含む。
- **ALAS2023-2026-3368〜3373（Corretto 各版）:** Oracle Java SE の脆弱性（CVE-2026-114820）。Corretto は Amazon 提供の OpenJDK ディストリビューション。
- **ALAS2023-2026-3350（amazon-cloudwatch-agent）:** 同梱の Go 標準ライブラリ由来の HTTP/2・証明書処理の修正など4件。
- **ALAS2023-2026-3342（freerdp）:** RDP クライアントの境界外読み取り・ヒープオーバーフロー等4件。
- **ALAS2023-2026-3338（emacs）:** TRAMP（Emacs のリモートファイル編集機能）経由の OS コマンドインジェクション2件。
- **ALAS2023NVIDIA-2026-314〜326（NVIDIA ドライバ系13パッケージ）:** 同一の NVIDIA セキュリティ情報（79 CVE）が各パッケージに共通して紐付く。

### 対処方法

- `sudo dnf check-release-update` でリリース更新を確認し、`sudo dnf update <パッケージ名>`（例: `sudo dnf update kernel`）で更新します。
- 本タスクは情報収集のみで、`sudo`（管理者権限）が必要なコマンドは**実行していません**。
- 出典: https://alas.aws.amazon.com/AL2023/ （各 ALAS ID のページ）

---

## 🎯 CVSS・OWASPスコア

> **読み方の注意:** CVSS（共通脆弱性評価システム、0.0〜10.0）、OWASP Risk Rating（尤度×影響度の0〜9評価）、OWASP Top 10（Webアプリ向けリスク分類）は**別物の尺度**で、数値の大小を直接比較しません。ALAS の Critical/Important ラベルも別物です。
>
> **取得範囲:** 詳細取得30件に紐付く重複除外140 CVE の全件で NVD API から CVSS を取得できました（未取得0件）。表では同一パッケージで **同一スコア・同一ベクタ・同一CWE** の CVE をまとめ、CVE 番号は接頭辞 `CVE-2026-` を省略して列挙しています（例: 110753 = CVE-2026-110753）。
>
> **採点者:** CVE-2026-111497 のみ NVD 自身の採点（Primary）、それ以外は発行元 CNA（CVE Numbering Authority、CVE採番機関）の採点（Secondary）です。CVE-2026-111183 / 18299 は CVSS v3.0 の値です（表で明記）。CVE-2026-114043 には CVSS v4.0 の 7.1（Secondary）もありますが、v3.1 とは比較不能のため本表は v3.1 の 6.5 を掲載しています。

### ① CVSS（公式値、NVD API 取得）

| 対象 | CVE | スコア | 深刻度 | 出所 | ベクタ（攻撃条件） |
|---|---|---|---|---|---|
| perl-Text-CSV_XS | 110753 (1件) | 9.8 | CRITICAL | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| perl-Text-CSV_XS | 110756, 110757 (2件) | 9.8 | CRITICAL | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| perl-Text-CSV_XS | 110759 (1件) | 9.8 | CRITICAL | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| gstreamer1-plugins-good | 111183 (1件) | 9.8 | CRITICAL | Secondary(CNA:trendmicro.com) | `(v3.0) AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 111497 (1件) | 9.8 | CRITICAL | Primary(NVD) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| kernel | 98432 (1件) | 9.8 | CRITICAL | Secondary(CNA:UUID416baaa9) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| perl-Cpanel-JSON-XS | 110685 (1件) | 9.1 | CRITICAL | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:H` |
| Corretto(JDK各版) | 114820 (1件) | 9.1 | CRITICAL | Secondary(CNA:oracle.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| amazon-cloudwatch-agent | 78663 (1件) | 9.1 | CRITICAL | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 102870 (1件) | 8.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| freerdp | 114045 (1件) | 8.8 | HIGH | Secondary(CNA:vulncheck.com) | `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 70007 (1件) | 8.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 83520 (1件) | 8.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 96957 (1件) | 8.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| perl-Cpanel-JSON-XS | 110681 (1件) | 8.1 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:H/A:H` |
| perl-Cpanel-JSON-XS | 110684 (1件) | 8.1 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 70175 (1件) | 8.1 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 70197 (1件) | 8.1 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| emacs | 108976 (1件) | 7.8 | HIGH | Secondary(CNA:mitre.org) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 114148 (1件) | 7.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| gstreamer1-plugins-good | 18299 (1件) | 7.8 | HIGH | Secondary(CNA:trendmicro.com) | `(v3.0) AV:L/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47489, 47595, 47599 (3件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47491 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47494 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47500, 47516, 47551, 47560, 47587, 47588, 47589, 47590, 47594, 47597 (10件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47501, 47511, 47523, 47530, 47548, 47553, 47561, 47601 (8件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47502, 47510, 47556 (3件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47504, 47569, 47572 (3件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47507 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47508 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47512, 47513, 47545, 47592 (4件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47514 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47528 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47540 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47552, 47559 (2件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47558 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47563 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47591 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47600 (1件) | 7.8 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| emacs | 79992 (1件) | 7.8 | HIGH | Secondary(CNA:redhat.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 96225, 96231 (2件) | 7.8 | HIGH | Secondary(CNA:microsoft.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 109468, 70159, 70181, 96236, 96959 (5件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Cpanel-JSON-XS | 110672 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Cpanel-JSON-XS | 110673 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Cpanel-JSON-XS | 110676 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Cpanel-JSON-XS | 110678 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Cpanel-JSON-XS | 110680 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Text-CSV_XS | 110752 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Text-CSV_XS | 110755 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| perl-Text-CSV_XS | 110758 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N` |
| python-dns | 114605 (1件) | 7.5 | HIGH | Secondary(CNA:github.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 58280 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 69651, 84008, 96958 (3件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 70179 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 70183 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 70186 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| amazon-cloudwatch-agent | 78659 (1件) | 7.5 | HIGH | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 96233 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 96237 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| dotnet(8.0/9.0/10.0) | 96960 (1件) | 7.5 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| dotnet(8.0/9.0/10.0) | 96222 (1件) | 7.4 | HIGH | Secondary(CNA:microsoft.com) | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| NVIDIA系(13パッケージ共通) | 47554 (1件) | 7.1 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47602 (1件) | 7.1 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47596 (1件) | 7.0 | HIGH | Secondary(CNA:nvidia.com) | `AV:P/AC:H/PR:L/UI:N/S:C/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47598 (1件) | 7.0 | HIGH | Secondary(CNA:nvidia.com) | `AV:L/AC:H/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| amazon-cloudwatch-agent | 111943 (1件) | 6.8 | MEDIUM | Secondary(CNA:UUID134c704f) | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:N` |
| freerdp | 114047 (1件) | 6.8 | MEDIUM | Secondary(CNA:vulncheck.com) | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:N` |
| NVIDIA系(13パッケージ共通) | 47509, 47529, 47532, 47537, 47538 (5件) | 6.7 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47515, 47524, 47527 (3件) | 6.7 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47522, 47542, 47543, 47546, 47547 (5件) | 6.7 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47525, 47533 (2件) | 6.7 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| perl-Cpanel-JSON-XS | 110686 (1件) | 6.5 | MEDIUM | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| perl-Text-CSV_XS | 110754 (1件) | 6.5 | MEDIUM | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H` |
| freerdp | 114043 (1件) | 6.5 | MEDIUM | Secondary(CNA:vulncheck.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:N/A:N` |
| freerdp | 114046 (1件) | 6.5 | MEDIUM | Secondary(CNA:vulncheck.com) | `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47565 (1件) | 6.4 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:H/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47586 (1件) | 6.4 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:P/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| NVIDIA系(13パッケージ共通) | 47518 (1件) | 6.0 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:H/PR:H/UI:N/S:U/C:H/I:H/A:L` |
| gstreamer1-plugins-good | 46471 (1件) | 5.5 | MEDIUM | Secondary(CNA:UUID134c704f) | `AV:L/AC:L/PR:N/UI:R/S:U/C:H/I:N/A:N` |
| NVIDIA系(13パッケージ共通) | 47492 (1件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47517, 47549, 47557 (3件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47534 (1件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47555 (1件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N` |
| NVIDIA系(13パッケージ共通) | 47566 (1件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47567, 47568 (2件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47603, 47604 (2件) | 5.5 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N` |
| amazon-cloudwatch-agent | 113470 (1件) | 5.4 | MEDIUM | Secondary(CNA:UUID134c704f) | `AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:L/A:N` |
| NVIDIA系(13パッケージ共通) | 47526, 47531 (2件) | 4.4 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:H/UI:N/S:U/C:N/I:N/A:H` |
| NVIDIA系(13パッケージ共通) | 47562 (1件) | 4.4 | MEDIUM | Secondary(CNA:nvidia.com) | `AV:L/AC:L/PR:L/UI:N/S:U/C:N/I:L/A:L` |
| gstreamer1-plugins-good | 88914 (1件) | 4.4 | MEDIUM | Secondary(CNA:redhat.com) | `AV:L/AC:L/PR:N/UI:R/S:U/C:L/I:N/A:L` |

- `AV:N`＝ネットワーク経由、`AV:L`＝端末上、`PR`＝必要権限、`UI:R`＝利用者の操作が必要、`C/I/A`＝機密性/完全性/可用性への影響。
- 悪用（実際の攻撃）の有無は今回確認していません。

### ② OWASP Risk Rating（**推定**）

OWASP Risk Rating Methodology（尤度＝起きやすさ × 影響度の0〜9評価。LOW<3、MEDIUM 3〜<6、HIGH 6〜9）による**推定値**です。公式値は存在しません。業務影響は環境依存のため採点せず、**CVSS ベクタから機械的に写像した技術ベースの推定**です（`owasp_rr.py` で算出）。

- 写像方針: skill=攻撃難度(AC:L→3/H→5)、motive=4、opportunity=攻撃経路(N→7, L/A→4。UI必要なら最大4)、size=到達範囲(N→9, A→6, L→5。権限要なら最大6)、discovery=3、exploit=(AC:L→5/H→3)、awareness=4、detection=8。影響は機密性/完全性/可用性を CVSS の H/L/N から 9/6/2・7/3/1・7/5/1 に、追跡可能性=7 とした。
- 傾向: 尤度は概ね MEDIUM（4.5〜5.6）、影響度が HIGH となる CVE は総合 High、その他は Medium。**Critical 判定になる CVE はなし**（推定）。

| 対象 | CVE | 尤度 | 影響度 | 総合（推定） |
|---|---|---|---|---|
| perl-Text-CSV_XS | 110753 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| perl-Text-CSV_XS | 110756, 110757 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| perl-Text-CSV_XS | 110759 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| gstreamer1-plugins-good | 111183 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 111497 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| kernel | 98432 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| perl-Cpanel-JSON-XS | 110685 | 5.38 MEDIUM | 6.0 HIGH | **High** |
| Corretto(JDK各版) | 114820 | 5.38 MEDIUM | 6.0 HIGH | **High** |
| amazon-cloudwatch-agent | 78663 | 5.38 MEDIUM | 5.75 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 102870 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| freerdp | 114045 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 70007 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 83520 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 96957 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| perl-Cpanel-JSON-XS | 110681 | 5.0 MEDIUM | 5.75 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110684 | 5.0 MEDIUM | 6.0 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 70175 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 70197 | 5.38 MEDIUM | 7.5 HIGH | **High** |
| emacs | 108976 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 114148 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| gstreamer1-plugins-good | 18299 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47489, 47595, 47599 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47491 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47494 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47500, 47516, 47551, 47560, 47587, 47588, 47589, 47590, 47594, 47597 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47501, 47511, 47523, 47530, 47548, 47553, 47561, 47601 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47502, 47510, 47556 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47504, 47569, 47572 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47507 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47508 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47512, 47513, 47545, 47592 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47514 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47528 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47540 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47552, 47559 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47558 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47563 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47591 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47600 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| emacs | 79992 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 96225, 96231 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 109468, 70159, 70181, 96236, 96959 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110672 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110673 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110676 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110678 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Cpanel-JSON-XS | 110680 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Text-CSV_XS | 110752 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Text-CSV_XS | 110755 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Text-CSV_XS | 110758 | 5.38 MEDIUM | 4.5 MEDIUM | **Medium** |
| python-dns | 114605 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 58280 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 69651, 84008, 96958 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 70179 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 70183 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 70186 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| amazon-cloudwatch-agent | 78659 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 96233 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 96237 | 5.0 MEDIUM | 7.5 HIGH | **High** |
| dotnet(8.0/9.0/10.0) | 96960 | 5.38 MEDIUM | 4.25 MEDIUM | **Medium** |
| dotnet(8.0/9.0/10.0) | 96222 | 5.38 MEDIUM | 6.0 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47554 | 4.5 MEDIUM | 5.75 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47602 | 4.5 MEDIUM | 6.0 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47596 | 4.0 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47598 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| amazon-cloudwatch-agent | 111943 | 5.0 MEDIUM | 6.0 HIGH | **High** |
| freerdp | 114047 | 5.0 MEDIUM | 6.0 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47509, 47529, 47532, 47537, 47538 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47515, 47524, 47527 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47522, 47542, 47543, 47546, 47547 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47525, 47533 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| perl-Cpanel-JSON-XS | 110686 | 5.0 MEDIUM | 4.25 MEDIUM | **Medium** |
| perl-Text-CSV_XS | 110754 | 5.0 MEDIUM | 4.25 MEDIUM | **Medium** |
| freerdp | 114043 | 5.0 MEDIUM | 4.5 MEDIUM | **Medium** |
| freerdp | 114046 | 5.0 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47565 | 4.5 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47586 | 4.0 MEDIUM | 7.5 HIGH | **High** |
| NVIDIA系(13パッケージ共通) | 47518 | 4.5 MEDIUM | 7.0 HIGH | **High** |
| gstreamer1-plugins-good | 46471 | 4.5 MEDIUM | 4.5 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47492 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47517, 47549, 47557 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47534 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47555 | 4.5 MEDIUM | 4.5 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47566 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47567, 47568 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47603, 47604 | 4.5 MEDIUM | 4.5 MEDIUM | **Medium** |
| amazon-cloudwatch-agent | 113470 | 5.0 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47526, 47531 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| NVIDIA系(13パッケージ共通) | 47562 | 4.5 MEDIUM | 4.25 MEDIUM | **Medium** |
| gstreamer1-plugins-good | 88914 | 4.5 MEDIUM | 4.75 MEDIUM | **Medium** |

### ③ OWASP Top 10:2025 との対応

NVD の CWE（弱点の種類の識別子）を、OWASP 公式 Top 10:2025 各カテゴリページ（https://owasp.org/Top10/2025/ ）の Mapped CWEs と機械的に照合しました。Top 10 は Web アプリ向け分類のため、メモリ破壊・DoS・OS/ドライバ系の CWE は「対象外」と表記し、無理に当てはめていません。

| 対象 | CVE | CWE → カテゴリ |
|---|---|---|
| perl-Text-CSV_XS | 110753 | CWE-416→対象外 / CWE-911→対象外 |
| perl-Text-CSV_XS | 110756, 110757 | CWE-116→A05 Injection |
| perl-Text-CSV_XS | 110759 | CWE-1286→対象外 |
| gstreamer1-plugins-good | 111183 | CWE-122→対象外 |
| dotnet(8.0/9.0/10.0) | 111497 | CWE-252→A10 Mishandling of Exceptional Conditions / CWE-787→対象外 |
| kernel | 98432 | CWE未付与→対象外 |
| perl-Cpanel-JSON-XS | 110685 | CWE-401→対象外 |
| Corretto(JDK各版) | 114820 | CWE-327→A04 Cryptographic Failures |
| amazon-cloudwatch-agent | 78663 | CWE-675→対象外 |
| dotnet(8.0/9.0/10.0) | 102870 | CWE-94→A05 Injection |
| freerdp | 114045 | CWE-122→対象外 |
| dotnet(8.0/9.0/10.0) | 70007 | CWE-787→対象外 |
| dotnet(8.0/9.0/10.0) | 83520 | CWE-502→A08 Software or Data Integrity Failures |
| dotnet(8.0/9.0/10.0) | 96957 | CWE-347→A04 Cryptographic Failures |
| perl-Cpanel-JSON-XS | 110681 | CWE-416→対象外 |
| perl-Cpanel-JSON-XS | 110684 | CWE-401→対象外 |
| dotnet(8.0/9.0/10.0) | 70175 | CWE-640→A07 Authentication Failures |
| dotnet(8.0/9.0/10.0) | 70197 | CWE-787→対象外 |
| emacs | 108976 | CWE-184→対象外 |
| dotnet(8.0/9.0/10.0) | 114148 | CWE-276→A01 Broken Access Control |
| gstreamer1-plugins-good | 18299 | CWE-416→対象外 |
| NVIDIA系(13パッケージ共通) | 47489, 47595, 47599 | CWE-281→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47491 | CWE-404→対象外 |
| NVIDIA系(13パッケージ共通) | 47494 | CWE-134→対象外 |
| NVIDIA系(13パッケージ共通) | 47500, 47516, 47551, 47560, 47587, 47588, 47589, 47590, 47594, 47597 | CWE-416→対象外 |
| NVIDIA系(13パッケージ共通) | 47501, 47511, 47523, 47530, 47548, 47553, 47561, 47601 | CWE-787→対象外 |
| NVIDIA系(13パッケージ共通) | 47502, 47510, 47556 | CWE-190→対象外 |
| NVIDIA系(13パッケージ共通) | 47504, 47569, 47572 | CWE-843→対象外 |
| NVIDIA系(13パッケージ共通) | 47507 | CWE-129→A05 Injection |
| NVIDIA系(13パッケージ共通) | 47508 | CWE-681→対象外 |
| NVIDIA系(13パッケージ共通) | 47512, 47513, 47545, 47592 | CWE-125→対象外 |
| NVIDIA系(13パッケージ共通) | 47514 | CWE-200→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47528 | CWE-824→対象外 |
| NVIDIA系(13パッケージ共通) | 47540 | CWE-191→対象外 |
| NVIDIA系(13パッケージ共通) | 47552, 47559 | CWE-862→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47558 | CWE-415→対象外 |
| NVIDIA系(13パッケージ共通) | 47563 | CWE-476→A10 Mishandling of Exceptional Conditions |
| NVIDIA系(13パッケージ共通) | 47591 | CWE-863→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47600 | CWE-908→対象外 |
| emacs | 79992 | CWE-78→A05 Injection |
| dotnet(8.0/9.0/10.0) | 96225, 96231 | CWE-59→A01 Broken Access Control |
| dotnet(8.0/9.0/10.0) | 109468, 70159, 70181, 96236, 96959 | CWE-770→対象外 |
| perl-Cpanel-JSON-XS | 110672 | CWE-401→対象外 |
| perl-Cpanel-JSON-XS | 110673 | CWE-674→対象外 |
| perl-Cpanel-JSON-XS | 110676 | CWE-405→対象外 |
| perl-Cpanel-JSON-XS | 110678 | CWE-770→対象外 |
| perl-Cpanel-JSON-XS | 110680 | CWE-787→対象外 |
| perl-Text-CSV_XS | 110752 | CWE-770→対象外 |
| perl-Text-CSV_XS | 110755 | CWE-407→対象外 |
| perl-Text-CSV_XS | 110758 | CWE-127→対象外 |
| python-dns | 114605 | CWE-674→対象外 |
| dotnet(8.0/9.0/10.0) | 58280 | CWE-674→対象外 |
| dotnet(8.0/9.0/10.0) | 69651, 84008, 96958 | CWE-407→対象外 |
| dotnet(8.0/9.0/10.0) | 70179 | CWE-290→A07 Authentication Failures |
| dotnet(8.0/9.0/10.0) | 70183 | CWE-362→A06 Insecure Design |
| dotnet(8.0/9.0/10.0) | 70186 | CWE-833→対象外 |
| amazon-cloudwatch-agent | 78659 | CWE-405→対象外 |
| dotnet(8.0/9.0/10.0) | 96233 | CWE-787→対象外 |
| dotnet(8.0/9.0/10.0) | 96237 | CWE-829→A08 Software or Data Integrity Failures |
| dotnet(8.0/9.0/10.0) | 96960 | CWE-405→対象外 |
| dotnet(8.0/9.0/10.0) | 96222 | CWE-295→A07 Authentication Failures |
| NVIDIA系(13パッケージ共通) | 47554 | CWE-347→A04 Cryptographic Failures |
| NVIDIA系(13パッケージ共通) | 47602 | CWE-119→対象外 |
| NVIDIA系(13パッケージ共通) | 47596 | CWE-281→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47598 | CWE-416→対象外 |
| amazon-cloudwatch-agent | 111943 | CWE-299→A07 Authentication Failures |
| freerdp | 114047 | CWE-295→A07 Authentication Failures |
| NVIDIA系(13パッケージ共通) | 47509, 47529, 47532, 47537, 47538 | CWE-787→対象外 |
| NVIDIA系(13パッケージ共通) | 47515, 47524, 47527 | CWE-125→対象外 |
| NVIDIA系(13パッケージ共通) | 47522, 47542, 47543, 47546, 47547 | CWE-20→A05 Injection |
| NVIDIA系(13パッケージ共通) | 47525, 47533 | CWE-129→A05 Injection |
| perl-Cpanel-JSON-XS | 110686 | CWE-416→対象外 |
| perl-Text-CSV_XS | 110754 | CWE-401→対象外 |
| freerdp | 114043 | CWE-125→対象外 |
| freerdp | 114046 | CWE-476→A10 Mishandling of Exceptional Conditions |
| NVIDIA系(13パッケージ共通) | 47565 | CWE-362→A06 Insecure Design |
| NVIDIA系(13パッケージ共通) | 47586 | CWE-416→対象外 |
| NVIDIA系(13パッケージ共通) | 47518 | CWE-732→A01 Broken Access Control |
| gstreamer1-plugins-good | 46471 | CWE-126→対象外 |
| NVIDIA系(13パッケージ共通) | 47492 | CWE-862→A01 Broken Access Control |
| NVIDIA系(13パッケージ共通) | 47517, 47549, 47557 | CWE-476→A10 Mishandling of Exceptional Conditions |
| NVIDIA系(13パッケージ共通) | 47534 | CWE-369→A10 Mishandling of Exceptional Conditions |
| NVIDIA系(13パッケージ共通) | 47555 | CWE-908→対象外 |
| NVIDIA系(13パッケージ共通) | 47566 | CWE-401→対象外 |
| NVIDIA系(13パッケージ共通) | 47567, 47568 | CWE-400→対象外 |
| NVIDIA系(13パッケージ共通) | 47603, 47604 | CWE-862→A01 Broken Access Control |
| amazon-cloudwatch-agent | 113470 | CWE-295→A07 Authentication Failures |
| NVIDIA系(13パッケージ共通) | 47526, 47531 | CWE-476→A10 Mishandling of Exceptional Conditions |
| NVIDIA系(13パッケージ共通) | 47562 | CWE-116→A05 Injection |
| gstreamer1-plugins-good | 88914 | CWE-190→対象外 |

### 今週の優先度（所見）

1. **最優先候補（CVSS 9.8）:** `kernel`（CVE-2026-98432、IPv4 処理、CNA=Linux kernel）、`dotnet8.0` の Brotli バッファオーバーフロー（CVE-2026-111497、NVD 自身の Primary 採点）、`gstreamer1-plugins-good` の rtpL16depay（CVE-2026-111183、v3.0）、Perl `Text::CSV_XS` の4件。いずれもネットワーク経由・認証不要のベクタですが、実際の到達性は利用形態（該当モジュールに外部入力を渡すか）に依存します。
2. **Corretto（Java）CVE-2026-114820（9.1）:** CWE-327（→ A04 Cryptographic Failures）。Java を使う全サービスが対象で、6系統を同時に更新する必要があります。
3. **dotnet 系:** 約25件の CVE を3バージョンで共通修正。CVSS 7.5〜8.8 が中心で、ASP.NET Core を公開している場合のみ優先度を上げる。
4. **NVIDIA ドライバ系:** 79 CVE（CVSS 4.4〜7.8、`AV:L`＝ローカル端末上の操作が前提）。GPU 搭載サーバのみ関係。
5. 総括: Critical ラベルは0件でも、CVSS 9.8 が複数ある週です。尺度が異なるため、CVSS と OWASP 推定の値は別軸で読んでください。

> 出典: NVD API（https://nvd.nist.gov/）、ALAS（https://alas.aws.amazon.com/AL2023/）、OWASP Risk Rating Methodology（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）

---

## その他

- Medium: 34件（ca-certificates, containerd, libxml2, openssh, nginx, golang, firefox, python3.11 ほか）/ Low: 1件（ecs-service-connect-agent）※件数のみの記録で詳細は割愛。
- 一覧の切り詰め（truncated）: あり。reportable 105件のうち詳細取得は先頭30件。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
