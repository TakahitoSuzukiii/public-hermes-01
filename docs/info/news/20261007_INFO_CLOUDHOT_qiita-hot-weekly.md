作成日: 2026-10-07 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-09-30〜2026-10-07

# Qiita クラウド人気記事 週報（AWS / Google Cloud / Azure / Cloudflare）

## 📌 今週のハイライト
- **AI エージェント×クラウド**の話題が引き続き多い。AWS では Strands・AgentCore・Bedrock Guardrails、Azure では Azure AI Search や「Agentic SOC」など。
- **セキュリティ**（情報漏洩の手口分類、API キー等の漏えい検知）が AWS タグで最も反応を集めた。
- Google Cloud は Gemini 関連の速報と、リリースノートの運用自動化が中心。ただし反応数は全体に小さめ。
- Cloudflare は「定番」側（文化祭 POS 構築記）が突出して人気。直近7日の新着は反応が少なめ。

## 🔥 今週これだけ読む3本
1. **高校の文化祭でPOSシステムをCloudflare上に1から構築/運用した話 〜短期開発から本番障害、そして完売まで〜**（いいね179 / ストック58）
   - 理由: 今回の対象タグ全体で最も反応が大きい。実運用で起きた障害まで書かれた体験談。
   - https://qiita.com/ast-24/items/454fc975b095230565c7
2. **AI感のないAWS構成図をAIエージェントに描かせたい！**（いいね126 / ストック94）
   - 理由: ストック数が最大級。構成図（アーキテクチャ図）作成を AI に任せる実践的な内容。
   - https://qiita.com/sagochiko/items/ef77b084ff2dee1f859c
3. **2026年の情報漏洩を手口で分類してみた**（いいね25 / ストック22）
   - 理由: 直近7日の新着（AWS タグ）で最上位。クラウド運用者にも関係するセキュリティ整理。
   - https://qiita.com/yama3133/items/071119dfea9ed24d0948

## 📝 タグ別ホット記事（直近7日）
※数値は取得時点（2026-10-07）の値。

### AWS（新着180件を走査／上位から選定。試験受験記・登壇報告など一部は除外）
- **2026年の情報漏洩を手口で分類してみた**（いいね25 / ストック22 / 2026-10-06）: 今年の情報漏洩事例を手口ごとに分類した整理記事。https://qiita.com/yama3133/items/071119dfea9ed24d0948
- **「シークレットスキャン」とは？漏れた API キー、誰が止めてくれるのか？…**（いいね13 / ストック16 / 2026-10-05）: シークレットスキャン（コード等に紛れた API キーを検知する仕組み）を業務システムや GitHub・GitLab で調べた内容。https://qiita.com/songchong/items/5ee39ef5b71510e36c2a
- **Amazon S3+vsftpdでFTPサーバを構築する**（いいね11 / ストック0 / 2026-10-06）: S3 をバックエンドにした FTP サーバ構築手順。https://qiita.com/naoaki-yzrh/items/d1f17a1dd4f050dbfd7f
- **Amazon Bedrock Guardrailsで個人情報を伏せたら、「みりん」が人名になった話（2026年版）**（いいね4 / ストック2 / 2026-10-02 / GMOコネクト）: Guardrails（生成 AI の入出力制御機能）の個人情報マスクで起きた誤検知の話。https://qiita.com/ntaka329/items/260b76e087ee593998d3
- **(新登場)Nova 2.5 Sonic爆誕：東京リージョンにもきている**（いいね4 / ストック0 / 2026-10-06）: 音声系モデル Nova 2.5 Sonic の登場と東京リージョン対応の紹介（タイトルからの読み取り）。https://qiita.com/yama3133/items/5ce2572730be29eb89fe

### Google Cloud（新着38件を走査／上位から選定。クラウドと関連の薄い記事等は除外）
- **【速報】Gemini 4 Argon 登場！公式データで見る“長時間働くAI”の現在地**（いいね6 / ストック3 / 2026-10-05）: Gemini の新モデル速報。公式データをもとに長時間タスク性能を整理（タイトルより）。https://qiita.com/tomokoro/items/69f8d2f1a3504927b6c7
- **Google Cloudのサポート終了を見逃さないように、Geminiでリリースノートを読んでSlackに通知する仕組みを作った**（いいね2 / ストック3 / 2026-09-30 / iret）: リリースノートを Gemini で要約し Slack に通知する運用自動化。https://qiita.com/y-miyake/items/27233fd9d151ecc90cc1
- **CodeMenderとMantis入門 AIで脆弱性を見つけて直す仕組みと違い**（いいね1 / ストック1 / 2026-10-01）: AI による脆弱性発見・修正の仕組み紹介。脆弱性の詳細・スコアは CISA／JPCERT 週報を参照。https://qiita.com/s_horikoshi/items/711b327de7b01d9f28ed
- **GCPでNext.jsアプリを動かす！最適なデプロイ戦略でやってよかった3つのこと**（いいね1 / ストック1 / 2026-10-01）: Next.js を GCP で動かす際のデプロイ上の工夫。https://qiita.com/fd_ai_teacher/items/358c503e9b069cf86f02
- **資格を取るか迷っている人へ。GCP全冠した僕の仕事とキャリアに起きた変化**（いいね1 / ストック1 / 2026-09-30）: GCP 資格を全て取得した体験談。https://qiita.com/ashahi00/items/16d77d07c1e35631b607

### Microsoft Azure（新着23件を走査／上位から選定。関連の薄い記事等は除外）
- **【生成AI活用】Visual Studio Subscription の $50 Azure クレジットで Windows Server + SQL Server 環境を構築する**（いいね3 / ストック2 / 2026-10-04）: 付帯クレジットで検証環境を作る手順。https://qiita.com/RYA234/items/1efcb99c150ea8a9e042
- **Azure AI Search から SharePoint Online のドキュメントを取り込む Step by Step**（いいね3 / ストック0 / 2026-10-06）: 検索サービスに SharePoint の文書を取り込む手順解説。https://qiita.com/ryoma-nagata/items/75016e85e04fca3bafd5
- **⚡Agentic SOC⚡ Microsoft Project Perception とは？…**（いいね1 / ストック1 / 2026-10-05 / Microsoft）: セキュリティ運用（SOC）向けエージェント構想の整理。https://qiita.com/aktsmm/items/c81ab3bd2235d3310aad
- **【Azure】Azure Firewall の SKU（Basic/Standard/Premium）はどれを選ぶ？要件から逆引きする選定メモ**（いいね2 / ストック0 / 2026-09-30 / パナソニック コネクト）: ファイアウォールの SKU（製品グレード）選びの目安。https://qiita.com/Ryutaro_Yamamoto_PCO/items/5d63bcab3553f6e00ed3
- **Azure Update 2026年9月まとめ**（いいね1 / ストック0 / 2026-10-05 / Microsoft）: 9月の Azure アップデート一覧。https://qiita.com/ManabuYamamoto/items/c5a77adf391eac1bf6e5

### Cloudflare（新着24件を走査／上位から選定。関連の薄い記事等は除外）
- **【入門】Cloudflareでできること・使われ方・AIとの相性をまとめてみた**（いいね1 / ストック1 / 2026-10-02）: Cloudflare の機能全体を俯瞰する入門記事。https://qiita.com/y-yoshizaki/items/9c7d0b28e7bec5692e6f
- **Astroの静的サイトに来るボットやAIクローラーを確認する**（いいね1 / ストック1 / 2026-10-01）: 静的サイトへのボット／AI クローラーのアクセス確認。https://qiita.com/webdecoy/items/fffab6988245e43217cb
- **Cloudflare Pages から Workers へ移したら管理画面だけ 404。…**（いいね1 / ストック1 / 2026-09-30）: Pages から Workers へ移行時の取りこぼしを配備前に防ぐ話。https://qiita.com/ishizakahiroshi/items/3744dd94411fc10c1dde
- **Cloudflare Access配下のNextcloud Officeで「ドキュメントの読み込みに失敗」を解消した話**（いいね1 / ストック0 / 2026-10-04）: Access（認証ゲート）配下での不具合の解消。https://qiita.com/Tatsuya0518/items/9d05497c0664373bca4f
- **Cloudflare WorkersのEmscripten対応が発表されたので試してみる**（いいね1 / ストック0 / 2026-10-02）: Workers 上で Emscripten（C/C++ を WebAssembly 化するツール）対応を試す記事。https://qiita.com/goosys/items/a85ba49f5795774c2aa7

## 📚 定番（直近30日・ストック20以上）
- **AWS**
  - AI感のないAWS構成図をAIエージェントに描かせたい！（ストック94）https://qiita.com/sagochiko/items/ef77b084ff2dee1f859c
  - 【AWS初心者向け】インフラ構成を図解で理解しよう！ALB・ECS・RDS・Lambda・NAT Gateway・VPCエンドポイントを一気に学ぶ（ストック49）https://qiita.com/Nao52/items/35441e4b0009aa128610
  - AWSのインフラ導入でAIを使っている箇所と手でやっている箇所（ストック32）https://qiita.com/infra365/items/aa30a54fc6f0849385a7
- **Google Cloud**: 該当なし
- **Microsoft Azure**: 該当なし
- **Cloudflare**
  - 高校の文化祭でPOSシステムをCloudflare上に1から構築/運用した話（ストック58）https://qiita.com/ast-24/items/454fc975b095230565c7

## ℹ この記事の見方
- いいね数・ストック数（あとで読むための保存数）は**取得時点（2026-10-07）の値**です。人気の目安であり、正確性・品質を保証するものではありません。
- 要約はタイトル等から読み取れる範囲で記載しています。詳細は各記事をご確認ください。
- 脆弱性に関する話題の詳細・スコアは CISA／JPCERT 週報を参照してください。
- 取得できなかった情報源: なし

## 出典
- Qiita API v2（items 取得、タグ AWS / Google Cloud / Microsoft Azure / Cloudflare）: https://qiita.com/api/v2/docs

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
