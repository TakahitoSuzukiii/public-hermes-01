作成日: 2026-11-20 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-13〜2026-11-20

# クラウド公式ブログ 週次ホット記事（2026-11-20 版）

## 📌 今週のハイライト
- **Cloudflare** が突出。フランスで DNS リゾルバ（ドメイン名をIPアドレスに変換する仕組み）の Quad9 が撤退した件の解説記事が、はてブ6・HN 902ポイントと大きな反響でした。
- **AWS** は AI エージェント関連（SAP 連携、Amazon MWAA 向けエージェントスキル）と、新しい AWS エクスペリエンスの安全なデフォルト設定、Well-Architected Framework 更新が中心です。
- **Microsoft** はセキュリティブログ中心で、AI コーディングエージェントを狙う攻撃や Microsoft 365 障害を装うフィッシングの話題が並びました。
- **Google Cloud** は反響指標の高い記事が少なく、Linux 向けエージェント型コードレビューの事例が最大でした。
- 脆弱性・攻撃キャンペーンの詳細やスコアは CISA／JPCERT の週報を参照してください。

## 🔥 今週これだけ読む3本
1. **Quad9’s withdrawal from France: A canary in the coal mine**（Cloudflare）— はてブ6 / HN 902pt（コメント450）。理由: 今週最大の反響。DNS レベルのブロック義務化がもたらす影響を扱う。 https://blog.cloudflare.com/quad9-withdrawal-from-france/
2. **新しい AWS エクスペリエンスにおける使いやすさと安全なデフォルト設定**（AWS・日本語）— はてブ2。理由: 日本語で読め、初期設定の安全性という実務に近い話題。 https://aws.amazon.com/jp/blogs/news/ease-of-use-and-secure-defaults-in-the-new-aws-experience/
3. **Sashiko: Lessons from building an agentic code review system for Linux**（Google Cloud）— HN 3pt。理由: Google Cloud で最も指標が高く、AI エージェントによるコードレビューの実例。 https://cloud.google.com/blog/products/application-development/lessons-from-building-sashiko-an-agentic-code-review-system/

## 🏢 ベンダー別ホット記事

### Google Cloud
今週は反響の大きい記事は少なめです（走査39件中、指標ありは2件）。
- **Sashiko: Linux 向けエージェント型コードレビューシステム構築の教訓**（2026-11-19）— はてブ0 / HN 3pt（https://news.ycombinator.com/item?id=50553280）。大規模OSSの開発速度に対し、AI エージェント（自律的に作業するAI）でレビューを支援した知見の紹介。 https://cloud.google.com/blog/products/application-development/lessons-from-building-sashiko-an-agentic-code-review-system/
- **ARMORY CASTLE Exploits vSphere**（2026-11-19）— はてブ0 / HN 1pt（https://news.ycombinator.com/item?id=50560544）。Google の脅威インテリジェンスによる攻撃活動の解説。詳細は原文および CISA/JPCERT を参照。 https://cloud.google.com/blog/topics/threat-intelligence/armory-castle-exploits-vsphere/
- 新着（日本語）: **問題を検出するだけでなく修正まで行う: pull リクエストで CodeMender を実行する方法**（2026-11-19、指標なし）。 https://cloud.google.com/blog/ja/products/identity-security/how-to-run-codemender-in-your-pull-requests/
- 新着（日本語）: **Cloud CISO の視点: 2027 年のセキュリティ動向予測**（2026-11-19、指標なし）。 https://cloud.google.com/blog/ja/products/identity-security/cloud-ciso-perspectives-our-security-forecast-2027/

### AWS
- **新しい AWS エクスペリエンスにおける使いやすさと安全なデフォルト設定**（2026-11-18/19）— はてブ2 / HNなし。MFA（多要素認証）登録可能なビルダーID、Organizations で管理される組織・プロジェクト、データ境界などを最初から適用する方針を紹介。 https://aws.amazon.com/jp/blogs/news/ease-of-use-and-secure-defaults-in-the-new-aws-experience/
- **AWS Well-Architected Framework のアップデートを発表**（2026-11-18）— はてブ2。6つの柱すべてで新規ガイダンス追加・既存改善。 https://aws.amazon.com/jp/blogs/news/announcing-updates-to-the-aws-well-architected-framework-3/
- **AI エージェントをより SAP の身近に: AWS for SAP MCP Server の新機能**（2026-11-18）— はてブ2。SuccessFactors 連携、OData V4 対応、Microsoft Entra ID 対応のアイデンティティ伝播などの追加。MCP は AI が外部ツールとつながる共通規格。 https://aws.amazon.com/jp/blogs/news/bringing-ai-agents-closer-to-sap-whats-new-in-aws-for-sap-mcp-server/
- **AWS エージェントスキルを使った Amazon MWAA のアップグレードとトラブルシューティング**（2026-11-19）— はてブ1。Airflow 環境の更新や DAG の調査をエージェントスキルで支援する手順。 https://aws.amazon.com/jp/blogs/news/upgrading-and-troubleshooting-amazon-mwaa-with-aws-agent-skills/
- **生成 AI セキュリティを強化する – SATv2 で始めるマルチアカウント環境の LLM ジャッキング対策**（2026-11-19）— はてブ1。LLM ジャッキングは他人のクラウド資格情報で生成AIを不正利用される攻撃。 https://aws.amazon.com/jp/blogs/news/llmjacking-protection-with-satv2/
- （参考・英語）Amazon Threat Intelligence の ARTEX AI エージェントによるサイバー犯罪観測（2026-11-14、HN 5pt: https://news.ycombinator.com/item?id=50512675）。 https://aws.amazon.com/blogs/security/amazon-threat-intelligence-observes-threat-actors-running-cybercrime-campaigns-with-artex-ai-agents/

### Microsoft
今週は指標の大きい記事はありません（走査5件、いずれもセキュリティブログ）。
- **High volume phishing campaign uses Microsoft 365 outage lures**（2026-11-17）— はてブ2。Microsoft 365 の障害を装ったフィッシングの観測。 https://www.microsoft.com/en-us/security/blog/2026/11/16/high-volume-phishing-campaign-uses-microsoft-365-outage-lures-target-multiple-industry-sectors-2/
- **Security for the agentic era, powered by Microsoft Perception**（2026-11-18）— はてブ1。AI エージェント時代向けのセキュリティ製品群の更新紹介。 https://www.microsoft.com/en-us/security/blog/2026/11/17/security-for-the-agentic-era-powered-by-microsoft-perception/
- **SCKit abuses ScreenConnect…**（2026-11-14）— はてブ1。リモート接続ツール悪用の攻撃チェーンと対策。 https://www.microsoft.com/en-us/security/blog/2026/11/13/sckit-abuses-screenconnect-deploy-remote-access-target-technician-sessions/
- 関連: AI コーディングエージェントのデバイスコード認証リスク（https://www.microsoft.com/en-us/security/blog/2026/11/17/the-risks-of-device-code-authentication-for-ai-coding-agents/）。

### Cloudflare
- **Quad9’s withdrawal from France: A canary in the coal mine**（2026-11-18）— はてブ6 / HN 902pt・450コメント（https://news.ycombinator.com/item?id=50538994）。公開DNSリゾルバにコンテンツブロックを義務づける危険性を論じる。 https://blog.cloudflare.com/quad9-withdrawal-from-france/
- **Kitesurf is now open source**（2026-11-14）— はてブ3 / HN 5pt（https://news.ycombinator.com/item?id=50518495）。AIエージェント向け実験的ブラウザエンジンのOSS化。 https://blog.cloudflare.com/kitesurf-open-source/
- **Introducing Spend Management**（2026-11-13）— はてブ1 / HN 6pt（https://news.ycombinator.com/item?id=50483797）。Workers 等の利用上限・アラート機能。 https://blog.cloudflare.com/spend-management/
- **An updated Clairic and Clairic-flash are now open-weight**（2026-11-19）— はてブ2 / HN 2pt。Workers AI の抽出モデルをオープンウェイト公開。 https://blog.cloudflare.com/open-clairic/
- **Adapting to AI penetration testing orchestrators**（2026-11-14）— はてブ0 / HN 2pt。 https://blog.cloudflare.com/adapting-to-ai-penetration-testing-orchestrators/

## 🌐 Hacker Newsで話題（公式ブログのフィード外）
| タイトル | ポイント | コメント数 | HNリンク |
|---|---|---|---|
| What's new in the .NET 11 runtime（Microsoft Learn） | 256 | 1 | https://news.ycombinator.com/item?id=50439284 |
| Announcing .NET 11（Microsoft DevBlogs） | 240 | 317 | https://news.ycombinator.com/item?id=50442225 |
| AWS Nitro Sandboxes on Amazon EKS, ECS and EC2 | 30 | 1 | https://news.ycombinator.com/item?id=50428199 |

※いずれも11月9〜10日公開で対象期間の直前ですが、HNでの反響が継続しています。

## ℹ この記事の見方
- 人気指標は **2026-11-20 取得時点** の「はてなブックマーク数」と「Hacker News（HN）ポイント」で、score はその合計です。
- 指標は人気の目安であり、正確性を保証しません。要約は公式フィードのタイトル・概要に基づきます。
- 取得できなかった情報源: なし（全フィード取得成功）。ただし Azure Blog・Microsoft DevBlogs・Cloudflare Blog（日本語）は期間内の記事が0件でした。

## 出典
- Google Cloud Blog（日本語/英語）公式フィード
- AWS 日本語ブログ / AWS News Blog / AWS Architecture Blog / AWS Security Blog 公式フィード
- Azure Blog / Microsoft DevBlogs / Microsoft Security Blog 公式フィード
- Cloudflare Blog（日本語/英語）公式フィード
- はてなブックマーク件数API、Hacker News（Algolia）API

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
