作成日: 2026-07-14T07:00:00Z / STATUS: INFO / TOPIC: WINUPDATE / 対象月: July 2026 Security Updates

# Windows Update月次セキュリティ更新まとめ（2026年7月 / Patch Tuesday）

Microsoft公式のMSRC（Microsoft Security Response Center、マイクロソフト セキュリティ対応センター）が公開しているCVRF（Common Vulnerability Reporting Framework、共通脆弱性報告フォーマット）データをもとに、2026年7月分（July 2026 Security Updates）のセキュリティ更新情報をまとめました。

## 📊 概要（重大度別の件数）

今回公開された脆弱性（CVE: Common Vulnerabilities and Exposures、共通脆弱性識別子）の総数は **2,140件** でした。重大度（Severity）別の内訳は以下の通りです。

| 重大度 | 件数 |
|---|---|
| 🔴 緊急（Critical） | 119件 |
| 🟠 重要（Important） | 829件 |
| 🟡 警告（Moderate） | 295件 |
| 🟢 注意（Low） | 30件 |
| ⚪ 不明（Unknown） | 867件 |

※「不明」はMicrosoftが個別の重大度を割り当てていない項目（クラウドサービス起因の脆弱性など）を含みます。

## 🚨 最優先：悪用が確認されている脆弱性（Exploited / ゼロデイ）

以下の3件は、Microsoftが「悪用が検出された（Exploitation Detected）」と公表している、いわゆる**ゼロデイ脆弱性**（修正パッチ公開前後に既に攻撃で使われている脆弱性）です。至急の対応が推奨されます。

1. **CVE-2026-58644**（緊急・CVSS 9.8）— Microsoft SharePoint リモートコード実行の脆弱性
   - 対象製品: Microsoft SharePoint Enterprise Server 2016
   - 対象KB: 5002880, 5002874, 5002873
   - 概要: 攻撃者が細工したリクエストを送ることで、対象サーバー上で任意のコードを実行できる可能性があります。SharePoint環境は特に優先的な適用を推奨します。

2. **CVE-2026-56155**（重要・CVSS 7.8）— Active Directory Federation Services（AD FS）権限昇格の脆弱性
   - 対象製品: Windows 10 Version 1809 for 32-bit Systems ほか
   - 対象KB: 5099538, 5099540, 5099536, 5099535, 5099445, 5099444
   - 概要: ローカルで低い権限を持つ攻撃者が、システム上でより高い権限を得られる可能性があります。

3. **CVE-2026-56164**（警告・CVSS 5.3）— Microsoft SharePoint Server 権限昇格の脆弱性
   - 対象製品: Microsoft SharePoint Enterprise Server 2016
   - 対象KB: 5002891, 5002883, 5002882
   - 概要: SharePoint上で権限を昇格される可能性がある脆弱性です。

## 📢 公開情報あり（Publicly Disclosed）

- **CVE-2026-50661**（重要・CVSS 6.1）— Windows BitLocker セキュリティ機能バイパスの脆弱性
  - 対象製品: Windows 10 Version 1809 for 32-bit Systems ほか
  - 概要: 攻撃手法が既に一般に公開されている脆弱性です（悪用の確認はまだありませんが、情報公開により攻撃発生リスクが高まります）。

## ⚠️ 要注意：CVSSスコア9.8以上でWindows/オンプレミス製品が対象の更新（対処が必要）

CVSS（Common Vulnerability Scoring System、共通脆弱性評価システム）スコアが9.8以上と極めて高く、かつWindowsやオンプレミス製品（自社サーバー等に導入されている製品）が対象の脆弱性です。全12件あります。

| CVE | 重大度 | CVSS | 悪用可能性の指標 | 概要 |
|---|---|---|---|---|
| CVE-2026-57092 | 緊急 | 9.9 | 可能性は低い | Windows VMSwitch 権限昇格 |
| CVE-2026-50522 | 緊急 | 9.8 | 可能性が高い | SharePoint リモートコード実行 |
| CVE-2026-58644 | 緊急 | 9.8 | **悪用検出済み**（上記参照） | SharePoint リモートコード実行 |
| CVE-2026-50518 | 緊急 | 9.8 | 可能性が高い | Windows DHCPサーバー リモートコード実行 |
| CVE-2026-55944 | 緊急 | 9.8 | 可能性が高い | Dynamics NAV / Dynamics 365 Business Central(オンプレ) リモートコード実行 |
| CVE-2026-56159 | 緊急 | 9.8 | 可能性は低い | DHCPサーバーサービス リモートコード実行 |
| CVE-2026-56188 | 緊急 | 9.8 | 可能性が高い | Windows Server ネットワークドライバー リモートコード実行 |
| CVE-2026-42990 | 重要 | 9.8 | 可能性は低い | SQL Server ODBCドライバー 権限昇格 |
| CVE-2026-49172 | 重要 | 9.8 | 低い | Windows FTPサービス リモートコード実行 |
| CVE-2026-54990 | 重要 | 9.8 | 低い | リモートデスクトップクライアント リモートコード実行 |
| CVE-2026-50447 | 重要 | 9.8 | 低い | Windows Message Queuing (MSMQ) リモートコード実行 |
| CVE-2026-56190 | 重要 | 9.8 | 低い | リモートデスクトッププロトコル(RDP) リモートコード実行 |

これらはいずれも `requiresUpdate: true`（更新プログラムの適用が必要）と判定されている項目です。

## ☁️ Azure（クラウド）関連の重大な脆弱性（参考情報・利用者側の更新作業は不要）

Microsoft側でクラウド基盤を修正済みのため、Windows Update等による利用者の対応は原則不要ですが、影響範囲を把握するための参考情報として、CVSS 9.8以上の主なものを挙げます（全13件中の一部抜粋）。

- CVE-2026-56163（CVSS 10）— Azure Kubernetes Service 権限昇格
- CVE-2026-66803（CVSS 10）— Azure Cosmos DB リモートコード実行
- CVE-2026-56191（CVSS 10）— Microsoft Exchange Online 改ざん（Tampering）
- CVE-2026-57106（CVSS 10）— Data Quality 権限昇格
- CVE-2026-62825（CVSS 10）— Azure Key Vault 権限昇格
- CVE-2026-58630（CVSS 10）— Azure App Service on Azure Stack Hub 権限昇格
- CVE-2026-58275（CVSS 10）— Azure DNS 権限昇格
- CVE-2026-45499（CVSS 9.9）— Azure OpenAI 権限昇格
- CVE-2026-57100（CVSS 9.9）— Microsoft Entra Provisioning Service 権限昇格
- CVE-2026-54120（CVSS 9.9）— Microsoft Surface リモートコード実行
- CVE-2026-50517（CVSS 9.9）— Microsoft M365 Copilot リモートコード実行
- CVE-2026-56165（CVSS 9.8）— Microsoft Account リモートコード実行
- CVE-2026-55010（CVSS 9.8）— Minecraft Bedrock Dedicated Server リモートコード実行

## 🛠 対処方法

1. **Windows Update または WSUS（Windows Server Update Services）経由で更新プログラムを適用してください。**
   - 個人PC・少人数環境: 設定 → Windows Update → 更新プログラムのチェック から適用できます。
   - 組織環境: WSUSやIntune等の管理ツールで配信・適用状況を確認してください。
2. 上記「悪用が確認されている脆弱性」「要注意（CVSS 9.8以上）」に該当する製品（特にSharePoint、AD FS、Windows 10/11、DHCPサーバー、RDP関連）を利用している場合は優先的に適用を検討してください。
3. Azure関連の項目はMicrosoft側で対応済みのため、利用者側での個別のパッチ適用作業は基本的に不要です。

> 本タスクではシステムへの更新適用作業（sudo／管理者権限を要する操作）は実行しません。実際の適用は鈴木さんご自身の判断・作業でお願いいたします。

## 出典

- Microsoft Security Response Center (MSRC) Update Guide: https://msrc.microsoft.com/update-guide/

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
