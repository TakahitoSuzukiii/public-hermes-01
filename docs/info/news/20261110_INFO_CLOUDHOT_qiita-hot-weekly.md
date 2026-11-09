作成日: 2026-11-10 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-03〜2026-11-10

# Qiita クラウド人気記事 週報（2026-11-10号）

## 📌 今週のハイライト
- AWS が引き続き話題の中心。AI 駆動開発や Amazon Bedrock（AWS の生成 AI 基盤サービス）、Textract（文書から文字を読み取るサービス）の日本語 OCR（光学文字認識）が目立ちました。
- AI エージェントの「権限管理」「ガバナンス」を扱う記事が Azure 節で複数あり、Entra ID（Azure の認証基盤）との組み合わせが関心を集めています。
- Google Cloud は IAM（権限管理）や用語整理の入門系が中心で、反応数は全体に控えめです。
- Cloudflare は Workers / Pages / D1 での個人開発・小規模構成の事例が中心でした。
- 脆弱性関連の記事も定番に並んでいますが、詳細・スコアは CISA／JPCERT 週報を参照してください。

## 🔥 今週これだけ読む3本
1. **AI駆動開発の次の段階: ソフトウェアファクトリー**（いいね81 / ストック55）
   選定理由: 今週のクラウド全体で突出した反応数。AI を使った開発の進め方を扱っています。
   https://qiita.com/Syoitu/items/9364a0a175893bb15219
2. **[AWS]日本語OCRがついにきちゃー！ ~Textractにいろいろ読ませてみた~**（いいね21 / ストック11）
   選定理由: 日本語対応という実用的な新機能を実際に試した検証記事。
   https://qiita.com/kikuziro/items/9aff0fefe89cfa13192e
3. **東京リージョンで使っていてもバージニア北部に依存しているもの**（いいね14 / ストック14）
   選定理由: 東京リージョン利用時に見落としやすい依存先を整理しており、設計・障害対策の参考になるため。
   https://qiita.com/yama3133/items/5416c243e14a5406dd6f

## 📝 タグ別ホット記事（直近7日）
（各数値は取得時点の値。各節は「いいね / ストック / 公開日」の順）

### AWS（走査118件・新着から選定。除外1件：宣伝色が強い記事）
- **AI駆動開発の次の段階: ソフトウェアファクトリー**（81 / 55 / 11-04）AI 活用で開発を工場のように回す考え方の紹介。https://qiita.com/Syoitu/items/9364a0a175893bb15219
- **[AWS]日本語OCRがついにきちゃー！ ~Textractにいろいろ読ませてみた~**（21 / 11 / 11-03）Textract で日本語文書を読ませた検証。https://qiita.com/kikuziro/items/9aff0fefe89cfa13192e
- **東京リージョンで使っていてもバージニア北部に依存しているもの**（14 / 14 / 11-06）東京リージョンでも米国東部側に依存する機能の整理。https://qiita.com/yama3133/items/5416c243e14a5406dd6f
- **集中力散漫＆過集中持ちエンジニアがAWS DEAを突破した「過集中スイッチ」の入れ方**（13 / 2 / 11-04）AWS 認定資格 DEA（Data Engineer Associate）の勉強法体験談。https://qiita.com/kohYoung_I/items/cce40cb5b9cdfc1f8787
- **【AWS】結果を返すか、答えを返すか。Web SearchとWeb Answerの使い分け【AgentCore】**（11 / 2 / 11-08）AgentCore（AI エージェント実行基盤）の検索機能の使い分け。https://qiita.com/Nana_777/items/6e466fb974972a79a323

### Google Cloud（走査25件。除外3件：宣伝色・無関係）
- **Cloud Runで403が出たら、誰の権限を確認する？ 3つの立場で学ぶGoogle Cloud IAM**（2 / 0 / 11-09）Cloud Run の 403 エラーを IAM の観点で整理。https://qiita.com/ditchcrimson/items/4d1e7acb4c7a9178d33a
- **ファイルの置き場所を変えたらOAuthのクライアントIDが無効に？自動化スクリプトが停止した原因と教訓**（1 / 0 / 11-06）OAuth 認証設定のトラブル事例。https://qiita.com/kazukichi_0914/items/aa6a90949c5366dba10c
- **Google Cloud SQLとBigQueryの違いがわからなかったので…整理した**（0 / 0 / 11-09）行指向・列指向、OLTP/OLAP から違いを整理。https://qiita.com/Pippichannnn/items/15076f94489041887b36
- **GCPの運用系サービスを超ざっくり説明する試み**（0 / 0 / 11-09）運用系サービスの概観。https://qiita.com/kmmk689/items/0c2ce1467bb47246a878
- **GCPのセキュリティ系サービスを超ざっくり説明する試み**（0 / 0 / 11-09）セキュリティ系サービスの概観。https://qiita.com/kmmk689/items/53c99c176ed7240d43e8

### Microsoft Azure（走査17件。除外3件：宣伝色・無関係）
- **AIガバナンスを後回しにすると起きやすいこと、現場の視点から整理する**（2 / 1 / 11-03）AI 統制を後回しにした場合のリスク整理。https://qiita.com/Sidejob/items/cbfdb20e996e0da91dfd
- **Azure AI Search：所有者ではないユーザーがインポート ウィザードを使うための権限設定手順**（1 / 1 / 11-06）マネージド ID だけでは足りない権限設定の手順。https://qiita.com/lks0426aa/items/dc57fa0e4a5fada6e86f
- **RBACだけでは足りない。AIエージェントの権限は「委任」と「自律」で考える ～ Entra ID で OBO を検証**（1 / 0 / 11-09）OBO（On-Behalf-Of：ユーザーの代理で動く認証方式）の検証。https://qiita.com/shou-wordwright555501/items/00c5972f3819f87715bb
- **会社携帯が支給されない会社でMFAをどう導入するか考えてみた**（0 / 2 / 11-03）MFA（多要素認証）の導入方法の検討。https://qiita.com/naunari/items/125a50cb833aceceb87c
- **【FaaS比較シリーズ #2】主要CSPのFaaSを横並びで比較する**（0 / 1 / 11-08）Lambda を軸に各社 FaaS（関数実行サービス）を比較。https://qiita.com/Doc-Tanukichi/items/2dc7e20484dd93bc682a

### Cloudflare（走査22件。除外3件：クラウドと関連が薄い記事）
- **入力を外部に送らないブラウザツール集を、Next.js の static export と Cloudflare Workers で作った**（1 / 1 / 11-09）https://qiita.com/hasegawa--2025/items/de5cbceeae78ed776a43
- **Cloudflare Pages Functions と D1 で、サーバーを持たずに先行登録フォームを作る**（1 / 1 / 11-08）重複・連投・ボット対策つきの構成例。https://qiita.com/YATTARU/items/9d1038d353186409e672
- **初めてのCI/CD。pushしただけで公開まで流れる理由を、図で理解した**（1 / 1 / 11-03）GitHub Actions + Workers の入門。https://qiita.com/tobaru/items/70aebab60529d72cb4b5
- **Cloudflare Workers で公開した静的サイトが Search Console で「HTTPS 以外の URL」と言われた件と対処**（0 / 1 / 11-09）https://qiita.com/toshinsai/items/664cf59da512ac8bd7be
- **【FaaS比較シリーズ #2】主要CSPのFaaSを横並びで比較する**（0 / 1 / 11-08）（Azure 節と同一記事）https://qiita.com/Doc-Tanukichi/items/2dc7e20484dd93bc682a

## 📚 定番（直近30日・ストック20以上）
### AWS
- **AWS初心者がエンジニアを辞めた話**（ストック45）https://qiita.com/tks_1128/items/e4cde327a910b5beba11
- **実際に試したClaude便利術20選 まとめ**（ストック62）https://qiita.com/N-Kyo/items/bf4a3a2185db2d28eee5
- **【AWS】AWS Lambda Web Functionsから考えるAWS Lambdaとは何なのか**（ストック20）https://qiita.com/ymd65536/items/3bc00ba77b87808bda9b
- ※ 脆弱性関連の定番記事2件は本記事では紹介せず、詳細・スコアは CISA／JPCERT 週報を参照してください。
### Google Cloud
- 該当なし
### Microsoft Azure
- 該当なし
### Cloudflare
- **どのようなサイトが狙われているか？Cloudflareセキュリティログから見る攻撃の傾向と対策**（ストック38）https://qiita.com/shioccii/items/cf18356730534053de95

## ℹ この記事の見方
- 「いいね」「ストック（後で読むための保存）」は**取得時点（2026-11-10）の値**です。公開直後の記事は数値が低く出ます。
- 人気の目安であり、記事内容の正確性を保証するものではありません。
- ホット＝直近7日の新着をいいね+ストック順、定番＝直近30日でストック20以上の記事です。
- 取得できなかった情報源: なし（4タグとも取得成功）

## 出典
- Qiita API v2 items（タグ別検索）: https://qiita.com/api/v2/docs

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
