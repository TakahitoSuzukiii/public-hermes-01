作成日: 2026-11-03 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-10-27〜2026-11-03

# Qiita クラウド人気記事 週報（2026-11-03）

## 📌 今週のハイライト
- AWS は生成AI関連（Amazon Bedrock、AgentCore）の話題が目立ち、書評記事が最も反応を集めました。
- 一方でネットワーク・コスト系の実践記事（SSM Session Manager、RDS Data API、AWS費削減）も安定して読まれています。
- Google Cloud / Azure / Cloudflare は全体にいいね数が少なく、今週は小粒な実践記事が中心でした。
- Cloudflare は AI エージェント（Agents）や月次アップデート、セキュリティ対策の話題が見られます。
- 脆弱性関連の話題が定番枠に出ていますが、詳細・スコアは CISA／JPCERT 週報を参照してください。

## 🔥 今週これだけ読む3本
1. **【宇宙最速書評】AWSでRAGとAIエージェントをがっつり業務実践できる名著「Amazon Bedrock実践ガイド」**（いいね24／ストック11）
   理由: 今週のAWS最多反応。生成AI基盤（Bedrock：AWSの生成AIサービス）の学び方の入口になります。
   https://qiita.com/minorun365/items/84cd50fda97df62cff88
2. **SSM Session Managerを使ってDBに接続する**（いいね16／ストック11）
   理由: 踏み台サーバーを置かずに DB へ入る定番手法で、保存数も多く実用的です。
   https://qiita.com/j-yasukawa/items/701554f14fe8b02ff34e
3. **Microsoft Student Ambassadorsとは？ なり方を画面つきで解説！**（いいね8／ストック8）
   理由: Azure 分野で最も反応が高く、学生向けの手順が画面つきで分かりやすい内容です。
   https://qiita.com/shahin0809/items/2365fbcb09411bb3e51c

## 📝 タグ別ホット記事（直近7日）

### AWS（走査113件。うち上位を掲載。宣伝色の強い記事・無関係な記事は除外）
- **「Amazon Bedrock実践ガイド」書評** 24/11・2026-10-27 — RAG（検索で情報を補う生成AI手法）とAIエージェントの業務活用本の紹介。 https://qiita.com/minorun365/items/84cd50fda97df62cff88
- **SSM Session Managerを使ってDBに接続する** 16/11・2026-10-29 — 踏み台なしでDB接続する手順。 https://qiita.com/j-yasukawa/items/701554f14fe8b02ff34e
- **RDS Data APIを使ってNAT不要構成にしてみた** 8/3・2026-10-29 — NAT Gateway（外部通信用の中継）なしでDBを操作する構成の紹介。 https://qiita.com/j-yasukawa/items/bd3785861c0e0bfc2f7e
- **AgentCore GatewayのターゲットにStep Functionsを指定できるようになりました** 6/0・2026-10-30 — AIエージェント基盤の新機能解説。 https://qiita.com/har1101/items/de6104e8057452ebd720
- **Lambdaをデュアル構成（VPC内外）にして学んだこと** 5/0・2026-10-30 — Lambda（サーバーレス実行環境）をVPC内外で分ける構成の知見。 https://qiita.com/shusaku009/items/f63bb5af714800ddbbc0

### Google Cloud（走査18件。除外：複数分野共通の製品アップデート記事など）
- **「現在気温BOT」のしくみとこだわり** 2/0・2026-10-31 — 気温に応じて動くBOTの仕組み解説。 https://qiita.com/UmiKazeYu/items/33b65f26620601120e70
- **HULFT SquareからGoogle Chatに通知する（Google Chat API）** 2/0・2026-10-28 — 処理完了を Chat に通知する方法。 https://qiita.com/sync_shu/items/752cf0fd34b1e981a386
- **【HTML/Canvas × Cloud Run】棒人間をWebアプリで再現** 0/1・2026-10-27 — Cloud Run（コンテナ実行基盤）で動かす遊び心ある作例。 https://qiita.com/toshyss/items/595668e2ed900691b353
- **GCPのデータ取り込み系サービスを超ざっくり説明する試み** 0/0・2026-11-02 — 取り込み系サービスの概観。 https://qiita.com/kmmk689/items/362b0a026a2fda3810a4
- **GCPのデータ保存系サービスを超ざっくり説明する試み** 0/0・2026-11-01 — 保存系サービスの概観。 https://qiita.com/kmmk689/items/f80248408aabfa45a8c7

### Microsoft Azure（走査19件）
- **Microsoft Student Ambassadorsとは？** 8/8・2026-11-02 — 学生アンバサダー制度の概要となり方。 https://qiita.com/shahin0809/items/2365fbcb09411bb3e51c
- **GitHub Copilot SDK の追悼式場を Azure で作ってみた** 5/6・2026-10-29 — 多数の同時アクセスでも数が欠けない構成の工夫。 https://qiita.com/shahin0809/items/d337af6f1b64a9c6ae53
- **Azure Storageアカウントの冗長化、結局どれ？** 1/0・2026-10-30 — 6つのプランを障害レベルから逆引き。 https://qiita.com/Ryutaro_Yamamoto_PCO/items/754944f02df913c51016
- **Azure HPC入門：CycleCloud + Slurm + NetApp Files** 1/0・2026-10-29 — HPC（高性能計算）クラスタ構築入門。 https://qiita.com/ManabuYamamoto/items/e70094409085d1c3b815
- **Azure Monitorで勤怠管理を試す（KQL変換でコスト99%削減?）** 0/1・2026-10-28 — ログ基盤の意外な活用例。 https://qiita.com/ManabuYamamoto/items/47db0fb06573c9940eeb

### Cloudflare（走査17件）
- **EmDash on CloudflareでWebサイトを公開しClaudeから更新** 2/1・2026-10-31 — AIでサイトを更新する試み。 https://qiita.com/tamaoki_t/items/d68f0cf4883100546e7b
- **robots.txt の User-agent: * は名前を書いたbotに効かない** 1/0・2026-11-02 — 書き忘れ検出スクリプト付きの注意喚起。 https://qiita.com/Aulvem/items/07d6810a77624418a7c9
- **ベルギーから.envを掘りに来た2,000件のアクセスをCloudflareで撃退** 0/0・2026-11-02 — 不審アクセス対策の体験談。 https://qiita.com/snack_info/items/e796fa83ba9122142b56
- **Cloudflare One 月次アップデート：2026年10月** 0/0・2026-11-02 — Gateway／Accessを中心とした更新まとめ。 https://qiita.com/shofuk9/items/0eb3857da6e69e98cb48
- **Cloudflare AgentsがPi 1.4に対応、中断・復旧・永続化を検証** 0/0・2026-11-01 — エージェントの耐障害性検証。 https://qiita.com/tanahiro2010/items/9b9db576e2a89b839797

## 📚 定番（直近30日・ストック20以上）
- AWS（タグ付きでクラウド関連性が高いものを抜粋）
  - AWS初心者がエンジニアを辞めた話（ストック41） https://qiita.com/tks_1128/items/e4cde327a910b5beba11
  - 【AWS】AWS Lambda Web Functionsから考えるAWS Lambdaとは何なのか（ストック20） https://qiita.com/ymd65536/items/3bc00ba77b87808bda9b
  - ※情報漏洩・PHP脆弱性・CVE関連の記事も上位にありますが、詳細・スコアは CISA／JPCERT 週報を参照してください。
- Google Cloud: 該当なし
- Microsoft Azure: 該当なし
- Cloudflare
  - どのようなサイトが狙われているか？Cloudflareセキュリティログから見る攻撃の傾向と対策（ストック36） https://qiita.com/shioccii/items/cf18356730534053de95

## ℹ この記事の見方
- いいね数・ストック数（保存数）は**取得時点（2026-11-03）の値**です。人気の目安であり、正確性を保証しません。
- 「ホット」は直近7日の新着をいいね+ストック順、「定番」は直近30日でストック20以上の記事です。
- 要約はタイトルと公開情報から読み取れる範囲で書いており、本文全体は確認していません。
- 取得できなかった情報源: なし

## 出典
- Qiita 公式 API / タグ別フィード（https://qiita.com/api/v2/items 、https://qiita.com/tags/<タグ名>/feed）

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
