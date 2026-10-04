作成日: 2026-09-08T07:00:00Z / STATUS: INFO / TOPIC: WINUPDATE / 対象月: September 2026 Security Updates

# Windows Update月次セキュリティ更新 監視レポート（2026年9月）

Microsoft Security Response Center（MSRC＝マイクロソフト製品のセキュリティ脆弱性情報を一元管理する公式窓口）が公開した、2026年9月分（米国時間9月8日公開）のセキュリティ更新プログラム情報をまとめました。

## 📊 全体サマリー

- 総CVE（Common Vulnerabilities and Exposures＝共通脆弱性識別子。個々の脆弱性に割り振られる管理番号）件数: **1,186件**
- 重大度別件数
  - Critical（緊急）: **119件**
  - Important（重要）: **913件**
  - Moderate（警告）: **112件**
  - Low（注意）: **18件**
  - Unknown（未分類）: **24件**

今月は過去最大級のボリュームで、Microsoft史上でも件数の多いパッチ Tuesday（毎月第2火曜日＝米国時間の月例セキュリティ更新日）の一つとなっています。

## 🚨 悪用済み（Exploited）— 最優先で確認してください

以下2件は、**セキュリティ更新プログラムが公開される前から、実際に悪用（攻撃者による利用）が確認されている**脆弱性です。CISA（米国サイバーセキュリティ・インフラセキュリティ庁）の既知悪用脆弱性カタログ（KEV＝Known Exploited Vulnerabilities）にも追加されています。該当環境をお持ちの場合は最優先で更新を適用してください。

| CVE番号 | 対象製品/コンポーネント | MSRC重大度 | CVSS v3.1（出所） | OWASP Risk Rating（推定） | 概要 |
|---|---|---|---|---|---|
| CVE-2026-81963 | Windows Update Stack（Windows Server 2025 等） | Important | **7.8** HIGH（CNA=Microsoft） | **Critical**（尤度6.62 HIGH×影響7.0 HIGH） | Windows Update関連機能における特権昇格の脆弱性 |
| CVE-2026-85880 | Windows ALPC（Windows 10等の広範なWindows OS） | Important | **7.8** HIGH（CNA=Microsoft） | **Critical**（尤度6.62 HIGH×影響7.0 HIGH） | ALPC機能における特権昇格の脆弱性 |

> 💡 CVSS 7.8でも、OWASP推定が Critical になるのは **「実際に悪用されている（ゼロデイ）」ため尤度が高い** からです。CVSSは「悪用されやすさの実績」を原則含まない一方、OWASP Risk Ratingは含めて評価する、という手法の違いです。

## ⚠️ 要注意（CVSS 9.8以上 34件 ／ Exploitation More Likely 58件）

> 🔧 **2026-10-04 訂正:** 初版は見出しを「Exploitation More Likely / CVSS高スコア」と一括りにしていましたが、実際は **別々の2つの基準** です。
> - **CVSS 9.8以上（更新適用が必要なもの）= 34件** … 深刻度が高いもの。ただし34件のうち、MSRCが「悪用の可能性が高い（Exploitation More Likely）」と評価したのは **2件のみ**（CVE-2026-69730、CVE-2026-69525）。残りは Less Likely 18件・Unlikely 14件です。
> - **Exploitation More Likely（悪用の可能性が高い）= 58件** … Microsoftが「攻撃者に悪用されやすい」と評価したもの。CVSSが9.8未満のものも多数含みます。
> 「CVSSが高い」ことと「悪用されやすい」ことは別の軸です。両方を見て優先度を決めてください。

**① CVSS 9.8（34件）のうち主要な項目**

| CVE | 内容 | MSRC評価 | CVSS v3.1（出所） | OWASP RR（推定） | OWASP Top10:2025 |
|---|---|---|---|---|---|
| CVE-2026-69730 | Windows DNS Server RCE | **More Likely** | 9.8（CNA） | **Critical**（尤度7.12 HIGH×影響7.0 HIGH） | A01〜A10に該当なし（CWE-416＝解放済みメモリの誤使用）※対象外 |
| CVE-2026-69579 | Windows Message Queuing RCE | Unlikely | 9.8（CNA） | **High**（5.12 MEDIUM×7.0） | 対象外（CWE-416） |
| CVE-2026-66302 | Skype for Business RCE | Less Likely | 9.8（CNA） | **High**（5.12 MEDIUM×7.0） | A06 Insecure Design（CWE-73） |
| CVE-2026-78509 | Microsoft Office（Mac版）RCE | Less Likely | 9.8（CNA） | **High**（5.5 MEDIUM×7.0） | 対象外（CWE-122＝ヒープバッファオーバーフロー） |
| CVE-2026-78510 | Microsoft Office RCE | Less Likely | **8.4（NVD Primary）** ／ Microsoft(CNA)は9.8 | **High**（5.5 MEDIUM×7.0） | 対象外（CWE-122） |
| CVE-2026-69845 | Windows DHCP Server RCE | Less Likely | 9.8（CNA） | **High**（5.12 MEDIUM×7.0） | A05 Injection（CWE-20＝入力検証の不備）／CWE-122は対象外 |
| CVE-2026-72979 | Windows DHCP Server RCE | Less Likely | 9.8（CNA） | **High**（5.12 MEDIUM×7.0） | 対象外（CWE-416） |

> ⚠️ **CVE-2026-78510 は評価が割れています。** NVD自身の採点（Primary）は **8.4**、Microsoft（CNA）の採点は **9.8** です。本表の「9.8」は初版記載値（MSRC由来）です。どちらを採るかは運用方針次第ですが、**出所を併記するのが安全** です。

**② Exploitation More Likely（58件）のうち主要な項目**

| CVE | 内容 | CVSS v3.1（出所） | OWASP RR（推定） | OWASP Top10:2025 |
|---|---|---|---|---|
| CVE-2026-69730 | Windows DNS Server RCE | 9.8（CNA） | **Critical** | 対象外（CWE-416） |
| CVE-2026-69525 | Remote Desktop Services RCE | 9.8（CNA） | **Critical** | 対象外（CWE-416） |
| CVE-2026-69676 | Windows Kerberos RCE | 8.8（CNA） | **High**（5.88 MEDIUM×7.0） | A07 Authentication Failures（CWE-294＝認証のキャプチャ・リプレイ） |
| CVE-2026-72940 | Windows Schannel RCE | 8.8（CNA） | **Critical**（6.62 HIGH×7.0） | 対象外（CWE-122） |

## ☁️ Azureクラウド関連の重大な脆弱性

以下3件はAzure（マイクロソフトのクラウドサービス）側のサービスに関する脆弱性で、**マイクロソフト側で対応済み、または利用者側の更新作業は不要**です（参考情報として記載）。

| CVE | 内容 | CVSS v3.1（出所） | OWASP RR（推定） | OWASP Top10:2025 |
|---|---|---|---|---|
| CVE-2026-70352 | Azure AI Language 特権昇格 | **10.0**（CNA）※NVD解析中 | **High**（3.62 MEDIUM×7.0） | A07 Authentication Failures（CWE-306＝重要機能の認証欠如） |
| CVE-2026-83711 | Azure AD B2C 特権昇格 | **10.0**（CNA）※NVD解析中 | **High**（3.62 MEDIUM×7.0） | A01 Broken Access Control（CWE-639＝ユーザ制御キーによる認可回避） |
| CVE-2026-83941 | Entra ID 特権昇格 | **9.9**（CNA）／**8.8（NVD Primary）** | **High**（3.62 MEDIUM×7.0） | A01 Broken Access Control（CWE-862＝認可の欠如） |

> 📝 **OWASP推定の見方:** これら3件は「提供元（Microsoft）側で対応済み／利用者作業不要」のため、**尤度（起きやすさ）を意図的に低く（3.62）見積もっています**（深刻度のCVSS 10と「今あなたが危ない度」は別物）。この尤度の低さは私の判断による推定です。

## 📰 MSRC公式ブログの補足情報

MSRC公式ブログ日本語版（2026年9月分）の本文を確認しました。主な注意点は以下の通りです。

- **悪用確認済み脆弱性への緊急対応の呼びかけ**: ブログ本文でも CVE-2026-85880（Windows ALPC 特権昇格）と CVE-2026-81963（Windows Update スタック 特権昇格）の2件について、「更新プログラムが公開されるよりも前に悪用が行われていることを確認している」旨が明記され、早急な適用を呼びかけています。
- **Microsoft Exchange Server 追加リリース案内**: Exchange Serverの更新プログラムを展開する際は、Microsoft Exchangeチームブログの記事「Released: September 2026 Exchange Server Security Updates」も併せて参照するよう案内されています。Exchange Serverを自社運用（オンプレミス）している場合は必読です。
- **今月の更新はベースライン更新プログラム（再起動が必要）**: 今月のWindows更新プログラムは通常型（フルスキャン・再起動を伴う）の更新であり、簡易適用が可能な「ホットパッチ」（再起動不要の軽量更新）のスケジュールとは別枠である旨が案内されています。
- **既知の問題（Known Issues）**: 各更新プログラムの既知の問題は、月次のセキュリティ更新プログラム リリースノートに個別掲載される形式のため、ブログ本文には具体的な内容の記載はありませんでした。該当のKB（Knowledge Base＝技術情報番号）を適用予定の場合は、リリースノート側での事前確認を推奨します。
- **既存の脆弱性情報を38件更新**: 過去に公開済みの脆弱性情報のうち38件について、対象ソフトウェア一覧の修正や謝辞の追記など、情報提供目的の更新が行われています（新規の脅威度変更ではありません）。

## 🔍 悪用済み脆弱性の詳しい解説

### CVE-2026-81963: Windows Update Stack Elevation of Privilege Vulnerability

**対象コンポーネント**: Windows Update Stack（Windows Updateの適用処理を担う内部の仕組み一式）。Windows Update機能自体は、Windows Server／Windows 10／11を問わず、ほぼ全てのWindows環境に標準搭載されています。

**スコア**: CVSS v3.1 **7.8 HIGH**（出所: CNA=Microsoft、ベクタ `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H`＝端末上で・低権限で・ユーザ操作なしに成立）／ OWASP Risk Rating（推定）**Critical**（尤度6.62 HIGH × 影響7.0 HIGH）／ OWASP Top10:2025 **A01 Broken Access Control**（CWE-284＝不適切なアクセス制御、CWE-59＝リンク解決の不備。いずれもA01の対応表に掲載）

**脆弱性の技術的種類**: 「improper link resolution before file access（link following）」＝リンク解決の不備（リンクフォロー攻撃）。ファイルへアクセスする前に、そのファイルパスが指すシンボリックリンクやジャンクション（Windowsにおけるファイルパスのショートカット機構）を正しく検証しないまま処理してしまう不具合です。攻撃者はこの隙を突いて、Windows Updateの処理が本来アクセスすべきでない、より高い権限を持つファイル（例: システムファイル）を代わりに操作させることができます。

**想定される攻撃の流れ**: この脆弱性はローカル権限昇格型（Elevation of Privilege＝すでに何らかのアクセス権を持つ攻撃者が、より高い権限を得る攻撃）です。攻撃者はまず一般ユーザー権限で端末にログイン（またはマルウェア等で足がかりを得た状態）している必要があり、その状態からWindows Update Stackの処理タイミングを悪用してリンクを差し替え、最終的にSYSTEM権限（Windowsの最上位権限）を奪取します。

**悪用状況**: MSRC・CISA双方で「更新プログラム公開前から悪用が確認された」ゼロデイ（対策が存在しない状態で悪用される脆弱性）として扱われています。具体的な攻撃グループ名やマルウェア名は、本稿執筆時点の公開情報では明らかにされていません。

**影響範囲**: 一般的なWindows PC・開発環境にも該当し得ます（Windows Update機能はほぼ全端末に存在するため）。ただし本脆弱性はローカル権限昇格型のため、リモートから直接侵入されるものではなく、既に何らかの形で端末にアクセスできる攻撃者が「より高い権限を得るための踏み台」として使うケースが想定されます。

### CVE-2026-85880: Windows Advanced Local Procedure Call (ALPC) Elevation of Privilege Vulnerability

**対象コンポーネント**: Windows ALPC（Advanced Local Procedure Call＝Windows内部のプロセス間通信の仕組み）。OSの中核機能であり、Windowsの各種サービスやプロセスが情報をやり取りする際に広く使われています。ほぼ全てのWindows端末（Windows 10/11、Windows Server各種）に存在します。

**スコア**: CVSS v3.1 **7.8 HIGH**（出所: CNA=Microsoft、ベクタ `AV:L/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H`）／ OWASP Risk Rating（推定）**Critical**（尤度6.62 HIGH × 影響7.0 HIGH）／ OWASP Top10:2025 **対象外**（CWE-122＝ヒープバッファオーバーフロー、CWE-908＝未初期化リソースの使用。いずれもTop10の対応表に無く、OSの基盤機能の不具合でWebアプリ向け分類に当てはまらないため）

**脆弱性の技術的種類**: 「heap-based buffer overflow（ヒープベースのバッファオーバーフロー）」＝プログラムが動的に確保するメモリ領域（ヒープ）に対して、想定より大きなデータを書き込んでしまい、隣接するメモリ領域を意図せず上書きしてしまう不具合です。攻撃者はこれを悪用して、任意のコードを実行させたり、プロセスの動作を乗っ取ったりできる可能性があります。

**想定される攻撃の流れ**: こちらもローカル権限昇格型です。既に一般ユーザー権限で端末を操作できる攻撃者（または侵入済みのマルウェア）が、ALPC通信に細工したデータを送り込み、ヒープバッファオーバーフローを発生させることで、より高い権限（SYSTEM権限）を取得します。

**悪用状況**: CVE-2026-81963と同様、更新プログラム公開前から実際の悪用が確認されているゼロデイ脆弱性として、MSRC・CISA KEVの双方に掲載されています。具体的な攻撃グループ・マルウェア名の詳細は本稿執筆時点では非公開です。

**影響範囲**: ALPCはWindows OS全体の基盤機能であるため、一般的なWindows PC・開発環境にも該当します。CVE-2026-81963と同じく、リモートから直接突かれるものではなく、既に足がかりを得た攻撃者による権限昇格の手段として悪用されるリスクがあります。

## ✅ 対処方法

1. **Windows Update または WSUS（Windows Server Update Services＝社内向け更新配信サーバー）経由での更新適用を推奨します。** 個人PC・開発機であれば「設定 → Windows Update」から最新の更新プログラムを確認・適用してください。
2. 悪用済み脆弱性（CVE-2026-81963、CVE-2026-85880）が含まれる更新は、CVSSスコア自体は7.8とそこまで高くありませんが、実際の悪用が確認済みのため **OWASP推定は Critical** で、優先度は最高です。速やかな適用を推奨します。
3. Exchange Serverを自社運用している場合は、上記MSRCブログの補足情報で案内されている個別のExchangeチームブログ記事もあわせてご確認ください。
4. 本タスクでは実際の更新適用作業（sudo／管理者権限を要する操作）は行いません。適用は鈴木さんご自身、または管理者権限をお持ちの方が実施してください。

## 🎯 CVSS・OWASPスコアの読み方と算出根拠（2026-10-04 追記）

- **CVSS（Common Vulnerability Scoring System＝共通脆弱性評価システム）** は深刻度を0.0〜10.0で示す国際基準です。本記事はすべて **v3.1** で統一し、NVD（米国国立標準技術研究所の脆弱性DB）で照合しました。「出所」が **CNA** のものは **発行元（CNA＝CVE採番機関。ここではMicrosoft）の採点**、**NVD Primary** はNVD自身の採点です。NVDで照合した15件では、MSRC配信データのCVSS値とNVDのCNA値は **13件で一致** しました。残る2件は採点者が割れています（CVE-2026-78510＝NVD Primary 8.4／CNA 9.8、CVE-2026-83941＝NVD Primary 8.8／CNA 9.9）ので、該当箇所に併記しています。NVD掲載の全CVEの値が一致するとは確認していません。
- **MSRCの重大度（Critical/Important等）はCVSSではなく** Microsoft独自のラベルです。別物として扱ってください。
- **OWASP Risk Rating（推定）** は「起きやすさ（尤度）× 被害の大きさ（影響）」を0〜9で評価する手法で、**公式値が存在しないため私の推定値** です（LOW<3 / MEDIUM 3〜<6 / HIGH 6〜9、マトリクスで総合判定）。尤度は攻撃の前提条件・MSRCの悪用可能性評価・悪用の確認有無から、影響は機密性・完全性・可用性・追跡可能性から見積もっています。**ビジネス影響は環境依存のため採点していません。**
- **OWASP Top 10:2025 は Webアプリ向け** の分類です。CWE（弱点の種類の識別子）をOWASP公式の対応表と照合し、**載っていないものは「対象外」** と明記しています（無理に当てはめていません）。
- MSRC配信データの対象39件（悪用済み2件・要注意34件・Azure3件）は、CVSS v3.1の計算式で **ベクタから再計算した値と配信値が全件一致** しました（配信データ内の整合性の確認であり、NVD側との一致確認とは別です）。
- **本記事で採点した対象:** 悪用済み2件、CVSS 9.8の主要7件、More Likelyの主要4件、Azure3件。要注意34件・More Likely58件の全件ではありません（件数が多いため。必要なら全件分を別表で作成できます）。

### 🔧 訂正履歴

| 日付 | 内容 |
|---|---|
| 2026-10-04 | ①CVSS・OWASPスコアを追記 ②要注意節の見出しを是正（「CVSS 9.8以上34件」と「More Likely 58件」は別基準。34件中More Likelyは2件のみ）③CVE-2026-78510 のCVSSがNVD Primary 8.4／CNA 9.8で割れている旨を注記 ④Kerberos・Schannelは「34件」ではなく「More Likely 58件」側の項目として整理し直し |

## 出典

- MSRC Security Update Guide: https://msrc.microsoft.com/update-guide/
- NVD API: https://nvd.nist.gov/
- OWASP Risk Rating Methodology: https://owasp.org/www-community/OWASP_Risk_Rating_Methodology
- OWASP Top 10:2025: https://owasp.org/Top10/2025/
- MSRC公式ブログ（2026年9月・日本語版）: https://www.microsoft.com/en-us/msrc/blog/2026/09/202609-security-update/
- CISA 既知悪用脆弱性カタログ: https://www.cisa.gov/known-exploited-vulnerabilities-catalog

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
