作成日: 2026-08-22 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

# AL2023セキュリティアドバイザリ週次まとめ（2026-08-22）— kernel6.18大量CVEロールアップとperl-Net-DNSコマンド実行脆弱性

> **ALAS（Amazon Linux Security Advisory）** とは、AWS（Amazon Web Services）がAmazon Linuxで見つかった脆弱性（ぜいじゃくせい＝ソフトウェアのセキュリティ上の弱点）を公式に告知する仕組みです。本記事はAWS公式のALAS RSS（フィード配信）を情報源に、直近1週間で新規公開されたアドバイザリのうち **Critical（緊急）** と **Important（重要）** をまとめたものです。

## サマリー（重大度別件数）

| 重大度 | 件数 |
|---|---|
| Critical（緊急） | 0 |
| Important（重要） | 22 |
| Medium（中） | 3（本記事では詳細割愛、件数のみ） |
| Low（低） | 0（本記事では詳細割愛、件数のみ） |

新規検知の合計: 25件 / うちCritical+Important（掲載対象）: 22件

---

## 対処方法（共通）

AL2023環境では、通常は以下のコマンドで更新可能なパッチの有無を確認し、必要に応じて適用します。

```bash
sudo dnf check-release-update
sudo dnf update
```

> 🔒 本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドは実行していません。実際の適用は各サーバ管理者の判断・作業としてお願いします。

---

## 詳細一覧（Critical + Important）

### ALAS2023-2026-2045（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2045](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2045.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel6.18`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-45945, CVE-2026-53027, CVE-2026-53402, CVE-2026-64187, CVE-2026-64189, CVE-2026-64205, CVE-2026-64256, CVE-2026-64258, CVE-2026-64259, CVE-2026-64260, CVE-2026-64261, CVE-2026-64262, CVE-2026-64263, CVE-2026-64264, CVE-2026-64265 …ほか95件（合計110件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: iommu/vt-d: Fix race condition during PASID entry replacement (CVE-2026-45945) In the Linux kernel, the following vulnerability has been resolved: fs/ntfs3: fix missing run load for vcn0 in attr_data_get_block_locked() (CVE-2026-53027) In the Linux kernel, the following vulnerability has been resolved: fbdev: fbcon: fix out-of-bounds read in err_out of fbcon_do_set_font() When fbcon_do_set_font() fails (e.g., due to a memory all…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2045.html

### ALAS2023-2026-2046（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2046](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2046.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `perl-Net-DNS`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-64193, CVE-2026-64194
- **概要:** Net::DNS versions through 1.55 for Perl allow remote execution injection via EDNS EXTENDED ERROR. Net::DNS::RR::OPT::EXTENDED_ERROR::_decompose parses the EXTRA-TEXT field of an EDNS EXTENDED-ERROR option (RFC 8914) by tokenising the raw bytes and passing the result to Perl's eval. There is some escaping done for $ and @, but not for backticks. This can be exploited for command execution if $pkt->edns->option('EXTENDED-ERROR') is called in array context, for example with a payload of {0:`"<comma…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2046.html

### ALAS2023-2026-2047（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2047](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2047.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `wget`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-58469
- **概要:** GNU Wget through 1.25.0, fixed in commit 37a40fc, contains a heap buffer underread vulnerability in the clean_metalink_string() function within src/metalink.c that allows a malicious server to trigger memory corruption by serving a Metalink document containing a whitespace-only URL. Attackers can cause the function to decrement a pointer past the start of the buffer when processing an all-whitespace Metalink URL, potentially leading to abnormal program behavior. (CVE-2026-58469)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2047.html

### ALAS2023-2026-2048（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2048](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2048.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `dotnet9.0`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-47303, CVE-2026-47304, CVE-2026-50524, CVE-2026-50525, CVE-2026-50526, CVE-2026-50527, CVE-2026-50648, CVE-2026-50649, CVE-2026-50651, CVE-2026-57108
- **概要:** Authentication bypass by assumed-immutable data in ASP.NET Core allows an authorized attacker to elevate privileges over a network. (CVE-2026-47303) Improper verification of cryptographic signature in .NET allows an unauthorized attacker to bypass a security feature over a network. (CVE-2026-47304) Improper validation of specified type of input in .NET Framework allows an unauthorized attacker to deny service over a network. (CVE-2026-50524) Allocation of resources without limits or throttling i…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2048.html

### ALAS2023-2026-2049（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2049](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2049.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `python-urwid`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-9323
- **概要:** The urwid web display backend (urwid/display/web.py) generates web session identifiers (urwid_id) in Screen.start() by concatenating two random.randrange(10**9) calls that use Python's Mersenne Twister PRNG, which is not cryptographically secure. Each call consumes approximately 30 bits of PRNG state, and the Mersenne Twister internal state is approximately 19,937 bits, so an attacker who observes approximately 334 session IDs (for example via the X-Urwid-ID HTTP response header) can fully recon…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2049.html

### ALAS2023-2026-2050（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2050](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2050.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `perl-Date-Manip`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-60074, CVE-2026-60075
- **概要:** Date::Manip versions through 6.99 for Perl return corrupted dates via non-ASCII decimal digits that pass the numeric range tests in check. The parse regexes capture year, month and day with the `\d` shorthand, which on a character string matches the whole Unicode decimal digit property `\p{Nd}` and not just `[0-9]`. Date::Manip::Base::check then validates the captured fields with numeric comparisons alone (`$y<1 || $y>9999`, `$m<1 || $m>12`, `$d<1 || $d>$days`), and _parse_check stores the numif…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2050.html

### ALAS2023-2026-2053（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2053](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2053.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `freerdp`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-64620, CVE-2026-64621
- **概要:** FreeRDP before 3.28.0 (affected <=3.27.1) contains a heap-based buffer overflow in crypto_rsa_common() (libfreerdp/crypto/crypto.c). The function writes the modular-exponentiation result into the caller's output buffer via BN_bn2bin() and only afterward checks output_length > out_length, so out-of-bounds bytes are written before the bounds check. On the server side, when a client selects RDP Standard Security, the encrypted client random is decrypted into a fixed 32-byte buffer. Because the serv…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2053.html

### ALAS2023-2026-2054（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2054](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2054.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `isns-utils`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-55995
- **概要:** A Double Free vulnerability in open-iscsi allows an unauthenticated MITM attacker to cause DoS. This issue affects open-iscsi: from ? through 56718d4e9d1a4f51c30697b5c0534144bb41c9bb. (CVE-2026-55995)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2054.html

### ALAS2023-2026-2055（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2055](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2055.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `javapackages-bootstrap`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-54399
- **概要:** Uncontrolled Resource Consumption vulnerability in the HTTP/1.1 message parser in Apache HttpComponents Core (5.4.2 and earlier, 5.5-beta1 and earlier) allows an remote attacker to cause a denial of service through memory exhaustion by sending messages with excessive number of headers / excessive header length (CVE-2026-54399)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2055.html

### ALAS2023-2026-2056（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2056](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2056.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `libssh2`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-66032, CVE-2026-66034
- **概要:** libssh2 through 1.11.1, fixed in commit 5e47761, contains a double-free vulnerability in the sftp_open() function in src/sftp.c that allows a malicious SSH server to corrupt the heap of any authenticated client opening an SFTP session. When a server responds to SSH_FXP_OPEN with SSH_FXP_STATUS containing FX_OK, the response data buffer is freed, and if a subsequent sftp_packet_require() call returns a specific error such as LIBSSH2_ERROR_CHANNEL_PACKET_EXCEEDED, the same pointer is freed a secon…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2056.html

### ALAS2023-2026-2057（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2057](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2057.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel6.12`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-45944, CVE-2026-46093, CVE-2026-53005, CVE-2026-53027, CVE-2026-53365, CVE-2026-53392, CVE-2026-53402, CVE-2026-63970, CVE-2026-64024, CVE-2026-64077, CVE-2026-64187, CVE-2026-64189, CVE-2026-64192, CVE-2026-64227, CVE-2026-64265 …ほか277件（合計292件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: iommu/vt-d: Clear Present bit before tearing down context entry (CVE-2026-45944) In the Linux kernel, the following vulnerability has been resolved: mm/vmalloc: take vmap_purge_lock in shrinker (CVE-2026-46093) In the Linux kernel, the following vulnerability has been resolved: af_unix: Drop all SCM attributes for SOCKMAP. (CVE-2026-53005) In the Linux kernel, the following vulnerability has been resolved: fs/ntfs3: fix missing…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2057.html

### ALAS2023-2026-2058（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2058](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2058.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `kernel`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-53392, CVE-2026-53393, CVE-2026-53400, CVE-2026-53402, CVE-2026-63806, CVE-2026-63810, CVE-2026-63826, CVE-2026-63829, CVE-2026-64077, CVE-2026-64187, CVE-2026-64189, CVE-2026-64266, CVE-2026-64279, CVE-2026-64296, CVE-2026-64298 …ほか175件（合計190件。全件はALASページ参照）
- **概要:** In the Linux kernel, the following vulnerability has been resolved: NFSv4/flexfiles: reject zero filehandle version count (CVE-2026-53392) In the Linux kernel, the following vulnerability has been resolved: nfsd: reset write verifier on deferred writeback errors (CVE-2026-53393) In the Linux kernel, the following vulnerability has been resolved: i2c: core: fix adapter registration race Adapters can be looked up based on their id using i2c_get_adapter() which takes a reference to the embedded str…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2058.html

### ALAS2023-2026-2059（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2059](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2059.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `nodejs24`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-13149, CVE-2026-13697, CVE-2026-14643, CVE-2026-15157, CVE-2026-16728, CVE-2026-16729, CVE-2026-53655, CVE-2026-56846, CVE-2026-56847, CVE-2026-56848, CVE-2026-56850, CVE-2026-58039, CVE-2026-58040, CVE-2026-58041, CVE-2026-58042 …ほか11件（合計26件。全件はALASページ参照）
- **概要:** brace-expansion through 5.0.6 is vulnerable to denial of service. The expand() function exhibits exponential-time complexity in the number of consecutive non-expanding '{}' brace groups. An attacker who passes a crafted string to expand(), directly or transitively, can cause significant CPU consumption and event-loop blocking. The max option does not mitigate this, as it bounds the output size rather than the recursion work. (CVE-2026-13149) undici's cache interceptor mishandles malformed Cache-…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2059.html

### ALAS2023-2026-2060（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2060](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2060.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `nodejs22`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-13149, CVE-2026-15157, CVE-2026-16728, CVE-2026-16729, CVE-2026-50812, CVE-2026-56846, CVE-2026-56847, CVE-2026-56848, CVE-2026-56850, CVE-2026-58039, CVE-2026-58040, CVE-2026-58042, CVE-2026-58043, CVE-2026-58044, CVE-2026-58045 …ほか7件（合計22件。全件はALASページ参照）
- **概要:** brace-expansion through 5.0.6 is vulnerable to denial of service. The expand() function exhibits exponential-time complexity in the number of consecutive non-expanding '{}' brace groups. An attacker who passes a crafted string to expand(), directly or transitively, can cause significant CPU consumption and event-loop blocking. The max option does not mitigate this, as it bounds the output size rather than the recursion work. (CVE-2026-13149) undici does not validate the type property of a duck-t…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2060.html

### ALAS2023-2026-2062（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2062](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2062.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `docker`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-56852
- **概要:** A norm.Iter can enter an infinite loop when handling input containing invalid UTF-8 bytes. (CVE-2026-56852)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2062.html

### ALAS2023-2026-2063（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2063](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2063.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `containerd`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-56852
- **概要:** A norm.Iter can enter an infinite loop when handling input containing invalid UTF-8 bytes. (CVE-2026-56852)
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2063.html

### ALAS2023-2026-2064（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2064](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2064.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `rust-cargo-c`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-53584, CVE-2026-53585, CVE-2026-53587, CVE-2026-66032, CVE-2026-66033, CVE-2026-66034, CVE-2026-66035
- **概要:** libgit2 Submodule path traversal (CVE-2026-53584) Unbounded Memory Allocation via Delta Object Result-Size Header (CVE-2026-53585) libgit2 version 1.9.4 and below is vulnerable to a heap out-of-bounds read in set_data() in src/libgit2/transports/smart_pkt.c. The vulnerable code uses a fixed-size strncmp (smart_pkt.c:239) against the unvalidated capability buffer of a smart-protocol pkt-line. When the bytes following the pkt-line in the contiguous receive buffer happen to continue with "ct-format…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2064.html

### ALAS2023-2026-2065（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2065](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2065.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `rust`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-45784, CVE-2026-50185, CVE-2026-53583, CVE-2026-53584, CVE-2026-53585, CVE-2026-53586, CVE-2026-53587
- **概要:** rust-openssl provides OpenSSL bindings for the Rust programming language. From 0.10.50 until 0.10.80, CipherCtxRef::cipher_update_inplace in openssl/src/cipher_ctx.rs incorrectly sized output buffers when used with AES key-wrap-with-padding ciphers EVP_aes_{128,192,256}_wrap_pad. For a non-multiple-of-8 input, OpenSSL writes up to 7 bytes past the end of the caller's buffer or Vec, producing attacker-controllable heap corruption when the plaintext length is attacker-influenced. This issue is fix…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2065.html

### ALAS2023-2026-2066（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2066](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2066.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `iscsi-initiator-utils`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-44943, CVE-2026-44944
- **概要:** An Improper Limitation of a Pathname to a Restricted Directory ('Path Traversal') vulnerability in open-iscsi allows remote MITM attackers to create root-owned files outside the database and inject lines into the record. This issue affects open-iscsi: from through 668ca1df9c9a1e9bdd5c999ae1d67c9c8909237e. (CVE-2026-44943) An Incorrect Authorization vulnerability in open-iscsi allows unprivilidged local users to use the isscsiuio control socket. This issue affects open-iscsi: from ? through 668ca…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2066.html

### ALAS2023-2026-2067（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2067](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2067.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `jackson-core`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-18401
- **概要:** The non-blocking (asynchronous) JSON parser in jackson-core does not enforce the maxNumberLength constraint defined in StreamReadConstraints (default: 1000 characters). An attacker able to submit JSON to an application that uses the async parser API can supply a number token of arbitrary length, leading to excessive memory allocation and potential CPU exhaustion, resulting in a denial of service. The synchronous parser enforces this limit correctly, so the constraint is applied inconsistently de…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2067.html

### ALAS2023-2026-2068（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2068](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2068.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `gnome-remote-desktop`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-18358
- **概要:** A flaw was found in gnome-remote-desktop as shipped in Red Hat Enterprise Linux. When the daemon is running in system mode with RDP enabled, the incoming connection handler bypasses the connection throttler, allowing an unauthenticated remote attacker to open many parallel pre-authentication connections to the RDP listener. This can accumulate accepted sockets and pending routing-token operations until timeout, exhausting resources and preventing legitimate users from establishing RDP sessions.…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2068.html

### ALAS2023-2026-2069（Important（重要））

- **ALAS ID:** [ALAS2023-2026-2069](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2069.html)
- **重大度:** Important（重要）
- **対象パッケージ:** `firefox`
- **公開日:** Mon, 17 Aug 2026 20:50:00 GMT
- **関連CVE（CVE＝共通脆弱性識別子）:** CVE-2026-16349, CVE-2026-16350, CVE-2026-16351, CVE-2026-16352, CVE-2026-16353, CVE-2026-16354, CVE-2026-16355, CVE-2026-16356, CVE-2026-16357, CVE-2026-16358, CVE-2026-16359, CVE-2026-16360, CVE-2026-16361, CVE-2026-16362, CVE-2026-16363 …ほか16件（合計31件。全件はALASページ参照）
- **概要:** Same-origin policy bypass in the DOM: Navigation component. This vulnerability was fixed in Firefox 153, Firefox ESR 115.38, and Firefox ESR 140.13. (CVE-2026-16349) Incorrect boundary conditions in the Audio/Video: cubeb component. This vulnerability was fixed in Firefox 153, Firefox ESR 115.38, and Firefox ESR 140.13. (CVE-2026-16350) Sandbox escape due to use-after-free in the DOM: Navigation component. This vulnerability was fixed in Firefox 153, Firefox ESR 115.38, and Firefox ESR 140.13. (…（原文はALASページ参照）
- **対処方法:** 上記共通手順（`sudo dnf check-release-update` 等）でパッチ適用状況を確認してください。本タスクでは `sudo` を要するため実行していません。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2069.html

---

## Medium / Low（参考・詳細割愛）

**Medium（3件）:** [ALAS2023-2026-2051](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2051.html)（python-jwt）, [ALAS2023-2026-2052](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2052.html)（python-idna）, [ALAS2023-2026-2061](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2061.html)（spice-vdagent）

---

## 出典

- AWS公式 ALAS RSSフィード（AL2023）
- 各アドバイザリの詳細は上記リンク先の公式ページをご参照ください。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
