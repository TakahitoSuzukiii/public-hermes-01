作成日: 2026-08-09 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

# AL2023セキュリティアドバイザリ週次まとめ（2026-08-09）— PHP各バージョンCritical脆弱性4件とPython/rcloneのImportant多発

> **ALAS（Amazon Linux Security Center）** とは、AWS が Amazon Linux 向けに公開している公式セキュリティアドバイザリです。本記事は AWS 公式 RSS フィード（`https://alas.aws.amazon.com/AL2023/alas.rss`）を情報源とし、前回収集（2026-08-01）以降に新規公開された **Critical（緊急）** および **Important（重要）** アドバイザリをまとめたものです。

## 今週のサマリ

| 重大度 | 件数 |
|---|---|
| Critical（緊急） | 4 |
| Important（重要） | 80 |
| Medium（中）※件数のみ | 5 |
| Low（低）※件数のみ | 0 |

Important 80件のうち **39件は kernel-livepatch（カーネルライブパッチ）** 関連で、対象 CVE（脆弱性識別子）はいずれも同一の2件でした。可読性のため、本記事では livepatch 分をまとめて1セクションに集約しています。

---

## 🔴 Critical（緊急）アドバイザリ（4件）

いずれも PHP 各バージョンに対する同一の脆弱性で、パッケージ違いのみです。

### ALAS2023-2026-2041〜2044: PHP（8.2 / 8.3 / 8.4 / 8.5）

| ALAS ID | 対象パッケージ |
|---|---|
| [ALAS2023-2026-2041](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2041.html) | php8.5 |
| [ALAS2023-2026-2042](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2042.html) | php8.4 |
| [ALAS2023-2026-2043](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2043.html) | php8.2 |
| [ALAS2023-2026-2044](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2044.html) | php8.3 |

**関連CVE:** CVE-2026-17543, CVE-2026-7260

**概要（要約）:**
- CVE-2026-17543: 攻撃者から渡されたパラメータ内のバックスラッシュ（`\`）のエスケープ処理が不適切なため、攻撃者にとって容易な **SQL インジェクション**（不正なSQL文を混入させ、データベースを不正操作される攻撃）が成立してしまう脆弱性。PHP 8.2系は8.2.33、8.3系は8.3.33、8.4系は8.4.24、8.5系は8.5.9より前のバージョンが対象。
- CVE-2026-7260: phar アーカイブ（PHP独自の圧縮パッケージ形式）内でシンボリックリンク（ファイルへの参照）を循環させることで、無限再帰処理を引き起こしCスタックを枯渇させ、PHPプロセスをクラッシュさせられる脆弱性（サービス拒否＝DoS）。対象バージョンは上記と同一。

**対処方法:** Amazon Linux 上では `sudo dnf check-release-update` および `sudo dnf update php*` 等でパッケージ更新を行うのが基本対処です（`sudo` 権限が必要なため、本タスクでは実行していません。実施は鈴木さんの判断・作業でお願いします）。

**出典:** https://alas.aws.amazon.com/AL2023/alas.rss

---

## 🟠 Important（重要）アドバイザリ

### 通常パッケージ（41件）

| ALAS ID | パッケージ | 主なCVE | 概要（要約） |
|---|---|---|---|
| [1991](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1991.html) | rpm | CVE-2026-44605 | NDBデータベースバックエンドで32ビット演算の未チェックによるヒープバッファオーバーフロー |
| [1993](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1993.html) | vim | CVE-2026-59856/57/58 | PHP補完スクリプトが検索パターンをエスケープせず実行 |
| [1994](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1994.html) | gstreamer1-plugins-bad-free | CVE-2026-12892等 | 細工されたH.264動画でヒープ範囲外読み取り |
| [1995](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1995.html) | python3.9 | CVE-2026-15308等 | HTMLパーサーのCPU DoS、tarfile展開時のフィルタ不備 |
| [1996](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1996.html) | python3.12 | CVE-2026-15308, 4360 | 同上系統 |
| [1997](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1997.html) | python3.13 | CVE-2026-15308, 4360 | 同上系統 |
| [1998](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1998.html) | python3.11 | CVE-2026-1502等 | 同上系統 |
| [1999](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1999.html) | python3.14 | CVE-2026-0864等 | 同上系統 |
| [2000](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2000.html) | python-pyasn1 | CVE-2026-59884等 | BERデコーダのタグID長無制限でCPU DoS |
| [2002](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2002.html) | rclone | CVE-2026-54572, 59733 | シンボリックリンク復元時のターゲット未検証 |
| [2006](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2006.html) | perl-DBI | CVE-2026-15043等 | SQL::Nanoで`<=`/`>=`演算子の判定が逆転 |
| [2007](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2007.html) | perl-YAML-Syck | CVE-2026-13713等 | アンカーノードのuse-after-free/double-free |
| [2008](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2008.html) | nginx | CVE-2026-42533等 | map指令の正規表現キャプチャ変数参照順序に起因する不具合 |
| [2009](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2009.html) | dotnet10.0 | CVE-2026-47300等17件 | ASP.NET Core認証アルゴリズム不備・リソース制限欠如等 |
| [2010](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2010.html) | dotnet8.0 | 同上17件 | 同上 |
| [2011](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2011.html) | valkey | CVE-2026-56684, 63639 | TLS接続処理でuse-after-free、RCEに繋がり得る |
| [2012](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2012.html) | freerdp | CVE-2026-55191等10件 | AVC444バッファ確保でヒープバッファオーバーフロー等 |
| [2013](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2013.html) | python-pillow | CVE-2026-54058等 | McIdas AREA画像読込時のストライド不正でメモリ範囲外アクセス |
| [2014](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2014.html) | kernel6.12 | CVE-2025-40158等39件 | Linuxカーネル多数の修正（ipv6/gpio等） |
| [2015](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2015.html) | python3.13-tornado | CVE-2026-49853等 | リダイレクト時にAuthorizationヘッダ等が残留 |
| [2016](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2016.html) | python-tornado | 同上 | 同上 |
| [2017](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2017.html) | java-1.8.0-amazon-corretto | CVE-2026-46968等9件 | Oracle Java SE（JSSE等）複数脆弱性 |
| [2018](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2018.html) | java-11-amazon-corretto | CVE-2026-46917等10件 | 同上 |
| [2019](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2019.html) | java-26-amazon-corretto | 同系統8件 | 同上 |
| [2020](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2020.html) | java-25-amazon-corretto | 同系統8件 | 同上 |
| [2021](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2021.html) | java-21-amazon-corretto | 同系統8件 | 同上 |
| [2022](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2022.html) | java-17-amazon-corretto | 同系統8件 | 同上 |
| [2023](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2023.html) | runfinch-finch | CVE-2026-39822等5件 | Go言語 os.Root がシンボリックリンクを不適切に辿る等 |
| [2024](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2024.html) | rust-cargo-c | CVE-2026-40034 | gix-submodule で `.gitmodules` のupdateフィールド検証不備 |
| [2026](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2026.html) | python-dulwich | CVE-2026-38974等3件 | SSHホスト鍵未検証、Windowsで任意ファイル書込→RCEに繋がるパス検証不備 |
| [2028](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2028.html) | glib2 | CVE-2026-16118 | xdgmime MIME magicファイル解析でヒープバッファオーバーフロー |
| [2029](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2029.html) | pipewire | CVE-2026-14324等 | RAOPモジュールのContent-Length未制限、alloca()呼び出しの上限欠如 |
| [2030](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2030.html) | cifs-utils | CVE-2026-12505 | cifs.upcallヘルパーがroot権限を安全に降格せず、権限昇格の恐れ |
| [2032](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2032.html) | kernel | CVE-2026-52991 | sched/psi: ファイルクローズとpressure書込のレース修正 |
| [2033](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2033.html) | unbound | CVE-2026-42955等13件 | 「ghost domain names」系攻撃でキャッシュTTL窓が拡張される |
| [2034](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2034.html) | aws-nitro-enclaves-cli | CVE-2026-42327 | rust-opensslがOCSPレスポンダURLをUTF-8未検証のまま文字列化 |
| [2035](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2035.html) | gawk | CVE-2026-40467等3件 | do_getline_redir()でのuse-after-free、整数オーバーフロー等 |
| [2036](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2036.html) | ansible-core | CVE-2026-16493 | git clone実行時に`--`区切りが無く、コレクション取得先URLでコマンド注入の恐れ |
| [2037](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2037.html) | 7zip | CVE-2026-14266 | ZDI-26-444記載の脆弱性（p7zip→7zip移行に伴う分類） |
| [2039](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2039.html) | libreswan | CVE-2026-12413等3件 | 不正形式のIKEv2フラグメントでplutoデーモンがクラッシュ（DoS） |
| [2040](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2040.html) | bind | CVE-2026-10723等8件 | 子ゾーンのNSEC3レコードを誤って正当と受理し、NXDOMAIN応答偽装の恐れ |

**対処方法（共通）:** `sudo dnf check-release-update` で更新可否を確認の上、`sudo dnf update <パッケージ名>` 等で適用します。カーネル更新（kernel6.12 / kernel 等）は再起動が必要な点に注意してください。本タスクでは `sudo` 権限を要する操作を行わないため実行していません。

---

### kernel-livepatch（カーネルライブパッチ）関連（39件・集約）

**ライブパッチ（livepatch）** とは、Linux カーネルを再起動せずに脆弱性修正パッチを適用できる仕組みです。対象は以下39件のALAS ID（`ALAS2023LIVEPATCH-2026-287`〜`316`等）で、いずれも**同一の2件のCVE**に対応するため集約して記載します。

**関連CVE:**
- CVE-2026-64531: Linuxカーネル net/openvswitch — サイズ超過のネストされたアクション属性を拒否する修正（未修正時は異常な入力によるメモリ破壊等のリスク）
- CVE-2026-64600: Linuxカーネル xfs — ILOCK（inode lock）取得サイクル後にデータフォークマッピングを再取得しない不整合の修正

**対象パッケージ（カーネルバージョン別livepatch、代表例）:** kernel-livepatch-6.18.38-73.137, 6.18.36-69.136/134/138, 6.18.35-68.127/129, 6.12.94-123.190/180/174/176, 6.12.92-122.168/166, 6.1.176-221.367/360, 6.1.176-220.360/358, 6.18.25-55.108/57.109, 6.12.90-120.164, 6.18.33-63.124, 6.18.30-61.119/116, 6.12.83-113.160/115.161, 6.1.170-210.320/213.321, 6.1.175-219.359, 6.1.172-216.339, 6.12.88-119.157/160 ほか（詳細は出典RSSを参照）。

**出典（代表リンク）:** https://alas.aws.amazon.com/AL2023/ALAS2023LIVEPATCH-2026-287.html （他38件も同一パターン、末尾番号違いで `alas.aws.amazon.com/AL2023/ALAS2023LIVEPATCH-2026-XXX.html` からアクセス可能）

**対処方法:** ライブパッチは通常 `sudo dnf update kernel-livepatch` または AWS の Livepatch サービス経由で自動適用されます。カーネル再起動なしで修正が反映されます。本タスクでは `sudo` を要する操作は実施していません。

> **注記（reportableTruncated）:** 自動収集スクリプト（`fetch-alas.mjs`）は詳細取得の礼儀（サーバー負荷配慮）から先頭30件までしか自動取得しません。本記事の重要（Important）・緊急（Critical）分は、Optimus が RSS 差分とAWS公式ページを個別に確認して全84件を網羅していますが、livepatch分は情報量削減のため上記の通り集約しています。

---

## 🟡 Medium（中）新規5件（件数のみ・参考情報）

| ALAS ID | パッケージ |
|---|---|
| [ALAS2023-2026-1992](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-1992.html) | libxml2 |
| [ALAS2023-2026-2025](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2025.html) | amazon-cloudwatch-agent |
| [ALAS2023-2026-2027](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2027.html) | jbig2dec |
| [ALAS2023-2026-2031](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2031.html) | openssh |
| [ALAS2023-2026-2038](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2038.html) | openvpn |

Low（低）新規は0件でした。

---

## 出典

- AWS公式 ALAS RSSフィード: https://alas.aws.amazon.com/AL2023/alas.rss
- 各アドバイザリの詳細ページ（上表リンク参照）

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
