作成日: 2026-10-29 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-10-29 週）

GitHub公式REST Search APIで集めた人気リポジトリ（スター10,000以上、母集団442件）を、前週（2026-10-22）と比べた差分レポートです。
「risers」は前週よりスターが増えたリポジトリ、「newcomers」は今週新しく集計対象に入ったリポジトリです。

> 用語: **スター** = GitHubで「気に入った」を示す印。人気の目安。**エージェント** = AIが自律的に作業を進める仕組み。**スキル** = AIエージェントに追加する手順書・拡張。**ハーネス** = AIエージェントを動かすための土台・実行環境。

## 今週の全体傾向

- **AIコーディングエージェント周辺**（スキル集、ハーネス、ゲートウェイ）が引き続き主役です。
- **morluto/rea** は今週も+42,409と大きく伸び、スター40万を突破しました。
- 母集団が356件から442件に拡大し、**定番の大型OSS**（ripgrep、prettier、coolify、mastodon など）が新規として多数加わりました。これは「急に人気になった」のではなく、集計対象に入ったためです。

## 🔺 前週比で伸びたリポジトリ（risers）

| 順位 | リポジトリ | スター | 前週比 | 主要言語 |
|---|---|---|---|---|
| 1 | morluto/rea | 406,459 | +42,409 | TypeScript |
| 2 | cloudflare/security-audit-skill | 52,508 | +13,831 | JavaScript |
| 3 | debpalash/VoiceStudio | 93,952 | +12,537 | Python |
| 4 | pbakaus/impeccable | 94,747 | +9,921 | Rust |
| 5 | deepseek-ai/deepseek-harness | 265,641 | +7,655 | TypeScript |
| 6 | stablyai/orca | 109,909 | +7,425 | TypeScript |
| 7 | HKUDS/DeepTutor | 49,503 | +7,352 | Python |
| 8 | DietrichGebert/ponytail | 179,876 | +6,926 | JavaScript |
| 9 | affaan-m/ECC | 292,440 | +6,190 | JavaScript |
| 10 | Graphify-Labs/graphify | 138,422 | +5,832 | Python |
| 11 | mattpocock/skills | 306,364 | +5,703 | Shell |
| 12 | heygen-com/hyperframes | 75,294 | +5,493 | TypeScript |
| 13 | TauricResearch/TradingAgents | 118,203 | +5,381 | Python |
| 14 | Panniantong/Agent-Reach | 106,129 | +5,205 | Python |

### 注目リポジトリ詳細

#### morluto/rea（+42,409 ⭐ 今週も最大の伸び）
- **概要:** AIエージェントを使い、アプリの挙動からネイティブバイナリ（実行ファイル）まで「何でもリバースエンジニアリング」するツール。
- **注目理由:** 先週の約+10万に続き、2週連続の突出した伸び。優先トピック `typescript` `claude` に該当。
- **主な特徴:** エージェント駆動の解析 / TypeScript製。
- **スター数:** 406,459 / **言語:** TypeScript
- リンク: https://github.com/morluto/rea

#### cloudflare/security-audit-skill（+13,831）
- **概要:** コーディングエージェント向けの多段階セキュリティ監査スキル。結果は独立した検証を経て出力される設計。
- **注目理由:** 先週の新規から連続して2位に浮上。大手企業発のセキュリティ系スキルとして関心が高い。
- **スター数:** 52,508 / **言語:** JavaScript
- リンク: https://github.com/cloudflare/security-audit-skill

#### debpalash/VoiceStudio（+12,537）
- **概要:** ElevenLabs（有料の音声合成サービス）の代替を目指す、完全ローカル動作のOSS。音声クローン、音声デザイン、動画吹き替えなど。
- **注目理由:** 2週連続で上位。ローカル・無料志向の流れに合致。優先トピック `python`。
- **スター数:** 93,952 / **言語:** Python
- リンク: https://github.com/debpalash/VoiceStudio

#### pbakaus/impeccable（+9,921）
- **概要:** コーディングエージェントに「デザインの語彙」を与え、見た目の磨き込みやレビューを指示しやすくするツール。
- **注目理由:** 優先トピック `rust` に該当。
- **スター数:** 94,747 / **言語:** Rust
- リンク: https://github.com/pbakaus/impeccable

#### stablyai/orca（+7,425）
- **概要:** 複数のコーディングエージェント（Claude Code等）を「艦隊」のようにまとめて動かす作業場。
- **注目理由:** 優先トピック `hermes-agent` `claude` `openclaw` `typescript` に該当。Hermes関連で今週最も目立つ。
- **スター数:** 109,909 / **言語:** TypeScript
- リンク: https://github.com/stablyai/orca

#### HKUDS/DeepTutor（+7,352）
- **概要:** 生涯にわたる個別最適化学習（パーソナライズ家庭教師）をAIで実現するプロジェクト。
- **注目理由:** 優先トピック `python`。
- **スター数:** 49,503 / **言語:** Python
- リンク: https://github.com/HKUDS/DeepTutor

#### その他の伸びたリポジトリ
- **deepseek-ai/deepseek-harness**（265,641 / TypeScript）: 「すべてがプラグイン」のエージェントハーネス。 https://github.com/deepseek-ai/deepseek-harness
- **DietrichGebert/ponytail**（179,876 / JavaScript）: AIに「一番怠け者の熟練開発者」のように考えさせるスキル（書かないコードが最良）。 https://github.com/DietrichGebert/ponytail
- **affaan-m/ECC**（292,440 / JavaScript）: エージェントの性能最適化システム（スキル・記憶・セキュリティ等）。 https://github.com/affaan-m/ECC
- **Graphify-Labs/graphify**（138,422 / Python）: コードや文書、SQLスキーマ等をクエリ可能な知識グラフに変換。 https://github.com/Graphify-Labs/graphify
- **mattpocock/skills**（306,364 / Shell）: 実務エンジニア向けのエージェント用スキル集。 https://github.com/mattpocock/skills
- **heygen-com/hyperframes**（75,294 / TypeScript）: HTMLを書いて動画をレンダリング。エージェント向け。 https://github.com/heygen-com/hyperframes
- **TauricResearch/TradingAgents**（118,203 / Python）: 複数のLLMエージェントによる金融取引フレームワーク。 https://github.com/TauricResearch/TradingAgents
- **Panniantong/Agent-Reach**（106,129 / Python）: AIエージェントにインターネット上の情報（SNS、動画等）を読ませる仕組み。 https://github.com/Panniantong/Agent-Reach

## 🆕 今週の新規ランクイン（newcomers）

今週は30件が新規でした。多くは定番OSSの集計対象入りです。開発者向けの主なものを紹介します。

| リポジトリ | スター | 言語 | 概要 |
|---|---|---|---|
| nektos/act | 72,478 | Go | GitHub Actionsをローカルで実行 |
| BurntSushi/ripgrep | 69,561 | Rust | .gitignoreを尊重する高速な正規表現検索ツール |
| coollabsio/coolify | 65,251 | PHP | Vercel/Heroku代替のセルフホストPaaS |
| sansan0/TrendRadar | 63,289 | Python | AI駆動の話題・トレンド監視ツール |
| makeplane/plane | 61,667 | TypeScript | Jira/Linear代替のOSSプロジェクト管理 |
| appwrite/appwrite | 57,790 | TypeScript | 認証・DB・ストレージ等を備えたOSSバックエンド基盤 |
| dockur/windows | 53,757 | Shell | Dockerコンテナ内でWindowsを動かす |
| ionic-team/ionic-framework | 52,727 | TypeScript | クロスプラットフォームUIツールキット |
| prettier/prettier | 52,386 | JavaScript | 意見を持つコード整形ツール |
| moeru-ai/airi | 50,882 | TypeScript | セルフホスト型のAIコンパニオン |
| mastodon/mastodon | 50,457 | Ruby | 分散型マイクロブログ |
| gogs/gogs | 47,909 | Go | 手軽に立てられるセルフホストGitサービス |
| zhayujie/CowAgent | 47,668 | Python | 個人用AIアシスタント／エージェントハーネス |
| paperless-ngx/paperless-ngx | 47,297 | Python | 書類のスキャン・索引・保管管理システム |
| fastapi/full-stack-fastapi-template | 46,110 | TypeScript | FastAPI+React等のフルスタックテンプレート |
| AstrBotDevs/AstrBot | 44,735 | Python | 多数のチャットツール・LLMをつなぐAIエージェント基盤 |
| Nutlope/hallmark | 41,759 | CSS | 「AIっぽいデザイン」を避けるClaude Code等向けスキル |
| ToolJet/ToolJet | 41,142 | HTML | 社内アプリ生成のOSSプラットフォーム |
| outline/outline | 41,105 | TypeScript | リアルタイム共同編集できるナレッジベース |
| papers-we-love/papers-we-love | 111,023 | Shell | コンピュータサイエンス論文の読書会資料 |
| CyC2018/CS-Notes | 186,375 | Python(表示) | 技術面接向けCS基礎知識まとめ（中国語） |
| DataTalksClub/data-engineering-zoomcamp | 46,518 | Jupyter Notebook | 無料9週間のデータエンジニアリング講座 |

※ 注意: 新規には、教材PDF配布、ハッキング関連のリンク集なども含まれていましたが、「開発者向け」の掲載基準および安全上の観点から割愛しました。また「Ebony-Vinyl/dsh-our-free-model」は無料モデル利用をうたうプラグインですが、提供元の信頼性が確認できていないため、先週に続き割愛しています。

## ⭐ 優先トピック注目枠（スター1万未満）

今週のデータでは、優先トピックに該当する1万未満のリポジトリは取得結果に含まれませんでした（優先トピック該当は全て1万以上）。

## 優先トピックの動き（まとめ）

- **claude / typescript:** rea、orca、ponytail、hyperframes、hallmark など上位の大半。エージェント系が主役。
- **hermes-agent:** 伸びた該当は stablyai/orca（109,909、+7,425）。NousResearch/hermes-agent 自体は258,421スターで集計中。cc-switch（150,037 / Rust）も `hermes-agent` トピックを持つ。
- **python:** VoiceStudio、DeepTutor、graphify、TradingAgents、Agent-Reach と多数。
- **rust:** impeccable（+9,921）、ripgrep（新規）、photocraft（74,721）。
- **go:** nektos/act、gogs が新規で登場（定番ツールの集計入り）。
- **nextjs:** coolify、appwrite が関連トピックで新規登場。
- **docker / angular / openclaw / nix:** docker関連（coolify、dockur/windows 等）が新規に多数。nix は目立った動きなし。

## 集計メモ

- データ元: GitHub公式REST Search API / 集計日 2026-10-29 / 前回 2026-10-22
- 掲載基準: スター10,000以上・開発者向け。優先トピックのみ1万未満も別枠。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
