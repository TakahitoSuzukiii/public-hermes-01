# AL2023 セキュリティアドバイザリ週次レポート（2026-11-14）

作成日: 2026-11-14 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果です。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 1 |
| Important | 74 |
| Medium | 31 |
| Low | 0 |

対象期間: 2026-11-07 〜 2026-11-14（新規合計 106 件）

> ⚠️ Critical+Important は計 75 件ですが、詳細取得には上限（30件）があり、先頭30件のみ詳細を確認しています（`reportableTruncated=true`）。残り45件の個別詳細は未取得です。

---

## 注目アドバイザリ（重大度順）

### 1. ALAS2023-2026-3458（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3458.html)） — Critical
- **対象パッケージ:** httpd（Apache HTTP Server、Webサーバソフト）
- **関連 CVE:** CVE-2026-109163, CVE-2026-119618, CVE-2026-63292
- **概要:** mod_vhost_alias（ホスト名ごとにディレクトリを切り替える機能）で、スタック（一時メモリ領域）に1バイト余分に書き込んでしまう不具合（バッファオーバーライト）が修正されました。ほかに競合状態（タイミング次第で処理が食い違う不具合）に関するCVEも含まれます。

### 2. 主な Important アドバイザリ（抜粋）
- **kernel6.12（3448、CVE 70件）/ kernel（3455、6件）:** Linuxカーネルの多数の修正（例: mm/pagewalk の古い状態参照、bonding の型の取り違え）。
- **kernel-livepatch（`ALAS2023LIVEPATCH-2026-424〜426`）:** IPv4ネットワーク処理の競合状態（CVE-2026-98432、use-after-free＝解放済みメモリの再利用）を再起動なしで修正するパッチ。
- **firefox（3439、CVE 144件）:** 同一オリジンポリシー（他サイトのデータ読取を防ぐ仕組み）の回避など多数。
- **tomcat10（3420）:** JNDI領域での認証の重要手順欠落（CVE-2026-101296）。
- **rpm（3430）:** 信頼できないパッケージ内のシンボリックリンク解析でヒープバッファオーバーフロー（CVE-2026-95520）。
- **freerdp（3435）:** RDPサーバ側の入力解析で処理を飛ばしDoS（サービス妨害、CVE-2026-121951 ほか）。
- **git（3445）:** 巨大マージ結果のサイズ計算オーバーフロー（CVE-2026-105437 ほか）。
- **libheif（3437）、xfsprogs（3453）、squid（3454）、rsyslog（3449）、qemu（3442）、nodejs22/24（3456/3457）、skopeo/buildah（3450/3451）、perl-CGI（3436）、libsoup3（3421）、gstreamer（3424）、postgresql-odbc（3427）、X.Org/Xwayland（3443/3444）、python-pillow/pyasn1（3441/3438）、fltk（3459）** なども Important。

- **対処方法:** `sudo dnf check-release-update` で更新を確認し、`sudo dnf update <パッケージ名>` で適用します。**sudo（管理者権限）が必要なため本タスクでは実行していません。** 実施は管理者権限を持つ方にお願いします。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3458.html ほか各 ALAS ページ

---

## 🎯 CVSS・OWASPスコア

> 📌 上の「Critical / Important」は **Amazon Linux 独自の重大度ラベル** で、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム＝0.0〜10.0）とは **別物** です。CVSSはNVD（米国の脆弱性DB）の **v3.1** 値で統一。「出所」の *Secondary* は **発行元(CNA)の採点** で、NVD自身（Primary）の採点ではありません。今回取得できた値はすべて Secondary です。件数が多いため **代表的な CVE のみ** 掲載しています（全CVEの採点は網羅していません）。

### ① CVSS v3.1

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ |
|---|---|---|---|---|---|
| CVE-2026-98432 | カーネルIPv4の競合状態（UAF）／livepatch | **9.8** | CRITICAL | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-119618 | httpd 競合状態 | **8.1** | HIGH | Secondary（CNA） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-101296 | Tomcat JNDI認証の手順欠落 | **8.1** | HIGH | Secondary（CNA） | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-108472 | xfs_admin のコマンドインジェクション | **7.8** | HIGH | Secondary（Red Hat） | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-63292 | httpd スタックバッファ（mod_vhost_alias） | **7.5** | HIGH | Secondary（CNA） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-121951 | FreeRDP 入力解析でDoS | **7.5** | HIGH | Secondary（VulnCheck） | `AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H` |
| CVE-2026-105437 | git マージのサイズ計算オーバーフロー | **7.5** | HIGH | Secondary（GitLab） | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-120208 | libheif ヒープオーバーフロー | **7.5** | HIGH | Secondary（VulnCheck） | `AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-95520 | rpm シンボリックリンク解析のヒープオーバーフロー | **7.1** | HIGH | Secondary（Red Hat） | `AV:L/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:H` |
| CVE-2026-109163 | httpd 1バイト上書き（63292の修正漏れ） | **未採点** | — | NVDに値なし | 下記「推定」参照 |
| CVE-2026-106071 | Node.js Permission Model の過剰許可 | **未採点** | — | NVDに値なし | — |
| CVE-2026-104786 / 93404 / 101291 | squid / rsyslog / qemu | **未取得** | — | NVDに未掲載（404相当） | — |

- **推定（公式値ではない）:** CVE-2026-109163 は CVE-2026-63292 と同種の欠陥のため、同ベクタで算出すると **7.5 HIGH（推定 CVSS 3.1）**。
- CVE-2026-121951 / 120208 / 101296 には CVSS v4.0 値（8.7 / 7.7 / 9.1）もありますが、**v3.1 と v4.0 は数値の比較不可**です。
- 悪用の確認（実際に攻撃に使われているか）は今回の取得範囲では確認していません。

### ② OWASP Risk Rating（推定）

「起きやすさ（尤度）×被害の大きさ（影響度）」を0〜9で評価（LOW<3 / MEDIUM 3〜<6 / HIGH 6〜9）。**公式値ではなく技術面のみの推定**です（業務影響は未採点）。

| CVE | 尤度 | 影響度 | 総合（推定） | 根拠 |
|---|---|---|---|---|
| CVE-2026-98432 | 5.25 MEDIUM | 7.0 HIGH | **High** | 遠隔から成立し得るが競合状態で難易度は高め。成功時の被害は大 |
| CVE-2026-119618 | 5.62 MEDIUM | 7.0 HIGH | **High** | Web公開サーバ。タイミング依存で再現性は低め |
| CVE-2026-101296 | 5.62 MEDIUM | 6.5 HIGH | **High** | 認証回避で機密性・完全性に影響 |
| CVE-2026-63292 / 109163 | 5.88 MEDIUM | 6.25 HIGH | **High** | ネットワーク到達可能。特定機能(mod_vhost_alias)利用時 |
| CVE-2026-105437 | 5.5 MEDIUM | 7.0 HIGH | **High** | 悪意あるデータ処理が前提 |
| CVE-2026-108472 | 5.25 MEDIUM | 7.0 HIGH | **High** | ローカルで細工入力が必要 |
| CVE-2026-121951 | 6.12 HIGH | 4.0 MEDIUM | **High** | 認証不要の遠隔DoS。機密性・完全性への影響なし |
| CVE-2026-95520 | 5.5 MEDIUM | 5.0 MEDIUM | **Medium** | 悪意あるrpmを扱う場合のみ |

要因値の例（尤度: skill5/motive4/opportunity4〜7/size9/discovery7/exploit1〜5/awareness4/detection8、影響: 機密性1〜7/完全性1〜7/可用性5〜7/追跡可能性7）。

### ③ OWASP Top 10:2025 との対応

Top 10 は **Webアプリ向け** の分類です。CWE（弱点の種類の識別子）をNVDから取得しました。**今回は公式ページの Mapped CWEs との照合は実施していません**（未照合）。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-106071 | CWE-284（不適切なアクセス制御） | A01 Broken Access Control（有力。未照合） |
| CVE-2026-108472 | CWE-78（OSコマンドインジェクション） | A05 Injection（有力。未照合） |
| CVE-2026-101296 | CWE-304（認証の重要手順欠落） | A07 Authentication Failures（有力。未照合） |
| CVE-2026-98432 | CWE-416 | 対象外（カーネル。Webアプリ向け分類のため） |
| CVE-2026-95520 / 120208 / 105437 / 63292 / 109163 | CWE-787 / 122 / 121（バッファオーバーフロー系） | 対象外（メモリ安全性の不具合） |
| CVE-2026-119618 / 121951 | CWE-362 / CWE-617 | 未照合（無理に当てはめない） |

### 今週の優先度（所見）
1. **最優先: カーネル（CVE-2026-98432、CVSS 9.8 Secondary / OWASP推定 High）** — 認証不要のネットワーク経由。livepatch 適用またはカーネル更新を。
2. **httpd（Critical ラベル）:** CVSS 7.5〜8.1。Apache公開サーバなら優先。
3. **tomcat10（8.1）**、git / libheif / rpm / xfsprogs（7.1〜7.8）は利用状況に応じて。
4. firefox（144件）、kernel6.12（70件）は件数が多いため、一括更新で対応するのが現実的。

> 📚 出典: NVD API（https://nvd.nist.gov/）、ALAS（https://alas.aws.amazon.com/）、OWASP Risk Rating Methodology（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）。NVD API は一時的に 503 が返りましたが再試行で取得済みです。

---

## その他
- Medium: 31件 / Low: 0件（件数のみ。詳細は割愛）
- 一覧の切り詰め: あり（Critical+Important 75件中、詳細取得は30件）

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の活動として公開しています。
