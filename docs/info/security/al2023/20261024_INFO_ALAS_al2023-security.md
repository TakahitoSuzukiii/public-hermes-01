# AL2023 セキュリティアドバイザリ週次レポート（2026-10-24）

作成日: 2026-10-24 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 3 |
| Important | 5 |
| Medium | 0 |
| Low | 0 |

対象期間: 2026-10-17 〜 2026-10-24（全8件を詳細取得済み、切り詰めなし）

---

## 注目アドバイザリ（重大度順）

### 1〜3. dotnet 系 Critical 3件（dotnet8.0 / dotnet9.0 / dotnet10.0）

- [ALAS2023-2026-3248](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3248.html)（dotnet9.0）、[ALAS2023-2026-3249](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3249.html)（dotnet10.0）、[ALAS2023-2026-3250](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3250.html)（dotnet8.0）— いずれも **Critical（緊急）**
- **対象パッケージ:** .NET ランタイム/SDK（Microsoft の開発基盤）。3本とも同一CVE。
- **関連 CVE:** CVE-2026-70188, CVE-2026-88092
- **概要:** ASP.NET Core（.NET の Web アプリ基盤）に、HTTPリクエストの解釈の食い違い（HTTP request/response smuggling＝リクエスト密輸。プロキシとサーバで解釈がずれることを悪用する攻撃）があり、認証なしの攻撃者がネットワーク経由でセキュリティ機能の回避（CVE-2026-70188）や改ざん（CVE-2026-88092）を行える恐れがあります。
- **対処方法:** `sudo dnf check-release-update` で更新の有無を確認し、`sudo dnf update dotnet*` 等で更新します。本タスクは情報収集のみで、`sudo`（管理者権限）が必要なコマンドは実行していません。

### 4. ALAS2023-2026-3280（python-awscrt）— Important

- [ALAS2023-2026-3280](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3280.html)
- **対象パッケージ:** python-awscrt（AWS Common Runtime の Python バインディング）
- **関連 CVE:** CVE-2026-12043
- **概要:** aws-c-http ライブラリの HPACK（HTTP/2のヘッダ圧縮方式）動的テーブルサイズ更新の処理不備により、悪意あるサーバに接続したクライアント側でメモリ破壊が起き、任意コード実行に至る恐れがあります。aws-c-http 0.11.0 以降への更新が推奨されています。
- **対処方法:** `sudo dnf update python3-awscrt` 等（要管理者権限・本タスクでは未実行）。

### 5〜8. PHP 系 Important 4件（php8.2 / 8.3 / 8.4 / 8.5）

- [ALAS2023-2026-3301](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3301.html)（php8.2）、[3302](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3302.html)（php8.3）、[3303](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3303.html)（php8.4）、[3304](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3304.html)（php8.5）— いずれも Important（重要）
- **関連 CVE:** CVE-2026-109618, CVE-2026-109619（4本とも同一）
- **概要:** PHP はメモリ不足（OOM）時に `longjmp()` で処理を中断しますが、一部の文脈でリクエスト用メモリが未初期化のまま後始末が走り、その領域を読む/分岐することでリモートコード実行（RCE）に至り得ます（CVE-2026-109618）。また、リクエスト用メモリを指すグローバル状態が正しくリセットされず、解放後のメモリを参照し得る問題もあります（CVE-2026-109619）。
- **対処方法:** `sudo dnf check-release-update` 後、使用中の PHP パッケージを `sudo dnf update php8.x*` で更新（要管理者権限・本タスクでは未実行）。

---

## 🎯 CVSS・OWASPスコア

> 📌 **読み方の注意:** 上の「Critical / Important」は **Amazon Linux 独自の重大度ラベル** で、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム＝脆弱性の深刻度を0.0〜10.0で表す国際基準）とは **別物** です。ここでは各CVEに「CVSS（NVD取得値）」と「OWASP（推定）」を並べます。CVSSは **v3.1** で統一し、NVD（米国国立標準技術研究所の脆弱性DB）から2026-10-24に取得しました。出所が **Primary** なら NVD自身の採点、**Secondary** なら CNA（CVE採番機関＝発行元）の採点です。

### ① CVSS v3.1（NVD取得値）

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ（攻撃条件） |
|---|---|---|---|---|---|
| CVE-2026-70188 | ASP.NET Core のHTTPリクエスト密輸（セキュリティ機能回避） | **9.1** | CRITICAL | Secondary（CNA: Microsoft） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N` |
| CVE-2026-88092 | ASP.NET Core のHTTPリクエスト密輸（改ざん） | **9.4** | CRITICAL | Secondary（CNA: Microsoft） | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L` |
| CVE-2026-12043 | aws-c-http HPACK処理不備（メモリ破壊） | **8.8** | HIGH | Secondary（CNA: AWS） | `AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H` |
| CVE-2026-109618 | PHP OOM時の未初期化メモリ（RCE） | **9.8** | CRITICAL | **Primary（NVD）** | `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-109619 | PHP グローバル状態の解放後参照 | **8.1** | HIGH | **Primary（NVD）** | `AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H` |

- 併記: CVE-2026-12043 は CVSS **v4.0 = 8.7 HIGH**（CNA: AWS）、CVE-2026-109618/109619 は CVSS **v4.0 = 9.2 CRITICAL**（CNA: PHP）もあります。**v3.1 と v4.0 は採点方式が違い、数値は比較できません**（本表はv3.1で統一）。
- CVE-2026-70188 / 12043 は NVD の状態が「Awaiting Analysis（分析待ち）」のため、NVD自身の採点(Primary)はまだありません。
- CISA の SSVC（悪用判断の枠組み）では、いずれも悪用状況 `exploitation: none`（悪用確認なし）。dotnet 2件は `automatable: yes`（自動化攻撃が可能）です。
- `AV:N`＝ネットワーク経由で攻撃可、`AC:H`＝攻撃条件が複雑、`UI:R`＝利用者の操作が必要、`PR:N`＝認証不要。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology（OWASPのリスク評価手法）は **「起きやすさ（尤度）× 被害の大きさ（影響度）」** を0〜9で評価し、LOW(<3)・MEDIUM(3〜<6)・HIGH(6〜9) に分けて総合判定します。**公式値は存在せず、公開情報から見積もった「推定値」** です。業務への影響（ビジネスインパクト）は環境依存のため採点せず、技術面のみで評価しています。

| CVE | 尤度（起きやすさ） | 影響度（技術面） | 総合（推定） | 根拠のひとこと |
|---|---|---|---|---|
| CVE-2026-70188 | 6.38 HIGH | 4.75 MEDIUM | **High** | 認証不要でネットワークから到達可（機密性・整合性に影響、可用性は影響なし） |
| CVE-2026-88092 | 6.38 HIGH | 5.75 MEDIUM | **High** | 同上。改ざんに加え可用性にも軽微な影響 |
| CVE-2026-12043 | 4.38 MEDIUM | 6.5 HIGH | **High** | 悪意あるサーバへ接続する場面が前提で尤度は中。成功時は任意コード実行 |
| CVE-2026-109618 | 5.13 MEDIUM | 6.5 HIGH | **High** | 攻撃条件が複雑（AC:H）で尤度は中。成功すればRCE |
| CVE-2026-109619 | 5.13 MEDIUM | 6.5 HIGH | **High** | 同上（解放後参照によるメモリ破壊） |

- 採用要因（例: 70188）: skill 5 / motive 4 / opportunity 7 / size 9、discovery 7 / exploit 5 / awareness 6 / detection 8、機密性6 / 完全性5 / 可用性1 / 追跡可能性7。他CVEも同じ手順で見積もり、悪用確認なし（SSVC: none）の点は exploit 値を低めにして反映しています。

### ③ OWASP Top 10:2025 との対応

Top 10 は **Webアプリ向け** の分類です。NVDのCWE（弱点の種類の識別子）を、OWASP公式の各カテゴリページの Mapped CWEs と照合しました（2026-10-24 取得）。

| CVE | CWE | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-70188 / 88092 | CWE-444（HTTPリクエスト解釈の不整合） | **A06:2025 Insecure Design**（安全でない設計） |
| CVE-2026-12043 | CWE-415（二重解放） | **対象外**（低レベルのメモリ管理不備でWebアプリ向け分類に該当しないため） |
| CVE-2026-109618 / 109619 | CWE-416（解放後使用）、CWE-755、CWE-824、CWE-1325 | CWE-755（例外状態の不適切な処理）が **A10:2025 Mishandling of Exceptional Conditions** に対応。他のCWEは対象外 |

### 今週の優先度（所見）

1. **最優先: dotnet 系（CVSS 9.1 / 9.4、OWASP推定 High）** — 認証不要・自動化攻撃が可能（SSVC）。ASP.NET Core を公開運用している場合は優先して更新してください。
2. **次点: PHP（CVE-2026-109618、CVSS 9.8）** — NVD(Primary)がCriticalと評価。ただしAC:H（攻撃条件が複雑）で、悪用は確認されていません。PHP を使うWebサーバは更新推奨です。
3. **python-awscrt（CVSS 8.8）** — 影響は悪意あるサーバへ接続するクライアント側に限られます。
4. 本環境（WSL/Ubuntu）はAL2023の実運用対象ではないため、あくまで参考情報です。

> 📚 出典: NVD API（https://nvd.nist.gov/）、ALAS2023-2026-3248〜3250 / 3280 / 3301〜3304（https://alas.aws.amazon.com/AL2023/）、OWASP Risk Rating Methodology（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）

---

## その他

- Medium: 0件 / Low: 0件

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
