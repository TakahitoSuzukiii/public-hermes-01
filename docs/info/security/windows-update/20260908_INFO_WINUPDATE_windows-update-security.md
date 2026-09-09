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

| CVE番号 | 対象製品/コンポーネント | 重大度 | CVSS | 概要 |
|---|---|---|---|---|
| CVE-2026-81963 | Windows Update Stack（Windows Server 2025 等） | Important | 7.8 | Windows Update関連機能における特権昇格の脆弱性 |
| CVE-2026-85880 | Windows ALPC（Windows 10等の広範なWindows OS） | Important | 7.8 | ALPC機能における特権昇格の脆弱性 |

## ⚠️ 要注意（Exploitation More Likely / CVSS高スコア）

「Exploitation More Likely（悪用の可能性が高い）」と評価された脆弱性、および CVSS 9.8以上のクリティカル/重要な脆弱性（Windows/オンプレミス環境向け、更新適用が必要なもの）が多数あります。件数が多いため主要なものを抜粋します（全34件はMSRC公式サイトでご確認いただけます）。

**CVSS 9.8（Critical、更新適用要）主要な項目:**
- CVE-2026-66302: Skype for Business RCE（リモートコード実行）
- CVE-2026-69579: Windows Message Queuing RCE
- CVE-2026-69730: Windows DNS Server RCE（Exploitation More Likely）
- CVE-2026-78509 / CVE-2026-78510: Microsoft Office Outlook / Word RCE
- CVE-2026-69845 / CVE-2026-72979: Windows DHCP Server RCE（2件）

**Exploitation More Likely評価の主なもの:**
- CVE-2026-69730: Windows DNS Server RCE（CVSS 9.8）
- CVE-2026-69525: Remote Desktop Services RCE（CVSS 9.8）
- CVE-2026-69676: Windows Kerberos RCE（CVSS 8.8）
- CVE-2026-72940: Windows Schannel RCE（CVSS 8.8）

## ☁️ Azureクラウド関連の重大な脆弱性

以下3件はAzure（マイクロソフトのクラウドサービス）側のサービスに関する脆弱性で、**マイクロソフト側で対応済み、または利用者側の更新作業は不要**です（参考情報として記載）。

- CVE-2026-70352: Azure AI Language 特権昇格（CVSS 10）
- CVE-2026-83711: Azure Active Directory B2C 特権昇格（CVSS 10）
- CVE-2026-83941: Entra ID 特権昇格（CVSS 9.9）

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

**脆弱性の技術的種類**: 「improper link resolution before file access（link following）」＝リンク解決の不備（リンクフォロー攻撃）。ファイルへアクセスする前に、そのファイルパスが指すシンボリックリンクやジャンクション（Windowsにおけるファイルパスのショートカット機構）を正しく検証しないまま処理してしまう不具合です。攻撃者はこの隙を突いて、Windows Updateの処理が本来アクセスすべきでない、より高い権限を持つファイル（例: システムファイル）を代わりに操作させることができます。

**想定される攻撃の流れ**: この脆弱性はローカル権限昇格型（Elevation of Privilege＝すでに何らかのアクセス権を持つ攻撃者が、より高い権限を得る攻撃）です。攻撃者はまず一般ユーザー権限で端末にログイン（またはマルウェア等で足がかりを得た状態）している必要があり、その状態からWindows Update Stackの処理タイミングを悪用してリンクを差し替え、最終的にSYSTEM権限（Windowsの最上位権限）を奪取します。

**悪用状況**: MSRC・CISA双方で「更新プログラム公開前から悪用が確認された」ゼロデイ（対策が存在しない状態で悪用される脆弱性）として扱われています。具体的な攻撃グループ名やマルウェア名は、本稿執筆時点の公開情報では明らかにされていません。

**影響範囲**: 一般的なWindows PC・開発環境にも該当し得ます（Windows Update機能はほぼ全端末に存在するため）。ただし本脆弱性はローカル権限昇格型のため、リモートから直接侵入されるものではなく、既に何らかの形で端末にアクセスできる攻撃者が「より高い権限を得るための踏み台」として使うケースが想定されます。

### CVE-2026-85880: Windows Advanced Local Procedure Call (ALPC) Elevation of Privilege Vulnerability

**対象コンポーネント**: Windows ALPC（Advanced Local Procedure Call＝Windows内部のプロセス間通信の仕組み）。OSの中核機能であり、Windowsの各種サービスやプロセスが情報をやり取りする際に広く使われています。ほぼ全てのWindows端末（Windows 10/11、Windows Server各種）に存在します。

**脆弱性の技術的種類**: 「heap-based buffer overflow（ヒープベースのバッファオーバーフロー）」＝プログラムが動的に確保するメモリ領域（ヒープ）に対して、想定より大きなデータを書き込んでしまい、隣接するメモリ領域を意図せず上書きしてしまう不具合です。攻撃者はこれを悪用して、任意のコードを実行させたり、プロセスの動作を乗っ取ったりできる可能性があります。

**想定される攻撃の流れ**: こちらもローカル権限昇格型です。既に一般ユーザー権限で端末を操作できる攻撃者（または侵入済みのマルウェア）が、ALPC通信に細工したデータを送り込み、ヒープバッファオーバーフローを発生させることで、より高い権限（SYSTEM権限）を取得します。

**悪用状況**: CVE-2026-81963と同様、更新プログラム公開前から実際の悪用が確認されているゼロデイ脆弱性として、MSRC・CISA KEVの双方に掲載されています。具体的な攻撃グループ・マルウェア名の詳細は本稿執筆時点では非公開です。

**影響範囲**: ALPCはWindows OS全体の基盤機能であるため、一般的なWindows PC・開発環境にも該当します。CVE-2026-81963と同じく、リモートから直接突かれるものではなく、既に足がかりを得た攻撃者による権限昇格の手段として悪用されるリスクがあります。

## ✅ 対処方法

1. **Windows Update または WSUS（Windows Server Update Services＝社内向け更新配信サーバー）経由での更新適用を推奨します。** 個人PC・開発機であれば「設定 → Windows Update」から最新の更新プログラムを確認・適用してください。
2. 悪用済み脆弱性（CVE-2026-81963、CVE-2026-85880）が含まれる更新は、CVSSスコア自体は7.8とそこまで高くありませんが、実際の悪用が確認済みのため優先度は最高です。速やかな適用を推奨します。
3. Exchange Serverを自社運用している場合は、上記MSRCブログの補足情報で案内されている個別のExchangeチームブログ記事もあわせてご確認ください。
4. 本タスクでは実際の更新適用作業（sudo／管理者権限を要する操作）は行いません。適用は鈴木さんご自身、または管理者権限をお持ちの方が実施してください。

## 出典

- MSRC Security Update Guide: https://msrc.microsoft.com/update-guide/
- MSRC公式ブログ（2026年9月・日本語版）: https://www.microsoft.com/en-us/msrc/blog/2026/09/202609-security-update/
- CISA 既知悪用脆弱性カタログ: https://www.cisa.gov/known-exploited-vulnerabilities-catalog

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
