# AL2023 セキュリティアドバイザリ週次レポート（2026-10-03）

作成日: 2026-10-03 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 1 |
| Important | 84 |
| Medium | 4 |
| Low | 1 |

対象期間: 2026-09-26 〜 2026-10-03

> ⚠️ 今週も Important 案件が非常に多く（84件）、その大半は kernel-livepatch（カーネルの再起動なしパッチ適用機能）の個別ビルド向けアドバイザリです。詳細取得には上限（30件）があるため、reportable（Critical+Important）85件のうち先頭30件のみ詳細を取得しています（`reportableTruncated=true`）。

---

## 注目アドバイザリ（重大度順）

### 1. ALAS2023-2026-3149（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3149.html)） — Critical

- **重大度:** Critical（緊急）
- **対象パッケージ:** amazon-ssm-agent（AWS Systems Manager Agent。EC2インスタンス等をリモート管理するためのエージェント）
- **関連 CVE（共通脆弱性識別子）:** CVE-2026-42505, CVE-2026-71556, CVE-2026-71557, CVE-2026-89049
- **概要:** ECH（Encrypted Client Hello、TLSハンドシェイクの暗号化拡張）を使った通信が、暗号化されないクライアントハロー内に事前共有鍵（PSK）の識別子が漏れていたことで、通信を傍受する第三者（パッシブな観測者）に匿名性を破られる恐れがありました（CVE-2026-42505）。また、go-git（Go言語で書かれたgit実装ライブラリ、バージョン5.19.2/6.0.0-alpha.5未満が対象）には、ワークツリー操作（checkout・status・add等）がシンボリックリンクの解決をワークツリーの範囲内に限定していない問題があり、悪意あるリポジトリをクローンして操作すると、意図したディレクトリ外のファイルを読み書きされる恐れがありました。
- **対処方法:** `sudo dnf check-release-update` および `sudo dnf update amazon-ssm-agent` 等による更新が必要です。本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドの実行は行っておりません。実際の適用は管理者権限を持つ方が実施してください。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3149.html

### 2. kernel-livepatch 関連アドバイザリ群（Important、30件）

今週の Important のうち詳細取得済み分はすべて、kernel-livepatch（Linux カーネルを再起動せずにパッチ適用する仕組み）の各カーネルビルド版に対する個別アドバイザリです（ID 例: `ALAS2023LIVEPATCH-2026-389` 〜 `418`）。対象パッケージ名（`kernel-livepatch-<バージョン>`）はカーネルビルドごとに異なりますが、修正内容は今週取得分すべてが同一のCVEでした。

- **CVE-2026-80521:** Linux カーネルの af_unix（UNIXドメインソケット関連サブシステム）で、`unix_del_edge()` 処理時に SCC（強連結成分、ソケット間の循環参照検出に使うデータ構造）エントリのリンク解除漏れがあり、不整合な状態を引き起こす恐れがある不具合。
- **対処方法:** livepatch は通常、`sudo yum update` や livepatch 管理コマンドの実行環境で自動適用される運用が一般的ですが、本タスクは情報収集のみを目的としており `sudo` を要するコマンドの実行は行っておりません。実際の適用状況・要否は管理者権限を持つ方が確認してください。
- **出典（代表）:** https://alas.aws.amazon.com/AL2023/ALAS2023LIVEPATCH-2026-389.html （他、`390`〜`418` 番台に同種のアドバイザリが多数存在）

> 上記2件で詳細取得済み30件のうち29件（kernel-livepatch）＋1件（Critical本体）をカバーしています。残る55件（reportable 85件 − 詳細取得30件）は今回のツール制約上、個別の詳細を取得できていません。次回以降の取得上限調整、または AWS 公式の該当週まとめページでの確認を推奨します。

---

## 🎯 CVSS・OWASPスコア（2026-10-04 追記）

> 📌 **読み方の注意:** 上の「Critical / Important」は **Amazon Linux 独自の重大度ラベル** で、CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム＝脆弱性の深刻度を0.0〜10.0で表す国際基準）とは **別物** です。ここでは各CVEに「CVSS（NVD公式値）」と「OWASP（推定）」を並べます。CVSSは **v3.1** で統一し、NVD（米国国立標準技術研究所の脆弱性DB）から取得しました。「出所」が *CNA* のものは、**脆弱性の発行元（CNA＝CVE採番機関）が付けた値** で、NVD自身の採点ではありません。

### ① CVSS v3.1（公式値）

| CVE | 概要 | CVSS v3.1 | 深刻度 | 出所 | ベクタ（攻撃条件） |
|---|---|---|---|---|---|
| CVE-2026-89049 | SSM Agent のSSRF（サーバ側リクエスト偽造）で、IAMロールの一時認証情報を窃取され得る | **9.9** | CRITICAL | CNA（Amazon） | `AV:N/AC:L/PR:L/UI:N/S:C/C:H/I:H/A:H` |
| CVE-2026-80521 | Linuxカーネル af_unix のSCCリンク解除漏れ | **7.8** | HIGH | CNA（Red Hat） | `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| CVE-2026-71556 | go-git のシンボリックリンク境界チェック不備 | **7.1** | HIGH | CNA（GitHub） | `AV:N/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:L` |
| CVE-2026-71557 | go-git の参照名未サニタイズ（ディレクトリトラバーサル） | **6.3** | MEDIUM | CNA（GitHub） | `AV:N/AC:L/PR:L/UI:R/S:U/C:N/I:H/A:L` |
| CVE-2026-42505 | ECHの事前共有鍵識別子の漏えい | **5.3** | MEDIUM | CNA | `AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N` |

- CVE-2026-89049 には **CVSS v4.0 の 8.5（HIGH）** も併記されています。**v3.1 と v4.0 は採点方式が違い、数値は比べられません**（本表はv3.1で統一）。
- `AV:N`＝ネットワーク経由で攻撃可、`AV:L`＝端末上での操作が必要、`PR:L`＝一般ユーザ権限が必要、`S:C`＝影響が他の領域へ波及（Scope Changed）。
- 実際の攻撃に使われているか（悪用の確認）は、今回の取得範囲では確認できていません。

### ② OWASP Risk Rating（推定）

OWASP Risk Rating Methodology（OWASPのリスク評価手法）は **「起きやすさ（尤度）× 被害の大きさ（影響度）」** を0〜9で評価し、LOW(<3)・MEDIUM(3〜<6)・HIGH(6〜9) に分けて総合判定します。**これは公式値が存在せず、公開情報から私が見積もった「推定値」** です。業務への影響（ビジネスインパクト）は環境によって変わるため採点せず、技術面のみで評価しています。

| CVE | 尤度（起きやすさ） | 影響度（技術面） | 総合（推定） | 根拠のひとこと |
|---|---|---|---|---|
| CVE-2026-89049 | 6.75 HIGH | 7.0 HIGH | **Critical** | 認証済みユーザが遠隔から悪用でき、IAM権限の乗っ取りに直結 |
| CVE-2026-80521 | 5.12 MEDIUM | 7.0 HIGH | **High** | 端末上のローカル権限が前提のため尤度は中程度。成功時の被害は大 |
| CVE-2026-71556 | 6.12 HIGH | 3.75 MEDIUM | **High** | 悪意あるリポジトリを開かせるだけで成立。整合性への被害が中心 |
| CVE-2026-71557 | 5.75 MEDIUM | 3.25 MEDIUM | **Medium** | 参照名の細工にはリポジトリ操作権限が必要 |
| CVE-2026-42505 | 5.0 MEDIUM | 2.75 LOW | **Low** | 通信の匿名性低下にとどまり、データ破壊は伴わない |

### ③ OWASP Top 10:2025 との対応

OWASP Top 10 は **Webアプリ向け** の分類です。各CVEのCWE（弱点の種類の識別子）を、OWASP公式の対応表と照合しました。

| CVE | CWE（弱点の種類） | OWASP Top 10:2025 |
|---|---|---|
| CVE-2026-89049 | CWE-918（SSRF）、CWE-1289 | **A01:2025 Broken Access Control**（アクセス制御の不備）※CWE-918が対応表に掲載 |
| CVE-2026-71556 | CWE-59（シンボリックリンク追跡） | **A01:2025 Broken Access Control** |
| CVE-2026-71557 | CWE-22（パストラバーサル） | **A01:2025 Broken Access Control** |
| CVE-2026-42505 | CWE-201（送信データへの機微情報の混入） | **A01:2025 Broken Access Control**（対応表にCWE-201掲載） |
| CVE-2026-80521 | CWE未付与（NVD） | **対象外**（カーネルの不具合でありWebアプリ向け分類に該当しないため） |

> ⚠️ 照合で確認できたのは「そのCWEが当該カテゴリの対応表に載っているか」までです。CWE-1289は対応表で確認できていません。

### 今週の優先度（所見）

1. **最優先: CVE-2026-89049（CVSS 9.9 / OWASP推定 Critical）** — SSM Agent は多くのEC2に常駐するため影響範囲が広く、IAM認証情報の窃取は他システムへの侵入の足がかりになります。`amazon-ssm-agent` を **3.3.4851.0 以降**（今回の修正版は 3.3.5226.0）へ更新してください（要管理者権限）。
2. 次点: go-git系2件（7.1 / 6.3）と、kernel-livepatchの af_unix（7.8、ローカル権限が前提）。
3. CVE-2026-42505（5.3）は優先度低め。

> 📚 出典: NVD API（https://nvd.nist.gov/）、ALAS-2023-2026-3149（https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3149.html）、ALAS2023LIVEPATCH-2026-389、OWASP Risk Rating Methodology（https://owasp.org/www-community/OWASP_Risk_Rating_Methodology）、OWASP Top 10:2025（https://owasp.org/Top10/2025/）

---

## その他

- Medium: 4件（libssh, ImageMagick, libxml2, awscli-2）/ Low: 1件（amazon-efs-utils）※いずれも件数のみの記録で詳細は割愛
- 一覧の切り詰め（truncated）: あり。reportable（Critical+Important）85件のうち、詳細取得は先頭30件までです。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
