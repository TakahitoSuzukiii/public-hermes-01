作成日: 2026-10-13 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-10-06〜2026-10-13

# Qiita クラウド人気記事 週報（AWS / Google Cloud / Azure / Cloudflare）

## 📌 今週のハイライト
- **AIエージェント関連が全分野で目立つ**：AWSの Bedrock AgentCore（AIエージェントを動かす基盤）や Strands、Google の ADK（Agent Development Kit）など、エージェントの構築・評価・運用の話題が多い週でした。
- **AWSが突出して活発**：走査143件、いいね100超の記事もあり、他3分野より反応が大きい傾向です。
- **Google Cloud / Azure は反応が小さめ**：いいね・ストックとも1桁以下の記事が中心で、「ハマりどころ」系の実践記事が主です。
- **Cloudflare は実運用・セキュリティログの記事が注目**。定番にも文化祭のシステム構築事例が入っています。

## 🔥 今週これだけ読む3本
1. **2026年の情報漏洩を手口で分類してみた**（いいね120 / ストック94）— 今週最も反応が大きく、セキュリティ全般の整理に役立ちそうです。 https://qiita.com/yama3133/items/071119dfea9ed24d0948
2. **高校の文化祭でPOSシステムをCloudflare上に1から構築/運用した話**（いいね193 / ストック61）— 構築から本番障害まで書かれた実体験で、定番として保存されています。 https://qiita.com/ast-24/items/454fc975b095230565c7
3. **AI感のないAWS構成図をAIエージェントに描かせたい！**（いいね135 / ストック102）— 実務で使える構成図作成の工夫で、ストック数が最多です。 https://qiita.com/sagochiko/items/ef77b084ff2dee1f859c

## 📝 タグ別ホット記事（直近7日）
※数値は取得時点の値。クラウドと関連が薄い・内容が不明確な記事は各節で一部除外しています。

### AWS（走査143件から選定）
- **2026年の情報漏洩を手口で分類してみた**（いいね120 / ストック94 / 2026-10-06）— 情報漏洩の手口を分類した整理記事。個別の脆弱性の詳細・スコアは CISA／JPCERT 週報を参照。 https://qiita.com/yama3133/items/071119dfea9ed24d0948
- **判断特化型GraphRAGをJevを使って構築してみた（ベクトル未使用）**（45 / 30 / 10-09）— GraphRAG（知識をグラフ構造で検索に使うAI手法）の構築例。 https://qiita.com/kikuziro/items/6191b5ad83520d181f38
- **Strands Deciderハンズオン！**（29 / 8 / 10-07）— AIエージェントSDK「Strands」の機能を試すハンズオン。 https://qiita.com/har1101/items/cf5e734358e09f2410d0
- **【AWS】GitHub ActionsとAgentCore Evaluationsでエージェントの評価をCI/CDに組み込んでみた**（10 / 3 / 10-11）— エージェントの品質評価を自動化パイプラインに入れる話。 https://qiita.com/yakumo_09/items/6f3936d9f7255a4259d9
- **【AWS AI League】Bedrock AgentCore でAIエージェントを作ってハマった6つのこと**（6 / 6 / 10-08）— 開発時のつまずきどころの共有。 https://qiita.com/AyaKunisawa/items/4e1d87e075a3bae93f40

### Google Cloud（走査14件）
- **【AIエージェント×動画量産パイプライン】…Google Cloud（Veo / Vertex AI）でマルチメディア工場を建設してみる**（1 / 0 / 10-11）— 動画生成を自動化する構成例。 https://qiita.com/kuis/items/d696ddf067eddde79e7f
- **Cloud Build の履歴を CSV に出して、失敗したままのトリガーだけ再実行する**（1 / 0 / 10-07）— CI/CD運用の小技。 https://qiita.com/taquangku/items/b618bbc18deafefde4cb
- **Google Drive × Cloud Run で構築する、完全クラウド完結の自動 LaTeX/PDF コンパイル環境**（0 / 0 / 10-12）— サーバーレスでPDF生成する環境の構築。 https://qiita.com/takase_hiroyuki/items/1a830f5217f2676b6b6a
- **ADK エージェントのトレースを Cloud Trace に送る——無言で失敗する5つのハマりどころ**（0 / 0 / 10-12）— 可観測性（トレース収集）の落とし穴集。 https://qiita.com/toyama0919/items/61d4783a783c60cfbba4
- **任天堂のサーバー構成を読み比べる。Super Mario RunのApp EngineとNPLNのGKE**（0 / 0 / 10-10）— 公開情報にもとづく構成比較。 https://qiita.com/harupython/items/fdde314f62c38605e23a
- 除外：Bedrock中心の記事（AWS寄り）ほか2件。

### Microsoft Azure（走査16件）
- **Azure AI Search から SharePoint Online のドキュメントを取り込む Step by Step**（4 / 0 / 10-06）— 検索基盤への取り込み手順。 https://qiita.com/ryoma-nagata/items/75016e85e04fca3bafd5
- **IBM Bobと一緒に約75円でAzure BatchのPoCをやってみた**（1 / 0 / 10-09）— 低コストで試すバッチ処理の検証。 https://qiita.com/takumiida1/items/0bbc471bd9a937f80413
- **#14. Azure IoT EdgeのStore-and-Forwardは何時間耐えられる？**（1 / 0 / 10-07）— 通信断時の保持・再送の検証。 https://qiita.com/yyyyssssyyy/items/e5d5d6c16990f2046b9b
- **Azure版Cloud9（Azure ML × VS Code Web）を閉域化しようとして、結局マネージドVNetに落ち着いた話**（0 / 1 / 10-07）— 閉域（外部非公開）構成の試行錯誤。 https://qiita.com/J-N/items/f73dffc9ceda41731421
- **Amazon Bedrockが（ほぼ）個人利用できなくなったのでMicrosoft Foundryで最新の生成AIモデルを使う**（0 / 0 / 10-12）— 代替として Foundry を使う話。 https://qiita.com/takumiida1/items/6afb2b9bd13dbdd23628
- 除外：Azure色の薄い記事3件ほか。

### Cloudflare（走査18件）
- **Jev 互換の判断AI「Clef」と Haiku 5.5 に同じ分類を306問。Clef が自信を持った13%は95%当たった**（6 / 2 / 10-08、企業Org投稿）— 判断AIの精度比較。 https://qiita.com/suwa_nobu/items/1cc4989b0fdd47e4ea12
- **どのようなサイトが狙われているか？Cloudflareセキュリティログから見る攻撃の傾向と対策**（5 / 2 / 10-12）— ログから見る攻撃傾向の分析。 https://qiita.com/shioccii/items/cf18356730534053de95
- **VPSのフロントをCloudflare経由にするメリット**（1 / 1 / 10-08）— CDN／プロキシ経由にする利点の整理。 https://qiita.com/okokok/items/96f7c747588d7db51833
- **Cloudflare Clef-omni は音声と動画をどこまで判定できるか**（0 / 0 / 10-10）— 音声・動画判定の得意/不得意の検証。 https://qiita.com/Takuya__/items/09858e2f665ed5c07746
- **LoLのBan/Pick統計サイト「BPGG」をDBサーバーなしで作った話**（0 / 0 / 10-12）— SQLite焼き込み構成の事例。 https://qiita.com/tawasi12/items/43caba9203dba3405d0a
- 除外：クラウドとの関連が薄い記事3件ほか。

## 📚 定番（直近30日・ストック20以上）
### AWS
- AI感のないAWS構成図をAIエージェントに描かせたい！（ストック102）https://qiita.com/sagochiko/items/ef77b084ff2dee1f859c
- 2026年の情報漏洩を手口で分類してみた（ストック94）https://qiita.com/yama3133/items/071119dfea9ed24d0948
- 判断特化型GraphRAGをJevを使って構築してみた（ストック30）https://qiita.com/kikuziro/items/6191b5ad83520d181f38
### Google Cloud
- 該当なし
### Microsoft Azure
- 該当なし
### Cloudflare
- 高校の文化祭でPOSシステムをCloudflare上に1から構築/運用した話（ストック61）https://qiita.com/ast-24/items/454fc975b095230565c7
- Jev・Clef・d1・Jeff・Kev…意思決定モデル（System One）を仕組みから比較する【2026年10月版】（ストック24）https://qiita.com/nogataka/items/a2f89a94d243b1b715cb

## ℹ この記事の見方
- いいね数・ストック数（あとで読む用の保存数）は**取得時点の値**です。人気の目安であり、記事の正確性を保証するものではありません。
- 要約はタイトルと公開情報から読み取れる範囲での紹介です。記事本文の転載はしていません。
- 個人著者名は記載していません。脆弱性の話題は CISA／JPCERT 週報を参照してください。
- 取得できなかった情報源：なし（全タグ取得成功）。

## 出典
- Qiita API v2 `https://qiita.com/api/v2/items`（タグ検索：AWS / Google Cloud / Azure / Cloudflare）

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
