作成日: 2026-09-05 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

# AL2023セキュリティアドバイザリ週次まとめ（2026-09-05）— kernel大量CVEロールアップとpostgresql/dotnet/Firefox関連の複数脆弱性

> **ALAS（Amazon Linux Security Advisory）** とは、AWS（Amazon Web Services）がAmazon Linuxで見つかった脆弱性（ぜいじゃくせい＝ソフトウェアのセキュリティ上の弱点）を公式に告知する仕組みです。本記事はAWS公式のALAS RSS（フィード配信）を情報源に、直近1週間で新規公開されたアドバイザリのうち **Critical（緊急）** と **Important（重要）** をまとめたものです。

## サマリー（重大度別件数）

| 重大度 | 件数 |
|---|---|
| Critical（緊急） | 0 |
| Important（重要） | 39 |
| Medium（中） | 13（本記事では詳細割愛、件数のみ） |
| Low（低） | 4（本記事では詳細割愛、件数のみ） |

新規検知の合計: 56件 / うちCritical+Important（掲載対象）: 39件

> ⚠️ 注記: Critical+Importantが39件と多く、詳細取得（overview/CVE一覧の展開）は先頭30件のみ実施しています。残り9件はALAS IDのみ把握しており、詳細は各アドバイザリページを直接ご確認ください。

---

## 対処方法（共通）

AL2023環境では、通常は以下のコマンドで更新可能なパッチの有無を確認し、必要に応じて適用します。

```bash
sudo dnf check-release-update
sudo dnf update
```

> 🔒 本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドは実行していません。実際の適用は各サーバ管理者の判断・作業としてお願いします。

---

## 詳細一覧（Critical + Important、先頭30件）

### ALAS2023-2026-2070（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2070](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2070.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `iperf3`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-71217
- **概要:** A flaw was found in iperf3. A remote attacker can exploit this vulnerability by sending crafted control-channel JSON with oversized numeric parameters, such as `parallel` and `len`, which are not properly validated by the server. This improper input validation can lead to excessive stream and thread creation, as well as large buffer allocations, causing resource exhaustion. Consequently, this can result in a Denial of Service (DoS) on the affected iperf3 server. (CVE-2026-71217)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2070.html

### ALAS2023-2026-2071（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2071](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2071.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel6.18`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-53005, CVE-2026-64192, CVE-2026-64227, CVE-2026-64287, CVE-2026-64352, CVE-2026-64353, CVE-2026-64371, CVE-2026-64375, CVE-2026-64472, CVE-2026-64530, CVE-2026-64532, CVE-2026-64533, CVE-2026-64538, CVE-2026-64542, CVE-2026-64543 …ほか250件（合計265件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: af_unix: Drop all SCM attributes for SOCKMAP. (CVE-2026-53005) In the Linux kernel, the following vulnerability has been resolved: bpf: Reject BPF_MAP_TYPE_INODE_STORAGE creation if BPF LSM is uninitialized When CONFIG_BPF_LSM=y is set, BPF inode storage maps (BPF_MAP_TYPE_INODE_STORAGE) are compiled into the kernel. However, if the BPF LSM is not explicitly enabled at boot time (e.g. omitted from the "lsm=" boot parameter), lsm…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2071.html

### ALAS2023-2026-2073（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2073](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2073.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `swiftlang`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-43823
- **概要:** When initializing an RSA public key from DER or PEM bytes throws an error, the EVP_PKEY* is double-freed: first in the catch block, then in the deinit. This can lead to a crash on future memory allocations. This double-free manifests when BoringSSL cannot decode the public key from the bytes provided. This vulnerability is addressed in swift-crypto version 4.5.1. (CVE-2026-43823)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2073.html

### ALAS2023-2026-2075（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2075](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2075.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `perl-DBI`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-73194
- **概要:** DBI versions before 1.652 for Perl allow a heap out-of-bounds write via an unvalidated numeric placeholder that sets the binder counter in preparse. preparse reserves seven output bytes per input byte, the width of the longest ':p99999' expansion. The ':N' branch parses the number with `atoi(src)` and assigns it to the binder counter with no range check, so a statement containing ':2147483648' leaves the counter negative (-2147483648 with glibc, where atoi wraps). Each following '?' then expands…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2075.html

### ALAS2023-2026-2076（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2076](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2076.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `postgresql17`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-14662, CVE-2026-14663, CVE-2026-14664, CVE-2026-14666, CVE-2026-14668, CVE-2026-14669, CVE-2026-14670, CVE-2026-14671, CVE-2026-14672, CVE-2026-14678, CVE-2026-14679, CVE-2026-14680, CVE-2026-14681, CVE-2026-15741, CVE-2026-15742 …ほか12件（合計27件。全件はALASページ参照）
- **概要:** Integer wraparound in PostgreSQL tsvector and tsquery data type functions allows an unprivileged database user to cause the server to undersize an allocation and write out-of-bounds, via crafted large inputs. This may execute arbitrary code as the operating system user running the database. These types are typically sourced from application logic, not taken from the application's user. Hence, application users attacking the database, through the application as a conduit, are unlikely. CVE-2026-6…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2076.html

### ALAS2023-2026-2077（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2077](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2077.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `postgresql15`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-14662, CVE-2026-14663, CVE-2026-14664, CVE-2026-14666, CVE-2026-14668, CVE-2026-14669, CVE-2026-14670, CVE-2026-14671, CVE-2026-14673, CVE-2026-14678, CVE-2026-14679, CVE-2026-14680, CVE-2026-15741, CVE-2026-15742, CVE-2026-16239 …ほか11件（合計26件。全件はALASページ参照）
- **概要:** Integer wraparound in PostgreSQL tsvector and tsquery data type functions allows an unprivileged database user to cause the server to undersize an allocation and write out-of-bounds, via crafted large inputs. This may execute arbitrary code as the operating system user running the database. These types are typically sourced from application logic, not taken from the application's user. Hence, application users attacking the database, through the application as a conduit, are unlikely. CVE-2026-6…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2077.html

### ALAS2023-2026-2078（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2078](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2078.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `postgresql16`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-14662, CVE-2026-14663, CVE-2026-14664, CVE-2026-14666, CVE-2026-14668, CVE-2026-14669, CVE-2026-14670, CVE-2026-14671, CVE-2026-14672, CVE-2026-14673, CVE-2026-14678, CVE-2026-14679, CVE-2026-14680, CVE-2026-15741, CVE-2026-15742 …ほか12件（合計27件。全件はALASページ参照）
- **概要:** Integer wraparound in PostgreSQL tsvector and tsquery data type functions allows an unprivileged database user to cause the server to undersize an allocation and write out-of-bounds, via crafted large inputs. This may execute arbitrary code as the operating system user running the database. These types are typically sourced from application logic, not taken from the application's user. Hence, application users attacking the database, through the application as a conduit, are unlikely. CVE-2026-6…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2078.html

### ALAS2023-2026-2079（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2079](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2079.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `postgresql18`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-14662, CVE-2026-14663, CVE-2026-14664, CVE-2026-14666, CVE-2026-14668, CVE-2026-14669, CVE-2026-14670, CVE-2026-14671, CVE-2026-14672, CVE-2026-14673, CVE-2026-14676, CVE-2026-14678, CVE-2026-14679, CVE-2026-14680, CVE-2026-14681 …ほか15件（合計30件。全件はALASページ参照）
- **概要:** Integer wraparound in PostgreSQL tsvector and tsquery data type functions allows an unprivileged database user to cause the server to undersize an allocation and write out-of-bounds, via crafted large inputs. This may execute arbitrary code as the operating system user running the database. These types are typically sourced from application logic, not taken from the application's user. Hence, application users attacking the database, through the application as a conduit, are unlikely. CVE-2026-6…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2079.html

### ALAS2023-2026-2080（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2080](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2080.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `microcode_ctl`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2025-31936, CVE-2025-31938, CVE-2025-35973, CVE-2026-20707, CVE-2026-20713, CVE-2026-20716, CVE-2026-20901, CVE-2026-20917
- **概要:** Improper handling of overlap between protected memory ranges for some Intel(R) Xeon(R) 6 processors when using Intel(R) TDX within SMM may allow an escalation of privilege. SMM adversary with a privileged user combined with a high complexity attack may enable escalation of privilege. This result may potentially occur via local access when attack requirements are present with special internal knowledge and requires no user interaction. The potential vulnerability may impact the confidentiality (h…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2080.html

### ALAS2023-2026-2083（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2083](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2083.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `libgit2`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-53583, CVE-2026-53584, CVE-2026-53585, CVE-2026-53586, CVE-2026-53587, CVE-2026-5917
- **概要:** libgit2 Inverted IP SubjectAltName Comparison in OpenSSL Backend ( vuln_1_1_1 ) (CVE-2026-53583) libgit2 Submodule path traversal (CVE-2026-53584) Unbounded Memory Allocation via Delta Object Result-Size Header (CVE-2026-53585) libgit2's builtin HTTP transport follows offsite redirects for the initial smart HTTP request by default. If the redirected server then returns 401 Unauthorized, libgit2 asks the application credential callback for credentials using the original remote URL, not the redire…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2083.html

### ALAS2023-2026-2084（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2084](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2084.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `clamav1.4`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-20339, CVE-2026-20345, CVE-2026-20346, CVE-2026-20347, CVE-2026-20348
- **概要:** A vulnerability in the PESpin file format parser of ClamAV could allow an unauthenticated, remote attacker to cause a DoS condition or possibly other expanded impacts as a result of memory corruption on an affected device. This vulnerability is due to improper boundary checks for content in PESpin files during scanning, which may result in an integer overflow. An attacker could exploit this vulnerability by submitting a crafted file that contains PESpin content to be scanned by ClamAV on an affe…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2084.html

### ALAS2023-2026-2085（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2085](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2085.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `dracut`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-15816
- **概要:** A flaw was found in dracut. The die() error-handling function writes its message into a shell script under the initramfs emergency-hook directory without properly shell-quoting it. When the message contains data derived from the DHCP ROOT_PATH option, an attacker on the adjacent network who controls a rogue DHCP server can inject a command-substitution sequence that executes as root the next time dracut sources its emergency hook scripts during standard boot-failure handling. (CVE-2026-15816)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2085.html

### ALAS2023-2026-2086（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2086](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2086.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `libsoup`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-15711
- **概要:** A vulnerability was found in libsoup's WebSocket frame parsing implementation. The library fails to validate length rules specified in RFC 6455 SS5.5, which mandates that all WebSocket control frames (e.g., PING, PONG, CLOSE) contain a payload of 125 bytes or less. A remote, unauthenticated attacker can exploit this by sending a non-compliant, oversized control frame. Because the parser handles this protocol violation improperly instead of throwing an immediate connection termination error, it t…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2086.html

### ALAS2023-2026-2087（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2087](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2087.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `libsoup3`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-15711
- **概要:** A vulnerability was found in libsoup's WebSocket frame parsing implementation. The library fails to validate length rules specified in RFC 6455 SS5.5, which mandates that all WebSocket control frames (e.g., PING, PONG, CLOSE) contain a payload of 125 bytes or less. A remote, unauthenticated attacker can exploit this by sending a non-compliant, oversized control frame. Because the parser handles this protocol violation improperly instead of throwing an immediate connection termination error, it t…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2087.html

### ALAS2023-2026-2088（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2088](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2088.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `openssl`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-14456
- **概要:** Issue summary: When an OpenSSL QUIC server (Listener SSL object) processes valid QUIC Initial packets for unknown destination connection IDs, it can allocate and queue new incoming channels without enforcing any limit. Impact summary: A remote peer that can make many Initial packets reach the server listener faster than the application accepts connections, can cause the memory allocated to store the per-channel state to grow without any limits, potentially making the QUIC listener unavailable an…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2088.html

### ALAS2023-2026-2094（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2094](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2094.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `dotnet10.0`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-62899, CVE-2026-62900, CVE-2026-62901, CVE-2026-62909
- **概要:** Inconsistent interpretation of http requests ('http request/response smuggling') in .NET allows an unauthorized attacker to bypass a security feature over a network. (CVE-2026-62899) Improper removal of sensitive information before storage or transfer in .NET allows an unauthorized attacker to disclose information over a network. (CVE-2026-62900) Unchecked input for loop condition in .NET allows an unauthorized attacker to deny service over a network. (CVE-2026-62901) Uncaught exception in .NET …（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2094.html

### ALAS2023-2026-2095（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2095](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2095.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `dotnet8.0`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-62899, CVE-2026-62900, CVE-2026-62901, CVE-2026-62909
- **概要:** Inconsistent interpretation of http requests ('http request/response smuggling') in .NET allows an unauthorized attacker to bypass a security feature over a network. (CVE-2026-62899) Improper removal of sensitive information before storage or transfer in .NET allows an unauthorized attacker to disclose information over a network. (CVE-2026-62900) Unchecked input for loop condition in .NET allows an unauthorized attacker to deny service over a network. (CVE-2026-62901) Uncaught exception in .NET …（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2095.html

### ALAS2023-2026-2096（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2096](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2096.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `dotnet9.0`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-62899, CVE-2026-62900, CVE-2026-62901, CVE-2026-62909
- **概要:** Inconsistent interpretation of http requests ('http request/response smuggling') in .NET allows an unauthorized attacker to bypass a security feature over a network. (CVE-2026-62899) Improper removal of sensitive information before storage or transfer in .NET allows an unauthorized attacker to disclose information over a network. (CVE-2026-62900) Unchecked input for loop condition in .NET allows an unauthorized attacker to deny service over a network. (CVE-2026-62901) Uncaught exception in .NET …（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2096.html

### ALAS2023-2026-2101（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2101](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2101.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `java-26-amazon-corretto`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-60589, CVE-2026-61308, CVE-2026-70906, CVE-2026-70907
- **概要:** Vulnerability in the Oracle Java SE, Oracle GraalVM for JDK, Oracle GraalVM Enterprise Edition product of Oracle Java SE (component: Security). Supported versions that are affected are Oracle Java SE: 8u501, 11.0.32, 17.0.20, 21.0.12, 25.0.4, 26.0.2; Oracle GraalVM for JDK: 17.0.20 and 21.0.12; Oracle GraalVM Enterprise Edition: 21.3.19. Difficult to exploit vulnerability allows unauthenticated attacker with network access via multiple protocols to compromise Oracle Java SE, Oracle GraalVM for J…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2101.html

### ALAS2023-2026-2102（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2102](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2102.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `java-25-amazon-corretto`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-60589, CVE-2026-61308, CVE-2026-70906, CVE-2026-70907
- **概要:** Vulnerability in the Oracle Java SE, Oracle GraalVM for JDK, Oracle GraalVM Enterprise Edition product of Oracle Java SE (component: Security). Supported versions that are affected are Oracle Java SE: 8u501, 11.0.32, 17.0.20, 21.0.12, 25.0.4, 26.0.2; Oracle GraalVM for JDK: 17.0.20 and 21.0.12; Oracle GraalVM Enterprise Edition: 21.3.19. Difficult to exploit vulnerability allows unauthenticated attacker with network access via multiple protocols to compromise Oracle Java SE, Oracle GraalVM for J…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2102.html

### ALAS2023-2026-2104（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2104](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2104.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `udisks2`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-7867
- **概要:** Local privilege escalation via as-user mount spoofing NOTE: https://github.com/azqzazq1/CVE-2026-7867-disk2root (CVE-2026-7867)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2104.html

### ALAS2023-2026-2105（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2105](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2105.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `firefox`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-66046, CVE-2026-72522, CVE-2026-74934, CVE-2026-74935, CVE-2026-74936, CVE-2026-74938, CVE-2026-74939, CVE-2026-74940, CVE-2026-74941, CVE-2026-74942, CVE-2026-74943, CVE-2026-74944, CVE-2026-74945, CVE-2026-74946, CVE-2026-74948 …ほか26件（合計41件。全件はALASページ参照）
- **概要:** Expat through 2.8.3 contains a denial of service vulnerability caused by quadratic algorithmic complexity in the storeAtts() function in xmlparse.c, where processing N specified attributes with non-normalized values triggers an O(N^2) linear scan of elementType->defaultAtts to determine CDATA status. A remote unauthenticated attacker can supply a single well-formed XML document of a few megabytes to an application parsing untrusted XML to cause excessive CPU consumption, resulting in denial of s…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2105.html

### ALAS2023-2026-2106（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2106](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2106.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel6.18`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-45897, CVE-2026-45901, CVE-2026-53090, CVE-2026-63978, CVE-2026-63979, CVE-2026-64017, CVE-2026-64283, CVE-2026-64523, CVE-2026-64562, CVE-2026-64563, CVE-2026-64564, CVE-2026-64567, CVE-2026-64572, CVE-2026-64575, CVE-2026-64576 …ほか158件（合計173件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: netfilter: nft_counter: serialize reset with spinlock (CVE-2026-45897) In the Linux kernel, the following vulnerability has been resolved: netfilter: nf_tables: revert commit_mutex usage in reset path (CVE-2026-45901) In the Linux kernel, the following vulnerability has been resolved: bpf: Fix ld_{abs,ind} failure path analysis in subprogs (CVE-2026-53090) In the Linux kernel, the following vulnerability has been resolved: net/h…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2106.html

### ALAS2023-2026-2107（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2107](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2107.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-64017, CVE-2026-64564, CVE-2026-64581, CVE-2026-68131, CVE-2026-68138, CVE-2026-68155, CVE-2026-68160, CVE-2026-68299, CVE-2026-68335, CVE-2026-68338, CVE-2026-68480, CVE-2026-72051, CVE-2026-74556, CVE-2026-74580
- **概要:** In the Linux kernel, the following vulnerability has been resolved: blk-mq: pop cached request if it is usable (CVE-2026-64017) In the Linux kernel, the following vulnerability has been resolved: sctp: don't free the ASCONF's own transport in DEL-IP processing (CVE-2026-64564) In the Linux kernel, the following vulnerability has been resolved: xfrm: fix sk_dst_cache double-free in xfrm_user_policy() (CVE-2026-64581) In the Linux kernel, the following vulnerability has been resolved: rbd: Reset p…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2107.html

### ALAS2023-2026-2108（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2108](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2108.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `vim`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-73070, CVE-2026-73071, CVE-2026-73072, CVE-2026-73073, CVE-2026-73074, CVE-2026-73075, CVE-2026-73076, CVE-2026-73077, CVE-2026-73078
- **概要:** Vim is an open source, command line text editor. Prior to 9.2.0842, the socket server backend in src/socketserver.c accepts unbounded client connections in socketserver_accept(), causing descriptors to overflow fd_set structures in src/channel.c and fixed-size struct pollfd arrays in src/os_unix.c, which allows a local process that can connect to the server socket to corrupt stack memory or terminate the Vim server. This issue is fixed in version 9.2.0842. (CVE-2026-73070) Vim is an open source,…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2108.html

### ALAS2023-2026-2109（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2109](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2109.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kbd`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-72693
- **概要:** `openvt -u` is intended to identify the owner of the current VT and then execute `login` as that user from a privileged context. In the documented `kbrequest`/init usage, the ownership test in `authenticate_user()` relies on `stat("/proc/<pid>/fd/0")`. `stat()` on `/proc/<pid>/fd/0` follows the symlink to the underlying TTY device node. As a result, `buf.st_uid` reflects the owner of the TTY node rather than the owner of the process holding the file descriptor. If the TTY owner returns to `root`…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2109.html

### ALAS2023-2026-2110（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2110](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2110.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel6.12`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-45897, CVE-2026-45901, CVE-2026-53090, CVE-2026-64017, CVE-2026-64205, CVE-2026-64290, CVE-2026-64562, CVE-2026-64563, CVE-2026-64564, CVE-2026-64567, CVE-2026-64572, CVE-2026-64576, CVE-2026-64579, CVE-2026-64580, CVE-2026-64581 …ほか138件（合計153件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: netfilter: nft_counter: serialize reset with spinlock (CVE-2026-45897) In the Linux kernel, the following vulnerability has been resolved: netfilter: nf_tables: revert commit_mutex usage in reset path (CVE-2026-45901) In the Linux kernel, the following vulnerability has been resolved: bpf: Fix ld_{abs,ind} failure path analysis in subprogs (CVE-2026-53090) In the Linux kernel, the following vulnerability has been resolved: blk-m…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2110.html

### ALAS2023-2026-2111（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2111](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2111.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `freerdp`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-64624, CVE-2026-66402, CVE-2026-67288, CVE-2026-67289, CVE-2026-67291, CVE-2026-67293, CVE-2026-67294, CVE-2026-67295, CVE-2026-67297, CVE-2026-67298, CVE-2026-67299, CVE-2026-67300, CVE-2026-67301, CVE-2026-67302, CVE-2026-67303 …ほか7件（合計22件。全件はALASページ参照）
- **概要:** FreeRDP before 3.28.0 treats lines beginning with forward slash in RDP files as raw command-line options, exposing the entire CLI parser surface to untrusted files. Attackers can craft malicious RDP files with /rdp2tcp, /cert:ignore, or /drive options to execute arbitrary commands, bypass certificate validation, or expose local filesystems without user interaction. (CVE-2026-64624) FreeRDP before 3.29.0 (affected versions <= 3.28.0) contains multiple TLS certificate identity validation weaknesse…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2111.html

### ALAS2023-2026-2112（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2112](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2112.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `libXfont2`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-44950, CVE-2026-59679
- **概要:** A flaw was found in the libXfont2 font-server client. This heap buffer overflow vulnerability allows a malicious font server to send specially crafted glyph data. The fs_read_glyphs() function fails to properly validate the total size of the incoming data, leading to an overwrite of memory beyond the intended buffer. If the X server runs as a privileged user, this could result in privilege escalation, allowing an attacker to gain higher access. If the X server runs as an unprivileged user, it co…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2112.html

### ALAS2023-2026-2113（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2113](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2113.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `rust-cargo-c`
- **公開日:** Mon, 31 Aug 2026 18:58:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-5917
- **概要:** libgit2 versions v0.27.0 through v1.9.0 built with the libssh2 SSH backend (USE_SSH=libssh2) contain a shell command injection vulnerability that allows remote attackers to execute arbitrary commands on an SSH server by supplying a repository path containing unescaped shell metacharacters such as single quotes, semicolons, or pipes. The gen_proto() function in ssh_libssh2.c inserts the repository path directly into a shell command string without escaping special characters before passing it to l…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2113.html

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。

## License

情報源: AWS公式 ALAS RSS（https://alas.aws.amazon.com/AL2023/alas.rss）
