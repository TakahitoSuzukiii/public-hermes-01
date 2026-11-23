作成日: 2026-11-24 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-17〜2026-11-24

# Qiita クラウド人気記事 週報（AWS / Google Cloud / Azure / Cloudflare）

## 📌 今週のハイライト
- **AI エージェント関連が全分野で目立つ週**。AWS では AI エージェントの認証（pre:Invent 関連）や設計論、Azure では Ignite 2026 の速報が多く出ました。
- **AWS**: S3 Vectors（ベクトル＝文章などを数値化したデータを保存する S3 の機能）と OpenSearch の比較、AWS Emulator（ローカルで AWS 風環境を動かす公式エミュレータ）の試用記事が人気。
- **Azure**: Ignite 2026 で Azure AI Search が「Foundry IQ」へ名称変更された話題が中心。
- **Google Cloud / Cloudflare**: 件数・反応とも小さめ。Cloudflare は Workers（エッジで動くサーバレス実行環境）の実装・性能改善の記事が中心。
- 脆弱性関連の話題（CodeMender、nginx 関連など）は本記事では深掘りしません。詳細・スコアは CISA／JPCERT の週報を参照してください。

## 🔥 今週これだけ読む3本
1. **【実験】Direct Connectの片系を落とすと、実際どれくらいで切り替わり、行きと戻りはどの回線を通るのか**（いいね20 / ストック5）
   - 理由: 専用線（Direct Connect）の冗長構成を実測した記事で、設計判断に直結する具体的な知見が得られそうです。
   - https://qiita.com/sh_fukatsu/items/5a069f9fce99a86efb05
2. **【pre:Inventまとめ】AWSのAIエージェント認証がいろいろ進化！MCPサーバー構築を例に一挙解説**（いいね20 / ストック6）
   - 理由: AI エージェントの認証という今週の主要トレンドを、MCP（AI と外部ツールをつなぐ共通規格）の例でまとめた内容です。
   - https://qiita.com/minorun365/items/bd6091f2599a0f37326b
3. **[AWS] S3Vectorsは全文検索エンジンとしてOpenSearchの代わりになるのか？**（いいね21 / ストック9）
   - 理由: 新サービスと既存サービスの使い分けを比較する、選定時に役立つテーマです。
   - https://qiita.com/kikuziro/items/cd1389f6a1601494895f

## 📝 タグ別ホット記事（直近7日）
※ 数値は取得時点（2026-11-24）の値。各節、宣伝色・クラウドと関連の薄い記事は一部除外しています。

### AWS（走査190件から選定／除外4件）
- **人間がボトルネックになった時代のAIエージェント設計**（いいね23 / ストック13 / 2026-11-18）— AI エージェント時代の開発・設計の考え方を論じた記事（Organization: kddiagile）。https://qiita.com/Syoitu/items/5bb47c01a8513e52d1b5
- **[AWS] S3Vectorsは全文検索エンジンとしてOpenSearchの代わりになるのか？**（21 / 9 / 2026-11-17）— S3 Vectors と OpenSearch の検索機能を比較。https://qiita.com/kikuziro/items/cd1389f6a1601494895f
- **【pre:Inventまとめ】AWSのAIエージェント認証が…**（20 / 6 / 2026-11-21）— エージェント認証の進化点を MCP サーバー構築例で解説。https://qiita.com/minorun365/items/bd6091f2599a0f37326b
- **【実験】Direct Connectの片系を落とすと…**（20 / 5 / 2026-11-18）— 回線障害時の切替時間と経路を実測。https://qiita.com/sh_fukatsu/items/5a069f9fce99a86efb05
- **【AWS Emulator】消し忘れの恐怖から卒業！公式エミュレータでS3とLambdaを動かしてみた**（9 / 7 / 2026-11-18）— ローカルで S3・Lambda を試し、課金の消し忘れを防ぐ話（Organization: iret）。https://qiita.com/N-Kyo/items/a111d174a751506790e2

### Google Cloud（走査23件から選定／除外4件）
- **【Gemini 4 Hydrogen】「とりあえず一番上」から卒業！Agent Studioで試す手順**（7 / 7 / 2026-11-19）— モデルの選び方を Agent Studio で試す手順（Organization: iret）。https://qiita.com/N-Kyo/items/80ac96fd59b08b1a879a
- **【自動修復AI】脆弱性を自動検知・修正する「CodeMender」とAIエージェント時代のセキュリティ基盤**（6 / 2 / 2026-11-19）— 自動修復 AI の紹介。※脆弱性の詳細は CISA／JPCERT 週報を参照。https://qiita.com/tomokoro/items/64a762de9e5bdf3e8f00
- **CDNが「キャッシュを近くに置く」以上にわからなかったので…AWS/GCPの構成まで調べて整理した**（1 / 1 / 2026-11-21）— CDN の仕組みと両クラウドの構成を整理。https://qiita.com/Pippichannnn/items/ef11cd8fe8fb5fc8e4a2
- **AWS ユーザー向け Google Cloud IAM 入門：権限は「リソース側」に書く**（0 / 0 / 2026-11-23）— AWS 経験者向けに IAM（権限管理）の考え方の違いを説明。https://qiita.com/leomarokun/items/d602adf22377679cf27e
- **gcloudのアカウントとプロジェクトをプロンプトに表示する「gcloud-ps1」を公開しました**（0 / 0 / 2026-11-23）— 操作ミス防止のための CLI 補助ツール。https://qiita.com/motuneko253/items/d7477100be56aa0d48ed

### Microsoft Azure（走査28件から選定／除外4件）
- **【Ignite 2026速報】Azure AI Search が Foundry IQ にリブランドし、2 種類のナレッジグラフ機能を搭載！ほか**（8 / 4 / 2026-11-18）— 名称変更と新機能の速報。https://qiita.com/nohanaga/items/21f3f3a1d2ecb14262b6
- **【前編】初めての海外出張で MS Ignite 2026 へ！出発〜バッジ受け取り**（6 / 2 / 2026-11-17）— 現地参加レポート（Organization: biprogy）。https://qiita.com/KoheiKushida/items/17d814af2e95a84a580d
- **【Autonomous AI Database】ADB-S@AzureのMCPサーバーにVS Code＋Clineから接続する**（5 / 1 / 2026-11-17）— Azure 上の Oracle DB に MCP で接続する手順（Organization: oracle）。https://qiita.com/marfujim/items/9018cba516cc1cbb31ba
- **Foundry IQ ナレッジグラフ解体新書**（2 / 2 / 2026-11-21）— ナレッジグラフ（情報同士の関係を網状に表すデータ）の種類を実装面から解説。https://qiita.com/nohanaga/items/60a56ef65194ab94b1d9
- **【Azure】証明書の自動更新をサービス別に整理する**（1 / 2 / 2026-11-19）— App Service 等での証明書更新の整理（Organization: fujitsu）。https://qiita.com/pienhalifax/items/d0713c39b7ae515ea359

### Cloudflare（走査44件から選定／除外4件）
※ 反応数は全体に小さい週です。
- **Next.js を TanStack Start に替えたら Cloudflare Workers の CPU 時間が 10 分の 1 に**（1 / 1 / 2026-11-21）— フレームワーク変更による CPU 時間削減の事例。https://qiita.com/HoneyMarron/items/91233edae62c04d5e2a8
- **既存サイトに手を入れずに多言語化する翻訳プロキシを Cloudflare Workers で作って分かった6つの設計ポイント**（1 / 1 / 2026-11-19）— 翻訳プロキシ構築の設計知見。https://qiita.com/MadTotoro/items/bdfe06672e95ce0c0589
- **Cloudflareの後ろに置いたApacheで、ログとIP単位の上限を実クライアントIPに戻す**（0 / 1 / 2026-11-20）— mod_remoteip の信頼範囲設定の解説。https://qiita.com/itaraiguma/items/9d5654ba676a8b0e397b
- **【個人開発】第3回：Cloudflareで独自ドメインのWebメールを作る**（0 / 1 / 2026-11-17）— D1（Cloudflare のデータベース）を使った連載（Organization: future-creation-factory）。https://qiita.com/kandu/items/dbd28f137773ec25efcb
- **nginxに2015年からの穴 ― Cloudflareの分析「nginx2root」を読んだ**（1 / 0 / 2026-11-20）— 脆弱性関連の話題。詳細・スコアは CISA／JPCERT 週報を参照。https://qiita.com/oosawak@github/items/71e509974faa05a1d72f

## 📚 定番（直近30日・ストック20以上）
### AWS
- **集中力散漫＆過集中持ちエンジニアがAWS DEAを突破した「過集中スイッチ」の入れ方**（ストック107）https://qiita.com/kohYoung_I/items/cce40cb5b9cdfc1f8787
- **AI駆動開発の次の段階: ソフトウェアファクトリー**（ストック105）https://qiita.com/Syoitu/items/9364a0a175893bb15219
- **実際に試したClaude便利術20選 まとめ**（ストック81）https://qiita.com/N-Kyo/items/bf4a3a2185db2d28eee5
### Google Cloud / Microsoft Azure / Cloudflare
- 該当なし

## ℹ この記事の見方
- いいね数・ストック数（あとで読む保存数）は **取得時点（2026-11-24）の値**です。**人気の目安であり、正確性を保証するものではありません。**
- ホット＝直近7日の新着をいいね＋ストック順、定番＝直近30日でストック20以上の記事。要約はタイトル等から読み取れる範囲で記載しています。
- 取得できなかった情報源: なし

## 出典
- Qiita API v2（公式 API）: https://qiita.com/api/v2/docs
- 各記事の URL は上記本文を参照

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
