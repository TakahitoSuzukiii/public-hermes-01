作成日: 2026-09-03 / STATUS: INFO / TOPIC: OUTAGE / 対象期間: 2026-08-27〜2026-09-03

# 週次まとめ: Microsoft 365 大規模障害（2026-09-03）

## 🌐 メガテック系

### 1. Microsoft 365 大規模障害（Exchange Online中心に拡大）
- **発生日:** 2026年9月1日
- **対象サービス:** Microsoft 365（マイクロソフトが提供する統合オフィスサービス群）のうち、Exchange Online（クラウド版メールサーバー）を中心に、Outlook・Teams・Azure（マイクロソフトのクラウド基盤）の一部機能にも影響が波及
- **原因:** 本記事作成時点で根本原因の公式発表は未確認。障害はExchange Onlineから始まり、複数のAzureサービス（Azure Cache for Redis＝キャッシュ高速化サービス、Azure Cosmos DB＝データベースサービス、Azure Storage＝クラウドストレージ等）にも影響が及んだと報じられています
- **影響範囲:** メール遅延、Outlook/Teamsの利用不可・機能低下など、法人利用者を中心に広範囲へ影響
- **復旧状況:** 9時間以上に及ぶ長時間障害となり、Microsoftは9月1日時点で「緩和策が進行中で改善傾向」「引き続き経過観察中」とアナウンス。本記事作成時点で完全復旧の公式報告は確認できていません
- **出典:** https://techcrunch.com/2026/09/01/microsoft-365-outage-drags-on-but-things-are-improving/ , https://www.crn.com/news/cloud/2026/microsoft-365-nine-hour-plus-outage-5-things-to-know , https://thecybersecguru.com/news/microsoft-365-outlook-teams-azure-down/

上記以外では、AWS・Google Cloud・Cloudflare・Meta（Facebook/Instagram）・Appleについて、対象期間内に発生したと確認できる大規模障害の報道は見つかりませんでした（Cloudflareのステータスページ上には成田・高雄など局所的な軽微インシデントの記録がありますが、サービス全体への影響を伴う大規模障害ではないため、本記事では割愛します）。

## 🇯🇵 日系企業系

今週（2026年8月27日〜9月3日）については、通信キャリア（NTTドコモ・au・ソフトバンク）、銀行・証券（みずほ・三菱UFJ・SBI証券等）、決済（PayPay等）、物流・小売の各分野で、対象期間内に発生したと確認できる新規の重大障害情報は、検索範囲内では見つかりませんでした。

なお、みずほ銀行については2026年9月12日〜13日にシステムメンテナンスによるサービス休止が予告されていますが、これは計画済みメンテナンスであり障害には該当しないため、参考情報として付記するにとどめます（出典: https://www.mizuhobank.co.jp/corporate/oshirase/maintenance_corporate.html ）。今週は大きな障害の報告なしと判断しました。

## 所感

今週はメガテック側でMicrosoft 365の大規模障害が目立ちました。9時間超という長時間に及び、Exchange OnlineからAzureの複数サービスへ影響が波及した点は、単一コンポーネント起因ではなく基盤側の広範な問題だった可能性を示唆しています。マイクロソフトは先々週もTeams・365で短時間の障害を起こしており、大型クラウド基盤における障害の頻発傾向が続いている印象です。一方、日系企業側は通信・金融・物流のいずれも新規の重大障害報道は確認されず、前週・前々週に続き比較的落ち着いた週でした。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
