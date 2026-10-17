# AL2023 セキュリティアドバイザリ週次レポート（2026-10-17）

作成日: 2026-10-17 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS を情報収集目的で監視した結果です。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 0 |
| Important | 56 |
| Medium | 21 |
| Low | 1 |

対象期間: 2026-10-03 〜 2026-10-17

> ⚠️ Important が56件あり、詳細取得の上限（30件）のため先頭30件のみ詳細を取得（`reportableTruncated=true`）。残り26件は未取得です。

---

## 注目アドバイザリ（取得済み30件・パッケージ別）

- **[ALAS2023-2026-3233](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3233.html)** Important / `mount-s3` / CVE 1件 — Improper handling of HPACK dynamic table size updates in the AWS Common Runtime aws-c-http library might allow a remote threat actor operating a server to cause memory co…
- **[ALAS2023-2026-3234](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3234.html)** Important / `mariadb1011` / CVE 13件 — A flaw was found in MariaDB. An authenticated user with permission to use the CONNECT storage engine can exploit an incorrect boundary check when handling DOS table types…
- **[ALAS2023-2026-3235](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3235.html)** Important / `mariadb114` / CVE 13件 — A flaw was found in MariaDB. An authenticated user with permission to use the CONNECT storage engine can exploit an incorrect boundary check when handling DOS table types…
- **[ALAS2023-2026-3236](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3236.html)** Important / `mariadb118` / CVE 13件 — A flaw was found in MariaDB. An authenticated user with permission to use the CONNECT storage engine can exploit an incorrect boundary check when handling DOS table types…
- **[ALAS2023-2026-3237](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3237.html)** Important / `mariadb123` / CVE 13件 — A flaw was found in MariaDB. An authenticated user with permission to use the CONNECT storage engine can exploit an incorrect boundary check when handling DOS table types…
- **[ALAS2023-2026-3238](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3238.html)** Important / `gnutls` / CVE 1件 — A hostname verification bypass in GnuTLS v3.8.13 allows attackers to circumvent the Common Name fallback mechanism and eavesdrop on communications via a crafted certifica…
- **[ALAS2023-2026-3221](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3221.html)** Important / `bind` / CVE 0件 — Amazon Linux–vended DNS resolvers shipped with an older DNSSEC root signing key. For hosts configured with DNSSEC validation enabled, this could result in DNS resolution …
- **[ALAS2023-2026-3222](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3222.html)** Important / `unbound` / CVE 0件 — Amazon Linux–vended DNS resolvers shipped with an older DNSSEC root signing key. For hosts configured with DNSSEC validation enabled, this could result in DNS resolution …
- **[ALAS2023-2026-3223](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3223.html)** Important / `dnsmasq` / CVE 0件 — Amazon Linux–vended DNS resolvers shipped with an older DNSSEC root signing key. For hosts configured with DNSSEC validation enabled, this could result in DNS resolution …
- **[ALAS2023-2026-3224](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3224.html)** Important / `systemd` / CVE 0件 — Amazon Linux–vended DNS resolvers shipped with an older DNSSEC root signing key. For hosts configured with DNSSEC validation enabled, this could result in DNS resolution …
- **[ALAS2023-2026-3151](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3151.html)** Important / `tomcat11` / CVE 24件 — Improper Access Control, Incorrect Authorization vulnerability in Apache Tomcat leads to security constraint bypass if a constraint for a longer path is specified before …
- **[ALAS2023-2026-3152](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3152.html)** Important / `flatpak-builder` / CVE 1件 — When use-git-am: true is enabled for a patch source, flatpak-builder invokes git am without disabling git hooks. A malicious source can include a post-applypatch hook, wh…
- **[ALAS2023-2026-3155](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3155.html)** Important / `python-pymongo` / CVE 1件 — A flaw was found in pymongo. An integer overflow exists in the bundled native extension for Binary JSON (BSON) document encoding when processing an unusually large amount…
- **[ALAS2023-2026-3156](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3156.html)** Important / `sudo` / CVE 1件 — A flaw was found in sudo. When sudoers rules use NOTBEFORE or NOTAFTER time-based access restrictions with timestamps that omit the trailing 'Z' timezone indicator, the t…
- **[ALAS2023-2026-3157](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3157.html)** Important / `rsyslog` / CVE 1件 — rsyslog's omfile dynaFile facility intentionally allows templates to generate flexible output paths. This supports valid deployments that route logs into different direct…
- **[ALAS2023-2026-3158](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3158.html)** Important / `python-jwcrypto` / CVE 1件 — A flaw was found in jwcrypto. The JWK.import_key() function validates the key_ops JWK member for duplicate values using an algorithm with O(n^2) time complexity, and the …
- **[ALAS2023-2026-3159](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3159.html)** Important / `python-hpack` / CVE 1件 — A flaw was found in hpack, an HTTP/2 Header Encoding for Python. Unbounded variable integer decoding can lead to excessive computation when processing specially crafted, …
- **[ALAS2023-2026-3161](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3161.html)** Important / `php8.2` / CVE 11件 — The mysqlnd wire protocol parser reads fields out of server packets before checking that the packet still holds enough bytes for them. A malicious or compromised MySQL se…
- **[ALAS2023-2026-3162](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3162.html)** Important / `php8.3` / CVE 11件 — The mysqlnd wire protocol parser reads fields out of server packets before checking that the packet still holds enough bytes for them. A malicious or compromised MySQL se…
- **[ALAS2023-2026-3163](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3163.html)** Important / `php8.4` / CVE 11件 — The mysqlnd wire protocol parser reads fields out of server packets before checking that the packet still holds enough bytes for them. A malicious or compromised MySQL se…
- **[ALAS2023-2026-3164](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3164.html)** Important / `php8.5` / CVE 11件 — The mysqlnd wire protocol parser reads fields out of server packets before checking that the packet still holds enough bytes for them. A malicious or compromised MySQL se…
- **[ALAS2023-2026-3165](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3165.html)** Important / `tomcat10` / CVE 13件 — Improper Check for Certificate Revocation vulnerability in Apache Tomcat. Both the OpenSSL and OpenSSL-FFM TLS implementations ignore CRLs when certificate uses a keystor…
- **[ALAS2023-2026-3166](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3166.html)** Important / `tomcat9` / CVE 13件 — Improper Check for Certificate Revocation vulnerability in Apache Tomcat. Both the OpenSSL and OpenSSL-FFM TLS implementations ignore CRLs when certificate uses a keystor…
- **[ALAS2023-2026-3167](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3167.html)** Important / `tomcat-native` / CVE 3件 — Buffer over-read vulnerability in Apache Tomcat Native during the TLS handshake permits a malicious user to trigger a DoS via a JVM crash. This issue affects Apache Tomca…
- **[ALAS2023-2026-3169](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3169.html)** Important / `rpcbind` / CVE 3件 — A stack-based buffer overflow was found in rpcbind's rpcinfo utility. When querying a remote rpcbind service with `rpcinfo -l`, address information returned by the server…
- **[ALAS2023-2026-3170](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3170.html)** Important / `rust` / CVE 1件 — gitoxide gix-fs before 0.23.0 contains a path validation bypass vulnerability in the worktree checkout mechanism that allows attackers to escape the worktree directory vi…
- **[ALAS2023-2026-3171](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3171.html)** Important / `python3.14-pip` / CVE 1件 — urllib3 is an HTTP client library for Python. From 1.10.3 until 2.8.0, the HTTPResponse.read_chunked and HTTPResponse.stream methods can allocate unbounded memory because…
- **[ALAS2023-2026-3172](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3172.html)** Important / `python3.13-pip` / CVE 1件 — urllib3 is an HTTP client library for Python. From 1.10.3 until 2.8.0, the HTTPResponse.read_chunked and HTTPResponse.stream methods can allocate unbounded memory because…
- **[ALAS2023-2026-3173](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3173.html)** Important / `python3.12-pip` / CVE 1件 — urllib3 is an HTTP client library for Python. From 1.10.3 until 2.8.0, the HTTPResponse.read_chunked and HTTPResponse.stream methods can allocate unbounded memory because…
- **[ALAS2023-2026-3174](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3174.html)** Important / `python3.11-pip` / CVE 1件 — urllib3 is an HTTP client library for Python. From 1.10.3 until 2.8.0, the HTTPResponse.read_chunked and HTTPResponse.stream methods can allocate unbounded memory because…

補足:
- ALAS2023-2026-3221〜3224（bind / unbound / dnsmasq / systemd）は CVE 番号なし。DNSSEC（DNS応答の改ざん検知機能）のルート署名鍵が古いまま同梱されていた問題で、DNSSEC検証を有効にしている環境のみ影響します。
- mariadb 4件（1011/114/118/123）は同一CVE群、php 4件（8.2〜8.5）も同一CVE群、python pip 4件（3.11〜3.14）は CVE-2026-97689（urllib3 の巨大メモリ確保）で共通です。

## 対処方法

`sudo dnf check-release-update` で新リリース確認、`sudo dnf update <パッケージ名>` で更新します。いずれも管理者権限（sudo）が必要なため、**本タスクでは実行していません**。適用は管理者権限を持つ方が行ってください。

---

## 🎯 CVSS・OWASPスコア

> 📌 上の「Important」は **Amazon Linux 独自の重大度ラベル** で、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム＝深刻度を0.0〜10.0で表す国際基準）とは **別物** です。CVSSは **v3.1** で統一し NVD（米国の脆弱性DB）から取得しました。*Secondary* は **発行元(CNA)の採点**、*Primary* は **NVD自身の採点** です。今回のCVEの大半は NVD 未採点で CNA 値のみです。

### ① CVSS v3.1（公式値・全64 CVE）

| CVE | 対象パッケージ | CVSS v3.1 | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-12043 | mount-s3 | **8.8** | HIGH | Secondary（CNA採点: CNA識別子 ff89ba41…・名称未確認） | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-107815 | mariadb1011, mariadb114, mariadb118, mariadb123 | **8.5** | HIGH | Secondary（CNA採点: GitHub） | `AV:N/AC:H/PR:L/UI:N/S:C/C:H/I:H/A:H` |
| CVE-2026-107816 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.4** | MEDIUM | Secondary（CNA採点: GitHub） | `AV:N/AC:L/PR:L/UI:N/S:C/C:L/I:N/A:L` |
| CVE-2026-107817 | mariadb1011, mariadb114, mariadb118, mariadb123 | **4.4** | MEDIUM | Secondary（CNA採点: GitHub） | `AV:L/AC:L/PR:N/UI:R/S:U/C:L/I:N/A:L` |
| CVE-2026-107821 | mariadb1011, mariadb114, mariadb118, mariadb123 | **8.0** | HIGH | Secondary（CNA採点: GitHub） | `AV:N/AC:H/PR:H/UI:N/S:C/C:H/I:H/A:H` |
| CVE-2026-107822 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.4** | MEDIUM | Secondary（CNA採点: GitHub） | `AV:N/AC:H/PR:H/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-107823 | mariadb1011, mariadb114, mariadb118, mariadb123 | **7.2** | HIGH | Secondary（CNA採点: GitHub） | `AV:N/AC:L/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-47023 | mariadb1011, mariadb114, mariadb118, mariadb123 | **4.9** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:N/AC:L/PR:H/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-47064 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.5** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-60184 | mariadb1011, mariadb114, mariadb118, mariadb123 | **4.4** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:N/AC:H/PR:H/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-60331 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.4** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:L/AC:H/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-60585 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.6** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:N/AC:H/PR:H/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-60747 | mariadb1011, mariadb114, mariadb118, mariadb123 | **6.2** | MEDIUM | Secondary（CNA採点: Oracle） | `AV:L/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-61081 | mariadb1011, mariadb114, mariadb118, mariadb123 | **2.7** | LOW | Secondary（CNA採点: Oracle） | `AV:N/AC:L/PR:H/UI:N/S:U/C:L/I:N/A:N` |
| CVE-2026-88647 | gnutls | **9.1** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-65182 | tomcat11 | **9.1** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-65183 | tomcat11 | **8.1** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-65637 | tomcat11 | **9.8** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-65905 | tomcat11 | **9.8** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-65927 | tomcat11 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-66422 | tomcat11 | **8.1** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:H/A:H` |
| CVE-2026-68525 | tomcat11 | **9.1** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-68569 | tomcat11 | **8.1** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-68763 | tomcat11 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-73180 | tomcat11 | **6.8** | MEDIUM | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:H/PR:L/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-73581 | tomcat11, tomcat10, tomcat9 | **6.5** | MEDIUM | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N` |
| CVE-2026-75973 | tomcat11, tomcat10, tomcat9 | **7.3** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L` |
| CVE-2026-76183 | tomcat11, tomcat10, tomcat9 | **9.8** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-77756 | tomcat11, tomcat10, tomcat9 | **3.7** | LOW | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:N/A:L` |
| CVE-2026-77762 | tomcat11, tomcat10, tomcat9 | **8.1** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-77791 | tomcat11, tomcat10, tomcat9 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-78383 | tomcat11, tomcat10, tomcat9 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-78437 | tomcat11, tomcat10, tomcat9 | **7.3** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:L` |
| CVE-2026-79677 | tomcat11, tomcat10, tomcat9 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-86248 | tomcat11, tomcat10, tomcat9 | **9.8** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-86350 | tomcat11, tomcat10, tomcat9 | **9.1** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-87022 | tomcat11, tomcat10, tomcat9 | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:H/A:N` |
| CVE-2026-32990 | tomcat11 | **5.3** | MEDIUM | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N` |
| CVE-2026-41293 | tomcat11, tomcat10, tomcat9 | **9.8** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-86320 | flatpak-builder | **7.8** | HIGH | Secondary（CNA採点: Red Hat） | `AV:L/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-96749 | python-pymongo | **8.4** | HIGH | Secondary（CNA採点: MongoDB） | `AV:L/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-96512 | sudo | **7.8** | HIGH | Secondary（CNA採点: Red Hat） | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-92709 | 未取得（NVD未掲載） | - | - | - |
| CVE-2026-92091 | python-jwcrypto | **5.9** | MEDIUM | Secondary（CNA採点: Red Hat） | `AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-59980 | python-hpack | v4.0のみ 6.3 MEDIUM（Secondary） | - | - | v3.1なし |
| CVE-2025-1218 | php8.2, php8.3, php8.4, php8.5 | **3.4** | LOW | Secondary（CNA採点: PHP） | `AV:A/AC:H/PR:N/UI:N/S:C/C:L/I:N/A:N` |
| CVE-2025-14181 | php8.2, php8.3, php8.4, php8.5 | **6.5** | MEDIUM | Secondary（CNA採点: PHP） | `AV:N/AC:H/PR:N/UI:N/S:U/C:N/I:L/A:H` |
| CVE-2026-6103 | php8.2, php8.3, php8.4, php8.5 | **4.3** | MEDIUM | Secondary（CNA採点: PHP） | `AV:L/AC:L/PR:N/UI:N/S:C/C:N/I:L/A:N` |
| CVE-2026-91765 | php8.2, php8.3, php8.4, php8.5 | **7.5** | HIGH | Secondary（CNA採点: PHP） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-91766 | php8.2, php8.3, php8.4, php8.5 | **5.9** | MEDIUM | Secondary（CNA採点: PHP） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:N/A:N` |
| CVE-2026-91767 | php8.2, php8.3, php8.4, php8.5 | **6.5** | MEDIUM | Secondary（CNA採点: PHP） | `AV:A/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N` |
| CVE-2026-91768 | php8.2, php8.3, php8.4, php8.5 | **6.5** | MEDIUM | Secondary（CNA採点: PHP） | `AV:A/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N` |
| CVE-2026-91769 | php8.2, php8.3, php8.4, php8.5 | **4.3** | MEDIUM | Secondary（CNA採点: PHP） | `AV:A/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N` |
| CVE-2026-92842 | php8.2, php8.3, php8.4, php8.5 | **5.9** | MEDIUM | Secondary（CNA採点: PHP） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:N/A:N` |
| CVE-2026-93682 | php8.2, php8.3, php8.4, php8.5 | **5.8** | MEDIUM | Secondary（CNA採点: PHP） | `AV:N/AC:L/PR:N/UI:N/S:C/C:L/I:N/A:N` |
| CVE-2018-1000007 | php8.2, php8.3, php8.4, php8.5 | **9.8** | CRITICAL | Primary（NVD採点） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-86243 | tomcat-native | **7.5** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-86246 | tomcat-native | **9.1** | CRITICAL | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-86247 | tomcat-native | **7.4** | HIGH | Secondary（CNA採点: CNA識別子 134c704f…・名称未確認） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-16277 | rpcbind | **6.5** | MEDIUM | Secondary（CNA採点: Red Hat） | `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H` |
| CVE-2026-16461 | rpcbind | **6.5** | MEDIUM | Secondary（CNA採点: Red Hat） | `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:N/A:H` |
| CVE-2026-94640 | rpcbind | **7.5** | HIGH | Secondary（CNA採点: Red Hat） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-100419 | rust | **7.0** | HIGH | Secondary（CNA採点: VulnCheck） | `AV:L/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-97689 | python3.14-pip, python3.13-pip, python3.12-pip, python3.11-pip | **7.5** | HIGH | Primary（NVD採点） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |

- `AV:N`=ネットワーク経由、`AV:L`=端末上、`PR:N`=権限不要、`UI:R`=利用者の操作が必要。
- CVE-2026-12043 / 96749 は v4.0 も併記ありますが、v3.1 と v4.0 は数値比較不可のため本表は v3.1 のみ。CVE-2026-59980 は v4.0（6.3 MEDIUM, CNA=GitHub）のみで v3.1 なし。CVE-2026-92709 は NVD 未掲載のため未取得（数値は創作しません）。
- CVE-2018-1000007 は php 系アドバイザリに含まれる古いCVE（curl関連）です。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology は **尤度（起きやすさ）×影響度（被害の大きさ）** を0〜9で評価し、LOW(<3)/MEDIUM(3〜<6)/HIGH(6以上) の組合せで総合判定します。**公式値は存在せず、以下はすべて「推定」** です。CVSS v3.1 ベクタから機械的に換算（攻撃元区分・必要権限・攻撃難度→尤度の要因、C/I/A→影響度の要因。skill=5, motive=4, awareness=6, detection=3, 追跡可能性=7 を固定）しました。業務影響（ビジネス）は環境依存のため採点していません。

| CVE | 尤度 | 影響度（技術） | 総合（推定） | 換算元 |
|---|---|---|---|---|
| CVE-2026-12043 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-107815 | 4.5 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:L 等から機械換算 |
| CVE-2026-107816 | 5.25 MEDIUM | 2.75 LOW | **Low** | AV:N/AC:L/PR:L 等から機械換算 |
| CVE-2026-107817 | 4.5 MEDIUM | 2.75 LOW | **Low** | AV:L/AC:L/PR:N 等から機械換算 |
| CVE-2026-107821 | 4.12 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:H 等から機械換算 |
| CVE-2026-107822 | 4.12 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:H 等から機械換算 |
| CVE-2026-107823 | 4.88 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:L/PR:H 等から機械換算 |
| CVE-2026-47023 | 4.88 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:L/PR:H 等から機械換算 |
| CVE-2026-47064 | 5.25 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:L/PR:L 等から機械換算 |
| CVE-2026-60184 | 4.12 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:H/PR:H 等から機械換算 |
| CVE-2026-60331 | 3.75 MEDIUM | 7.0 HIGH | **High** | AV:L/AC:H/PR:H 等から機械換算 |
| CVE-2026-60585 | 4.12 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:H 等から機械換算 |
| CVE-2026-60747 | 4.5 MEDIUM | 4.0 MEDIUM | **Medium** | AV:L/AC:L/PR:N 等から機械換算 |
| CVE-2026-61081 | 4.88 MEDIUM | 2.75 LOW | **Low** | AV:N/AC:L/PR:H 等から機械換算 |
| CVE-2026-88647 | 6.0 HIGH | 5.5 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-65182 | 6.0 HIGH | 5.5 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-65183 | 5.25 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-65637 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-65905 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-65927 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-66422 | 5.25 MEDIUM | 5.5 MEDIUM | **Medium** | AV:N/AC:L/PR:L 等から機械換算 |
| CVE-2026-68525 | 6.0 HIGH | 5.5 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-68569 | 5.25 MEDIUM | 5.5 MEDIUM | **Medium** | AV:N/AC:L/PR:L 等から機械換算 |
| CVE-2026-68763 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-73180 | 4.5 MEDIUM | 5.5 MEDIUM | **Medium** | AV:N/AC:H/PR:L 等から機械換算 |
| CVE-2026-73581 | 6.0 HIGH | 3.25 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-75973 | 6.0 HIGH | 3.25 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-76183 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-77756 | 5.25 MEDIUM | 2.5 LOW | **Low** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-77762 | 5.25 MEDIUM | 7.0 HIGH | **High** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-77791 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-78383 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-78437 | 6.0 HIGH | 3.25 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-79677 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86248 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86350 | 6.0 HIGH | 5.5 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-87022 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-32990 | 6.0 HIGH | 2.75 LOW | **Medium** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-41293 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86320 | 4.5 MEDIUM | 7.0 HIGH | **High** | AV:L/AC:L/PR:N 等から機械換算 |
| CVE-2026-96749 | 4.5 MEDIUM | 7.0 HIGH | **High** | AV:L/AC:L/PR:N 等から機械換算 |
| CVE-2026-96512 | 4.5 MEDIUM | 7.0 HIGH | **High** | AV:L/AC:L/PR:L 等から機械換算 |
| CVE-2026-92709 | 未取得 | - | - |
| CVE-2026-92091 | 5.25 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-59980 | 算出不可 | - | - | v3.1ベクタなし |
| CVE-2025-1218 | 4.0 MEDIUM | 2.75 LOW | **Low** | AV:A/AC:H/PR:N 等から機械換算 |
| CVE-2025-14181 | 5.25 MEDIUM | 4.5 MEDIUM | **Medium** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-6103 | 4.5 MEDIUM | 3.0 MEDIUM | **Medium** | AV:L/AC:L/PR:N 等から機械換算 |
| CVE-2026-91765 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-91766 | 5.25 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-91767 | 4.75 MEDIUM | 4.0 MEDIUM | **Medium** | AV:A/AC:L/PR:N 等から機械換算 |
| CVE-2026-91768 | 4.75 MEDIUM | 4.0 MEDIUM | **Medium** | AV:A/AC:L/PR:N 等から機械換算 |
| CVE-2026-91769 | 4.75 MEDIUM | 2.75 LOW | **Low** | AV:A/AC:L/PR:N 等から機械換算 |
| CVE-2026-92842 | 5.25 MEDIUM | 4.0 MEDIUM | **Medium** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-93682 | 6.0 HIGH | 2.75 LOW | **Medium** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2018-1000007 | 6.0 HIGH | 7.0 HIGH | **Critical** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86243 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86246 | 6.0 HIGH | 5.5 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-86247 | 5.25 MEDIUM | 5.5 MEDIUM | **Medium** | AV:N/AC:H/PR:N 等から機械換算 |
| CVE-2026-16277 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-16461 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-94640 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |
| CVE-2026-100419 | 3.75 MEDIUM | 7.0 HIGH | **High** | AV:L/AC:H/PR:N 等から機械換算 |
| CVE-2026-97689 | 6.0 HIGH | 4.0 MEDIUM | **High** | AV:N/AC:L/PR:N 等から機械換算 |

### ③ OWASP Top 10:2025 対応

Top 10 は **Webアプリ向け** の分類です。NVD の CWE（弱点の種類）を、OWASP公式 Top 10:2025 各カテゴリページの Mapped CWEs 掲載と照合しました。掲載が無いものは「対象外」とし、無理に当てはめていません。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-12043 | CWE-415 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-107815 | CWE-787 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-107816 | CWE-125 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-107817 | CWE-125 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-107821 | CWE-1285 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-107822 | CWE-706, CWE-863 | A01 Broken Access Control |
| CVE-2026-107823 | CWE-116, CWE-144 | A05 Injection |
| CVE-2026-47023 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-47064 | CWE-284 | A01 Broken Access Control |
| CVE-2026-60184 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-60331 | CWE-284 | A01 Broken Access Control |
| CVE-2026-60585 | CWE-284 | A01 Broken Access Control |
| CVE-2026-60747 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-61081 | CWE-200 | A01 Broken Access Control |
| CVE-2026-88647 | CWE-297 | A07 Authentication Failures |
| CVE-2026-65182 | CWE-284, CWE-863 | A01 Broken Access Control |
| CVE-2026-65183 | CWE-367 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-65637 | CWE-20 | A05 Injection |
| CVE-2026-65905 | CWE-294 | A07 Authentication Failures |
| CVE-2026-65927 | CWE-193 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-66422 | CWE-285 | A01 Broken Access Control |
| CVE-2026-68525 | CWE-863 | A01 Broken Access Control |
| CVE-2026-68569 | CWE-287 | A07 Authentication Failures |
| CVE-2026-68763 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-73180 | CWE-613 | A07 Authentication Failures |
| CVE-2026-73581 | CWE-299 | A07 Authentication Failures |
| CVE-2026-75973 | CWE-287 | A07 Authentication Failures |
| CVE-2026-76183 | CWE-289 | A07 Authentication Failures |
| CVE-2026-77756 | CWE-444 | A06 Insecure Design |
| CVE-2026-77762 | CWE-362 | A06 Insecure Design |
| CVE-2026-77791 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-78383 | CWE-770 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-78437 | CWE-459 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-79677 | CWE-1025, CWE-772 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-86248 | CWE-287 | A07 Authentication Failures |
| CVE-2026-86350 | CWE-444 | A06 Insecure Design |
| CVE-2026-87022 | CWE-130 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-32990 | CWE-20 | A05 Injection |
| CVE-2026-41293 | CWE-20 | A05 Injection |
| CVE-2026-86320 | CWE-94 | A05 Injection |
| CVE-2026-96749 | CWE-190 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-96512 | CWE-863 | A01 Broken Access Control |
| CVE-2026-92709 | - | 未取得 |
| CVE-2026-92091 | CWE-407 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-59980 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2025-1218 | CWE-122 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2025-14181 | CWE-190 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-6103 | CWE-190 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-91765 | CWE-674 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-91766 | CWE-200, CWE-522 | A01 Broken Access Control / A06 Insecure Design |
| CVE-2026-91767 | CWE-122 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-91768 | CWE-1023 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-91769 | CWE-297 | A07 Authentication Failures |
| CVE-2026-92842 | CWE-122, CWE-125 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-93682 | CWE-125 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2018-1000007 | NVD-CWE-noinfo | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-86243 | CWE-126 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-86246 | CWE-1188 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-86247 | CWE-366 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-16277 | CWE-121 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-16461 | CWE-121 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-94640 | CWE-400 | 対象外（Webアプリ向け分類に該当なし） |
| CVE-2026-100419 | CWE-59 | A01 Broken Access Control |
| CVE-2026-97689 | CWE-770 | 対象外（Webアプリ向け分類に該当なし） |

### ④ 今週の優先度（所見）

1. **Tomcat 系（tomcat11 / 10 / 9 / tomcat-native）**: CNA採点でCVSS 9.8 CRITICALが複数（CVE-2026-65637 / 65905 / 76183 / 86248 / 41293 等）。認証不要・ネットワーク経由で、Tomcat を外部公開している環境では最優先。
2. **GnuTLS（CVE-2026-88647, 9.1）**: ホスト名検証の迂回（中間者攻撃で通信を傍受され得る）。TLS通信全般に関わるため優先度高。
3. **mount-s3（CVE-2026-12043, 8.8）**: HPACK処理の不備（二重解放）。悪意あるサーバへ接続した場合に影響。
4. **sudo（CVE-2026-96512, 7.8）/ pymongo（96749, 8.4）**: ローカル権限が前提。共有環境では注意。
5. MariaDB は CONNECT ストレージエンジン等を使う環境のみ影響が大きい（最大 8.5）。
6. 本環境は WSL/Ubuntu のため実運用対象外で、参考情報です。実悪用の有無は今回の取得範囲では未確認です。

> 📚 出典: [ALAS 一覧](https://alas.aws.amazon.com/AL2023/)、NVD API（https://nvd.nist.gov/）、OWASP Risk Rating（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）

---

## その他

- Medium: 21件 / Low: 1件（件数のみ。例: glycin, loupe, device-mapper-persistent-data）
- 一覧の切り詰め: あり（Important 56件中30件のみ詳細取得）

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
