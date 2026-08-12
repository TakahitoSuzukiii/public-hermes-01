作成日: 2026-08-11 / STATUS: INFO / TOPIC: WINUPDATE / 対象月: August 2026 Security Updates

# Windows Update月次セキュリティ更新レポート（2026年8月）

Microsoft公式のMSRC（Microsoft Security Response Center：マイクロソフト セキュリティ対応センター）が公開するCVRF（Common Vulnerability Reporting Framework：共通脆弱性報告フォーマット）APIから取得した、2026年8月分（Patch Tuesday：毎月第2火曜日に一斉公開されるセキュリティ更新）の情報をまとめます。

- 公開日（initial release）: 2026-08-11
- 総脆弱性件数: 790件

## 重大度別 件数

| 重大度 | 件数 |
|---|---|
| Critical（緊急） | 108 |
| Important（重要） | 397 |
| Moderate（警告） | 207 |
| Low（注意） | 32 |
| Unknown（不明） | 46 |

## 🚨 悪用済み（Exploited）— 最優先対応

MicrosoftがWild（実際の攻撃）で悪用を確認したゼロデイ脆弱性（脆弱性が公表・修正される前から悪用が始まっているもの）です。**最優先で更新適用を検討してください。**

- **CVE-2026-68820**（Important, CVSS 7.0）
  Windows Ancillary Function Driver for WinSock Elevation of Privilege Vulnerability（Windows AFD／WinSockの権限昇格の脆弱性）
  対象製品: Windows 10 Version 1809 for 32-bit Systems ほか
  対象KB: 5120238, 5120242, 5120229, 5120249, 5120233, 5120228, 5121003, 5120994, 5120240, 5121000, 5120418, 5120386, 5120385
  概要: WinSock用の補助関数ドライバ（AFD.sys）に権限昇格の脆弱性があり、既に悪用（Exploitation Detected）が確認されています。ローカル攻撃前提ですが、既知の攻撃実績があるため優先度は最上位です。

## ⚠️ 要・更新適用（CVSS 9.8以上、オンプレミス/Windows対象）

CVSS（Common Vulnerability Scoring System：脆弱性の深刻度を10点満点で評価する指標）9.8以上、かつ実機での更新適用が必要な脆弱性です。

| CVE | 重大度 | CVSS | Exploitability Index（悪用可能性の指標） | 概要 |
|---|---|---|---|---|
| CVE-2026-62815 | Critical | 9.8 | N/A | Microsoft QUIC（次世代通信プロトコル）のリモートコード実行 |
| CVE-2026-62878 | Critical | 9.8 | Exploitation Less Likely（悪用の可能性は低い） | Windows DNS Serverのリモートコード実行 |
| CVE-2026-62893 | Critical | 9.8 | Exploitation More Likely（悪用の可能性が高い） | Windows Deployment Services TFTP Serverのリモートコード実行 |
| CVE-2026-65791 | Critical | 9.8 | Exploitation Unlikely（悪用の可能性は低い） | Windows iSCSI Target Serviceのリモートコード実行 |
| CVE-2026-59124 | Important | 9.8 | Exploitation More Likely（悪用の可能性が高い） | Microsoft HPC（High Performance Computing）Packのリモートコード実行 |

特に **CVE-2026-62893**（Windows Deployment Services TFTP Server）と**CVE-2026-59124**（HPC Pack）は「Exploitation More Likely（今後悪用される可能性が高い）」と評価されており、次点で注意が必要です。

## ☁️ Azureクラウド関連の重大な脆弱性（利用者側の対応不要・参考情報）

Azure等のクラウドサービス側で修正済み、またはMicrosoft側で対応するため、利用者によるパッチ適用は不要な脆弱性です（CVSS 9.8以上）。参考情報として列挙します。

- CVE-2026-63508（CVSS 10）Microsoft Planetary Computer Pro 権限昇格
- CVE-2026-56162（CVSS 10）Azure SQL Database 権限昇格
- CVE-2026-65667（CVSS 10）Microsoft Teams 権限昇格
- CVE-2026-50515（CVSS 9.9）Azure Service Bus リモートコード実行
- CVE-2026-59115（CVSS 9.9）Microsoft Entra Provisioning Service 権限昇格
- CVE-2026-50481（CVSS 9.9）Azure Active Directory 権限昇格
- CVE-2026-62830（CVSS 9.9）Azure SRE Agent 権限昇格
- CVE-2026-62873（CVSS 9.8）Microsoft 365 Admin Center 権限昇格

（参考: Azure Linux（OSS基盤）関連の高深刻度脆弱性も45件確認されていますが、こちらもクラウド側対応のため個別列挙は割愛します。）

## その他の注目すべき脆弱性

- **CVE-2026-62832**（Important, CVSS 7.8）Windows User Profile Service 権限昇格 — 一般に公開済み（Publicly Disclosed：詳細情報が既に公開されている）
- **CVE-2026-72971**（Important, CVSS 5.5）Windows Container Isolation FS Filter Driver（unionfs.sys）改ざん — 一般に公開済み
- Exploitation More Likely（悪用の可能性が高い）と評価された脆弱性は全体で34件あります。代表例として、SharePoint Serverのリモートコード実行（CVE-2026-65665, CVE-2026-63520）、Windows DHCP Serverのリモートコード実行（CVE-2026-62823）などが含まれます。

## 対処方法

1. Windows Update（Windowsの標準アップデート機能）またはWSUS（Windows Server Update Services：組織内向けの更新配布サーバー）経由で、上記対象KBを含む最新の累積更新プログラムの適用を推奨します。
2. 特に「悪用済み（Exploited）」「Exploitation More Likely」に分類された脆弱性を含む更新は優先的にご対応ください。
3. 本レポートは情報提供のみを目的としており、**sudo／管理者権限を要する更新適用作業は本タスクでは実行しません。** 実際の適用は管理者権限をお持ちの方が、動作確認の上で計画的に実施してください。

## 出典

- Microsoft Security Response Center Update Guide: https://msrc.microsoft.com/update-guide/

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
