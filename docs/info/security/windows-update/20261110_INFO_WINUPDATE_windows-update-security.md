作成日: 2026-11-10T08:00:00Z / STATUS: INFO / TOPIC: WINUPDATE / 対象月: November 2026 Security Updates

# Windows Update月次セキュリティ更新 監視レポート（2026年11月）

MSRC（Microsoft Security Response Center＝マイクロソフト製品の脆弱性情報を一元管理する公式窓口）が公開した2026年11月分（米国時間11月10日公開）の情報をまとめました。

## 📊 全体サマリー

- 総CVE（共通脆弱性識別子＝脆弱性ごとの管理番号）件数: **1,362件**（MSRC CVRF API集計。報道各社の件数は集計範囲の違いで1,092〜1,259件と幅あり）
- 重大度別（MSRCのラベル。CVSSではありません）
  - Critical（緊急）: **69件** / Important（重要）: **1,132件** / Moderate（警告）: **113件** / Low（注意）: **48件**
- 悪用済み: **1件** ／ 悪用の可能性が高い（Exploitation More Likely）: **42件** ／ CVSS9.8以上の要更新: **16件**

## 🚨 悪用済み（Exploited）— 最優先

### CVE-2026-124194 Microsoft Outlook なりすまし（Spoofing）の脆弱性

| 項目 | 内容 |
|---|---|
| 対象 | Microsoft 365 Apps for Enterprise / Office LTSC 2021 / Office LTSC 2024（Outlook）。※Windows累積更新ではなく**Office側の更新**で修正 |
| MSRC重大度 | Moderate |
| CVSS v3.1 | **6.5 MEDIUM**（`AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:N/A:N`）出所: **NVD掲載のCNA（Microsoft）採点＝Secondary**。NVD自身（Primary）の採点は未確認 |
| OWASP Risk Rating（推定） | 尤度5.75 MEDIUM × 影響4.75 MEDIUM ⇒ **Medium**（推定） |
| OWASP Top10:2025（推定） | CWE-356（危険な操作をUIが警告しない）→ **A06 Insecure Design** 相当と推定（公式Mapped CWEsとの照合は未実施） |

**根拠（推定の要因値）:** skill3/motive9（実際に悪用中）/opportunity4（ユーザーがファイルを開く必要あり）/size9（メール経由で誰にでも送れる）、discovery7/exploit5/awareness6/detection3。影響は機密性6（NTLMv2ハッシュ漏えい）/完全性5/可用性1/追跡可能性7。業務影響は環境依存のため採点していません。

**深掘り解説**
- **対象:** Outlook（メールソフト）。一般的なOffice利用PCに広く存在します。Outlook/Microsoft 365アプリを使っているPCは**関係あり**です。
- **脆弱性の種類:** 危険な動作の前に出るべき警告（外部コンテンツの警告）が出ない「UI警告の欠落」。
- **攻撃の流れ:** ①攻撃者が細工したメッセージファイル（.msg等）を送る → ②被害者がOutlookで開く → ③警告なしで攻撃者のネットワーク上の場所へ自動接続 → ④**NTLMv2ハッシュ**（Windowsのパスワードから作られる認証用の値）が流出 → ⑤攻撃者がハッシュを他システムへ中継（リレー）してなりすますか、解読してパスワードを復元。**プレビューウィンドウでは発動しません**（開く操作が必要）。
- **悪用状況:** Microsoftは悪用を確認済みですが、攻撃グループ名・マルウェア名・手口の詳細は**公開されていません**。CISA（米国サイバーセキュリティ機関）のKEV（既知の悪用脆弱性カタログ）に追加済みで、米連邦機関の対処期限は2026-11-24。発見者は「nono」氏とBenoît Sevens氏（Anthropic社のClaude AI利用の記載あり）。
- 参照: SecurityWeek / The Hacker News / Qualys / Malwarebytes / Dark Reading（Tenableコメント）の報道で横断確認。

## ⚠️ 要注意（Exploitation More Likely かつ更新必須の主なもの）

「悪用される可能性が高い」とMSRCが評価した主な項目です。

| CVE | 内容 | MSRC重大度 | CVSS v3.1 | OWASP RR（推定） | Top10:2025 |
|---|---|---|---|---|---|
| CVE-2026-118207 | Exchange Server RCE（遠隔コード実行）。対象: Exchange Server SE（KB5133453） | Critical | 8.8（CNA=Secondary） | 尤度4.88×影響7.0 ⇒ High | 対象外（CWE-706の対応は未確認） |
| CVE-2026-118146 | Active Directory Domain Services RCE | Critical | 8.8（CNA=Secondary） | 尤度4.88×影響7.0 ⇒ High | A01（CWE-863） |
| CVE-2026-119952 | Windows Schannel（TLS処理部品）RCE | Critical | 8.1（MSRC値） | 尤度4.62×影響7.0 ⇒ High | 対象外 |
| CVE-2026-113862 | Windows NAT RCE | Critical | 8.1（MSRC値） | 同上 ⇒ High | 対象外 |
| CVE-2026-118148 | AD DS 特権昇格 | Critical | 7.5（MSRC値） | 同上 ⇒ High | 未判定 |
| CVE-2026-121662/121663 | Visual Studio Code RCE / セキュリティ機能回避 | Important | 8.6 / 8.8（MSRC値） | 尤度4.88×影響7.0 ⇒ High | 未判定 |
| 他約30件 | Windows Installer・Print Spooler・Kernel・Graphics Kernel・WMI・Task Scheduler・HTTP.sys・SMB Client等の特権昇格、TCP/IP DoS | Important | 7.0〜7.8（MSRC値） | ローカル特権昇格が中心。個別の算出は省略 | OS系は対象外 |

> 💡 「MSRC値」はNVD APIで個別確認していないもの（MSRC CVRF記載のCVSS v3.1）。全件のNVD照合はレート制限のため今回は一部のみ実施しました。

## 🔴 CVSS 9.8以上（Windows/オンプレ）の一覧

いずれも「Exploitation Less Likely（悪用の可能性は低い）」評価ですが、認証不要のネットワーク経由で攻撃可能な点が共通です。サーバ用途のものが大半で、一般的な開発PCに直接影響する範囲は限定的です。

**OWASP Risk Rating（推定・共通）:** 尤度5.38 MEDIUM × 影響8.5 HIGH ⇒ **High**（skill5/motive4/opportunity7/size9、discovery3/exploit3/awareness4/detection8、機密9/完全9/可用9/追跡7）。

| CVE | 内容（対象） | MSRC | CVSS v3.1（NVD上のCNA=Secondary） | Top10:2025 |
|---|---|---|---|---|
| CVE-2026-112967 | Xbox Live Networking Service RCE | Critical | 9.8 | 対象外（CWE-122ヒープオーバーフロー） |
| CVE-2026-116928 | Windows Search RCE | Critical | 9.8 | 対象外（CWE-787 範囲外書き込み） |
| CVE-2026-119958 | LDAP（ディレクトリ検索プロトコル）RCE | Critical | 9.8 | 対象外（CWE-787） |
| CVE-2026-85844 | Kerberos（認証方式）特権昇格 | Important | 9.8 | A07（CWE-288 認証回避。推定） |
| CVE-2026-88218 | DNS Server RCE | Important | 9.8 | 対象外（CWE-415 二重解放） |
| CVE-2026-88234 | iSCSI RCE | Important | 9.8 | 対象外（CWE-763） |
| CVE-2026-88243 | DHCP Server RCE | Important | 9.8 | 対象外（CWE-125） |
| CVE-2026-95882 / 95901 | DirectMusic RCE | Important | 9.8 | 対象外（CWE-121/415） |
| CVE-2026-96067 / 96078 | Color Management RCE | Important | 9.8 | 対象外（CWE-190/122） |
| CVE-2026-96157 | Media Foundation RCE | Important | 9.8 | 対象外（CWE-122） |
| CVE-2026-116945 | SQL Server 2025 RCE | Important | 9.8 | 対象外（CWE-122） |
| CVE-2026-120002 | SharePoint Server SE 特権昇格 | Important | **9.9（NVD=Primary扱い、出所Microsoft）** | A01（CWE-863） |

※ SOCRadarは、Windows Search（CVE-2026-116928）をExchangeのCVE-2026-118207と同じメンテナンス枠で適用するよう推奨しています。

## ☁️ Azure/クラウド関連の重大なもの（利用者の対応は原則不要・参考）

| CVE | 内容 | CVSS v3.1 | OWASP RR（推定） | Top10:2025 |
|---|---|---|---|---|
| CVE-2026-109469 | Entra Device Registration 特権昇格 | **10.0**（CNA=Secondary） | 尤度5.38×影響8.5 ⇒ High | A01（CWE-639 ユーザー制御キーによる認可回避） |
| CVE-2026-119990 | Azure OpenAI 特権昇格 | 9.8（CNA=Secondary） | 同上 ⇒ High | A07（CWE-306 重要機能の認証欠如） |
| CVE-2026-109467 | Azure DevOps Server RCE（オンプレ版は更新必要） | 9.9（CNA=Secondary） | 尤度4.62×影響7.0 ⇒ High（推定） | A07（CWE-287） |

## 📰 MSRC公式ブログの補足情報

出典: https://www.microsoft.com/en-us/msrc/blog/2026/11/202611-security-update （日本語版。ブログ本文への直接アクセスは403で拒否されたため、**検索結果に表示された本文抜粋**から取得。全文は未確認）

- **主な注意点:** 更新公開前から悪用が確認されているのは **CVE-2026-124194（Outlookなりすまし）** のみ。早急に適用するよう呼びかけ。
- **Windows Server 2022 Datacenter: Azure Edition:** 今月はホットパッチ（再起動不要の更新）ではなく**再起動が必要なベースライン更新**。ホットパッチ利用環境のみ影響。
- **Exchange Server:** 展開時はExchangeチームブログ「Released: November 2026 Exchange Server Security Updates」を併せて参照。
- **既知の問題（Known Issues）:** 各KBに記載。報道では、KB5132061/KB5132059（Windows 11 26H2/26H1）は「既知の問題なし」。PowerShellが署名済みスクリプトのエンコード検証を厳格化し、不正なUTF-8のスクリプトは署名検証に失敗する場合あり（BOM付きUTF-8で保存し再署名）。12月後半はオプションのプレビュー更新なし（1月再開）。
- 既存の脆弱性情報87件が情報更新のみ（追加対応不要）。

## 🛡 対処方法

- **Windows:** Windows Update／WSUS（社内更新配信サーバ）経由で11月累積更新（例: KB5132061、KB5132059、KB5131087 等、OS別）を適用。
- **Office/Outlook:** Officeアプリで「ファイル → アカウント → 更新オプション → 今すぐ更新」。管理端末は管理者に確認。
- **Exchange/SQL/SharePoint:** 該当サーバ管理者が個別の更新を適用（Exchange SEはKB5133453）。
- 暫定策（Outlook）: 出所不明の.msg等を開かない。
- 本タスクではsudo／管理者権限が必要な操作は一切実行していません。

## 📝 注記（スコアの扱い）

- CVSSはNVDに載っているCNA（Microsoft）採点＝Secondaryを記載。NVD自身のPrimary採点が確認できたのはCVE-2026-120002のみ。MSRCの重大度ラベルはCVSSとは別物。
- OWASP Risk Ratingは技術ベースの**推定**（業務影響は未採点）。Top10:2025の対応も一部は推定で、公式カテゴリページとの照合は未実施。メモリ破壊系・OS系は「対象外（Webアプリ向け分類のため）」。
- 報道各社で件数が異なるため、本稿の件数はMSRC CVRF API集計値。

## 出典

- https://msrc.microsoft.com/update-guide/
- https://api.msrc.microsoft.com/cvrf/v3.0/cvrf/2026-Nov
- https://services.nvd.nist.gov/ （NVD API）
- SecurityWeek / The Hacker News / Qualys / Malwarebytes / Dark Reading / SOCRadar 各社11月Patch Tuesday記事

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
