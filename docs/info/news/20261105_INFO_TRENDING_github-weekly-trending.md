作成日: 2026-11-05 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-11-05 週）

GitHub公式REST Search APIで集めた人気リポジトリ（スター10,000以上、母集団443件）を、前週（2026-10-29）と比べた差分レポートです。
「risers」は前週よりスターが増えたリポジトリ、「newcomers」は今週新しく集計対象に入ったリポジトリです。

> 用語: **スター** = GitHubで「気に入った」を示す印。人気の目安。**エージェント** = AIが自律的に作業を進める仕組み。**スキル** = AIエージェントに追加する手順書・拡張。**ハーネス** = AIエージェントを動かすための土台・実行環境。**OSS** = ソースコードが公開されたソフトウェア。

## 今週の全体傾向

- **AIコーディングエージェント周辺**（スキル集、ハーネス、メモリ、デザイン補助）が引き続き主役です。
- **morluto/rea** は今週も +26,996 で首位。3週連続で最大の伸びですが、伸び幅は先週（+42,409）から縮小しました。
- 新規ランクインは17件。多くは「急に人気になった」ではなく、集計対象に入った定番OSS（flask、laravel、youtube-dl など）です。
- ハーネス系では **deepseek-harness** と、その無料モデル利用プラグイン系が上位に並びました。

## 🔺 前週比で伸びたリポジトリ（risers・掲載14件）

| 順位 | リポジトリ | スター | 前週比 | 主要言語 |
|---|---|---|---|---|
| 1 | morluto/rea | 433,455 | +26,996 | TypeScript |
| 2 | thedotmack/claude-mem | 113,382 | +8,960 | TypeScript |
| 3 | pbakaus/impeccable | 103,608 | +8,861 | Rust |
| 4 | mattpocock/skills | 314,630 | +8,266 | Shell |
| 5 | cloudflare/security-audit-skill | 60,772 | +8,264 | JavaScript |
| 6 | deepseek-ai/deepseek-harness | 273,606 | +7,965 | TypeScript |
| 7 | debpalash/VoiceStudio | 101,650 | +7,698 | Python |
| 8 | Gathin23/cleanyourtv | 52,460 | +7,448 | Python |
| 9 | D4Vinci/Scrapling | 97,622 | +7,326 | Python |
| 10 | Nutlope/hallmark | 48,532 | +6,773 | CSS |
| 11 | stablyai/orca | 116,383 | +6,474 | TypeScript |
| 12 | HKUDS/DeepTutor | 55,330 | +5,827 | Python |
| 13 | ifixai-ai/iFixAi | 43,496 | +5,796 | Python |
| 14 | affaan-m/ECC | 297,676 | +5,236 | JavaScript |

（元データ15件のうち1件は後述の注意書きの理由で割愛）

### 注目リポジトリ詳細

#### morluto/rea（+26,996 ⭐ 3週連続の最大の伸び）
- **概要:** AIエージェントを使い、アプリの挙動からネイティブバイナリ（実行ファイル）まで「何でもリバースエンジニアリング（仕組みの解析）」するツール。
- **注目理由:** スター43万を突破。伸びは鈍化しつつも突出。優先トピック `rust` `typescript` `python` `claude` に該当。
- **主な特徴:** エージェント駆動の解析 / TypeScript製。
- **スター数:** 433,455 / **言語:** TypeScript
- リンク: https://github.com/morluto/rea

#### thedotmack/claude-mem（+8,960）
- **概要:** エージェントの作業内容を記録し、セッションをまたいで文脈（コンテキスト）を引き継ぐ「永続メモリ」。
- **注目理由:** 今週新たに上位入り。「AIに記憶を持たせる」ニーズの高まりを反映。優先トピック `typescript` `claude` `openclaw`。
- **スター数:** 113,382 / **言語:** TypeScript
- リンク: https://github.com/thedotmack/claude-mem

#### pbakaus/impeccable（+8,861）
- **概要:** コーディングエージェントに「デザインの語彙」を与え、見た目の磨き込みやレビューを指示しやすくするツール。
- **注目理由:** 2週連続の上位。優先トピック `rust`。
- **スター数:** 103,608 / **言語:** Rust
- リンク: https://github.com/pbakaus/impeccable

#### cloudflare/security-audit-skill（+8,264）
- **概要:** コーディングエージェント向けの多段階セキュリティ監査スキル。結果は独立した検証を経て出力される設計。
- **注目理由:** 大手企業発のセキュリティ系スキルとして3週連続で上位。
- **スター数:** 60,772 / **言語:** JavaScript
- リンク: https://github.com/cloudflare/security-audit-skill

#### deepseek-ai/deepseek-harness（+7,965）
- **概要:** 「すべてがプラグイン」をうたうエージェントハーネス。
- **注目理由:** スター27万超。他ツール（cc-switch 等）も対応を打ち出し、周辺エコシステムが拡大中。優先トピック `typescript`。
- **スター数:** 273,606 / **言語:** TypeScript
- リンク: https://github.com/deepseek-ai/deepseek-harness

#### Gathin23/cleanyourtv（+7,448）
- **概要:** Wi-Fi経由でAndroid/Google TVの不要アプリを整理し、すっきりしたホーム画面に変えるツール。
- **注目理由:** 今週新たに上位入り。生活に近い実用ツール。優先トピック `python` `claude`。
- **スター数:** 52,460 / **言語:** Python
- リンク: https://github.com/Gathin23/cleanyourtv

#### D4Vinci/Scrapling（+7,326）
- **概要:** 単発のリクエストから大規模クロール（Webの巡回収集）までを扱うWebスクレイピング（情報収集）フレームワーク。
- **注目理由:** AI向けスクレイピングの需要を背景に伸長。優先トピック `python`。
- **スター数:** 97,622 / **言語:** Python
- リンク: https://github.com/D4Vinci/Scrapling

#### stablyai/orca（+6,474）
- **概要:** 複数のコーディングエージェント（Claude Code等）を「艦隊」のようにまとめて動かす作業場。
- **注目理由:** 優先トピック `hermes-agent` `claude` `openclaw` `typescript` に該当。Hermes関連で目立つ存在。
- **スター数:** 116,383 / **言語:** TypeScript
- リンク: https://github.com/stablyai/orca

#### その他の伸びたリポジトリ
- **mattpocock/skills**（314,630 / Shell）: 実務エンジニア向けのエージェント用スキル集。 https://github.com/mattpocock/skills
- **debpalash/VoiceStudio**（101,650 / Python）: ElevenLabs代替を目指す完全ローカルの音声クローン・吹き替えOSS。 https://github.com/debpalash/VoiceStudio
- **Nutlope/hallmark**（48,532 / CSS）: 「AIっぽいデザイン」を避けるClaude Code等向けスキル。 https://github.com/Nutlope/hallmark
- **HKUDS/DeepTutor**（55,330 / Python）: AIによるパーソナライズ家庭教師。 https://github.com/HKUDS/DeepTutor
- **ifixai-ai/iFixAi**（43,496 / Python）: AIエージェントを第三者目線で監査・評価するツール。 https://github.com/ifixai-ai/iFixAi
- **affaan-m/ECC**（297,676 / JavaScript）: エージェントの性能最適化システム（スキル・記憶・セキュリティ等）。 https://github.com/affaan-m/ECC

## 🆕 今週の新規ランクイン（newcomers・17件中、開発者向けを掲載）

| リポジトリ | スター | 言語 | 概要 |
|---|---|---|---|
| getify/You-Dont-Know-JS | 184,847 | （なし） | JavaScript言語を深く学べる書籍シリーズ |
| github/gitignore | 176,167 | （なし） | .gitignoreのテンプレート集 |
| ytdl-org/youtube-dl | 141,460 | Python | 動画サイトからの動画取得コマンドラインツール |
| rasbt/LLMs-from-scratch | 107,862 | Jupyter Notebook | PyTorchでChatGPT風LLMをゼロから実装して学ぶ |
| laravel/laravel | 85,231 | Blade | PHPのWebアプリフレームワーク |
| realworld-apps/realworld | 84,366 | TypeScript | 各種技術で作るMedium.comクローンのデモアプリ集 |
| pallets/flask | 74,962 | Python | Python製の軽量Webフレームワーク |
| wagoodman/dive | 54,699 | Go | Dockerイメージの各層を調べるツール |
| pingdotgg/t3code | 47,758 | TypeScript | （説明なし）TypeScript製プロジェクト |
| Donchitos/Claude-Code-Game-Studios | 35,691 | Shell | Claude Codeをゲーム開発スタジオ化（49エージェント・72スキル） |
| vercel/chatbot | 21,032 | TypeScript | Vercel製のNext.js製AIチャットボット |
| MemoriLabs/Memori | 17,420 | Python | エージェント向けの記憶基盤 |

※ 注意: `swisskyrepo/PayloadsAllTheThings`（攻撃手法ペイロード集）は、掲載基準（開発者向け）および安全上の観点から割愛しました。また、前週までと同様に「Ebony-Vinyl/dsh-our-free-model」（今週 +11,448 と伸びていますが、無制限の無料モデル利用をうたうプラグインで、提供元の信頼性が確認できていないもの）は割愛しています。

## ⭐ 優先トピック注目枠（スター1万未満）

- **Orkas-AI/Orkas**（9,035 / JavaScript）: ローカル優先のOSS（MIT）AIチーム。指揮役が複数エージェントを束ねて作業。`claude` `openclaw`。 https://github.com/Orkas-AI/Orkas
- **leerob/next-mdx-blog**（7,581 / TypeScript）: Next.js + MDX + Tailwind CSSのブログテンプレート。`typescript` `nextjs`。 https://github.com/leerob/next-mdx-blog
- **ThinkInAIXYZ/deepchat**（6,384 / TypeScript）: 強力なAIを個人の環境につなぐスマートアシスタント。`typescript` `claude` `openclaw` `hermes-agent`。 https://github.com/ThinkInAIXYZ/deepchat
- **Sylinko/Everywhere**（6,347 / C#）: 画面上のアプリ文脈を理解するデスクトップAIアシスタント。`claude` `openclaw` `hermes-agent`。 https://github.com/Sylinko/Everywhere

## 優先トピックの動き（まとめ）

- **claude / typescript:** rea、claude-mem、orca、deepseek-harness、hallmark など上位の大半。エージェント系が主役。
- **hermes-agent:** 該当で伸びたのは stablyai/orca（116,383、+6,474）。NousResearch/hermes-agent 自体は260,794スター（先週258,421から約+2,400）。新規では deepchat、Everywhere（いずれも1万未満）が `hermes-agent` トピックを持つ。
- **python:** VoiceStudio、Scrapling、cleanyourtv、DeepTutor、iFixAi、flask（新規）など多数。
- **rust:** impeccable（+8,861）、reaも該当。clash-verge-rev・cc-switch・photocraftも集計中。
- **go:** wagoodman/dive が新規。awesome-go は集計中。
- **nextjs:** vercel/chatbot（新規）、leerob/next-mdx-blog（1万未満の注目枠）。
- **docker / angular / openclaw / nix:** docker は dive、angular は realworld、openclaw は Memori・Orkas 等が登場。nix は目立った動きなし。

## 集計メモ

- データ元: GitHub公式REST Search API / 集計日 2026-11-05 / 前回 2026-10-29
- 掲載基準: スター10,000以上・開発者向け。優先トピックのみ1万未満も別枠。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
