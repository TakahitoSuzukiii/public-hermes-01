作成日: 2026-10-22 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-10-22 週）

GitHub公式REST Search APIで集めた人気リポジトリ（スター10,000以上、母集団356件）を、前週（2026-10-15）と比べた差分レポートです。
「risers」は前週よりスターが増えたリポジトリ、「newcomers」は今週新しく集計対象に入ったリポジトリです。

> 用語: **スター** = GitHubで「気に入った」を示す印。人気の目安。**エージェント** = AIが自律的に作業を進める仕組み。**スキル** = AIエージェントに追加する手順書・拡張。

## 今週の全体傾向

- **AIコーディングエージェント周辺**（Claude Code用スキル/プラグイン、ハーネス、オーケストレーション）が引き続き上位を占めています。
- **逆アセンブル・リバースエンジニアリング系**（rea、Ghidra）が同時に伸びています。
- 純粋なツール以外にも、ローカルで動く音声合成（VoiceStudio）、Rust製フォトエディタなど「自前で動かせるOSS」が増加しました。

## 🔺 前週比で伸びたリポジトリ（risers）

| 順位 | リポジトリ | スター | 前週比 | 主要言語 |
|---|---|---|---|---|
| 1 | morluto/rea | 364,050 | +100,292 | TypeScript |
| 2 | debpalash/VoiceStudio | 81,415 | +13,051 | Python |
| 3 | stablyai/orca | 102,484 | +9,291 | TypeScript |
| 4 | DietrichGebert/ponytail | 172,950 | +8,764 | JavaScript |
| 5 | boykopovar/AnyPS5 | 46,721 | +8,594 | C++ |
| 6 | storytold/photocraft | 71,158 | +8,413 | Rust |
| 7 | mattpocock/skills | 300,661 | +8,235 | Shell |
| 8 | deepseek-ai/deepseek-harness | 257,986 | +7,664 | TypeScript |
| 9 | anomalyco/opencode | 220,063 | +6,245 | TypeScript |
| 10 | affaan-m/ECC | 286,250 | +6,198 | JavaScript |
| 11 | Graphify-Labs/graphify | 132,590 | +5,796 | Python |
| 12 | heygen-com/hyperframes | 69,801 | +5,499 | TypeScript |
| 13 | anthropics/claude-plugins-official | 43,809 | +5,173 | Python |
| 14 | NationalSecurityAgency/ghidra | 93,002 | +4,622 | Java |

### 注目リポジトリ詳細

#### morluto/rea（+100,292 ⭐ 今週の最大の伸び）
- **概要:** AIエージェントを使い、アプリの挙動からネイティブバイナリまで「何でもリバースエンジニアリング」するツール。
- **注目理由:** 1週間で約10万スター増という突出した伸び。
- **主な特徴:** エージェント駆動の解析 / TypeScript製 / Claude系の利用に対応。
- **スター数:** 364,050 / **言語:** TypeScript
- リンク: https://github.com/morluto/rea

#### stablyai/orca
- **概要:** 複数のコーディングエージェント（Claude Code等）を「艦隊」のようにまとめて動かす作業場。
- **注目理由:** 優先トピック `hermes-agent` `claude` `openclaw` `typescript` に該当。Hermes関連で今週最も目立つ。
- **スター数:** 102,484 / **言語:** TypeScript
- リンク: https://github.com/stablyai/orca

#### debpalash/VoiceStudio
- **概要:** ElevenLabsの代替を目指す、完全ローカル動作のOSS。音声クローン、音声デザイン、動画吹き替えなど。
- **注目理由:** 完全ローカル=無料・プライバシー重視の流れに合致。
- **スター数:** 81,415 / **言語:** Python
- リンク: https://github.com/debpalash/VoiceStudio

#### DietrichGebert/ponytail
- **概要:** AIエージェントに「一番怠け者の熟練開発者」のように考えさせる（書かないコードが最良）スキル。
- **スター数:** 172,950 / **言語:** JavaScript
- リンク: https://github.com/DietrichGebert/ponytail

#### storytold/photocraft
- **概要:** 純粋なRustでゼロから書かれたOSSの写真編集ソフト。
- **注目理由:** 優先トピック `rust`。
- **スター数:** 71,158 / **言語:** Rust
- リンク: https://github.com/storytold/photocraft

#### その他の伸びたリポジトリ
- **mattpocock/skills**（300,661 / Shell）: 実務エンジニア向けのエージェント用スキル集。 https://github.com/mattpocock/skills
- **deepseek-ai/deepseek-harness**（257,986 / TypeScript）: 「すべてがプラグイン」のエージェントハーネス。 https://github.com/deepseek-ai/deepseek-harness
- **anomalyco/opencode**（220,063 / TypeScript）: オープンソースのコーディングエージェント。 https://github.com/anomalyco/opencode
- **affaan-m/ECC**（286,250 / JavaScript）: エージェントの性能最適化システム（スキル・記憶・セキュリティ等）。 https://github.com/affaan-m/ECC
- **Graphify-Labs/graphify**（132,590 / Python）: コードや文書、SQLスキーマをクエリ可能な知識グラフに変換。 https://github.com/Graphify-Labs/graphify
- **heygen-com/hyperframes**（69,801 / TypeScript）: HTMLを書いて動画をレンダリング。エージェント向け。 https://github.com/heygen-com/hyperframes
- **anthropics/claude-plugins-official**（43,809 / Python）: Anthropic管理の公式Claude Codeプラグイン集。 https://github.com/anthropics/claude-plugins-official
- **NationalSecurityAgency/ghidra**（93,002 / Java）: 米NSA開発のリバースエンジニアリング基盤。 https://github.com/NationalSecurityAgency/ghidra
- **boykopovar/AnyPS5**（46,721 / C++）: PS5実行ファイルをLinux/Windowsへ移植するツール。 https://github.com/boykopovar/AnyPS5

## 🆕 今週の新規ランクイン（newcomers）

| リポジトリ | スター | 言語 | 概要 |
|---|---|---|---|
| labuladong/fucking-algorithm | 135,948 | Markdown | LeetCode攻略。「どう」だけでなく「なぜ」まで解説 |
| d3/d3 | 113,794 | Shell(表示) | SVG/Canvas/HTMLでデータを可視化するライブラリ |
| microsoft/ML-For-Beginners | 91,669 | Jupyter Notebook | 12週・26レッスンの機械学習入門 |
| cheaper-inference/OmniRoute | 79,735 | TypeScript | 1つの窓口で多数のAIプロバイダーに接続するMITライセンスのゲートウェイ |
| doocs/advanced-java | 79,162 | Java | Javaバックエンド開発者向け面接・知識まとめ（中国語） |
| tw93/Mole | 72,362 | Shell | Mac/PCを軽く保つCLIツール |
| ai-job-search-dev/ai-job-search | 63,378 | Python | Claude Code上で動くAI求人応募フレームワーク |
| cloudflare/security-audit-skill | 38,677 | JavaScript | 多段階セキュリティ監査を行うエージェント用スキル |

※ 注意: 今週の新規には、ライセンス認証の回避ツールやハッキングツール集も含まれていましたが、「開発者向け」の掲載基準および安全上の観点から本記事では紹介を割愛しました。また「dsh-our-free-model」は無料モデル利用をうたうプラグインですが、提供元の信頼性が確認できていないため割愛しています。

## ⭐ 優先トピック注目枠（スター1万未満）

- **homarr-labs/dashboard-icons**（8,908 / TypeScript）: ダッシュボードやAIエージェント向けの3,400以上のアイコン。MCPサーバー付き。トピック: typescript / claude / openclaw / docker。 https://github.com/homarr-labs/dashboard-icons
- **Kiranism/next-shadcn-dashboard-starter**（7,157 / TypeScript）: Next.js 16 + shadcn/ui 製のAI対応管理画面テンプレート。トピック: nextjs。 https://github.com/Kiranism/next-shadcn-dashboard-starter
- **lingdojo/kana-dojo**（3,696 / TypeScript）: Duolingo風の日本語学習サイト（Next.js製）。トピック: nextjs。 https://github.com/lingdojo/kana-dojo

## 優先トピックの動き（まとめ）

- **claude / typescript:** rea、orca、ponytail、opencode、hyperframes など上位の大半。エージェント系が主役。
- **hermes-agent:** 今週の該当は stablyai/orca（スター102,484、+9,291）。
- **python:** VoiceStudio、graphify、claude-plugins-official、ML-For-Beginners。
- **rust:** photocraft（+8,413）が唯一の目立つ動き。
- **nextjs:** 1万未満の注目枠で2件（管理画面テンプレート、日本語学習）。
- **go / angular / nix:** 今週は目立った動きなし。

## 集計メモ

- データ元: GitHub公式REST Search API / 集計日 2026-10-22 / 前回 2026-10-15
- 掲載基準: スター10,000以上・開発者向け。優先トピックのみ1万未満も別枠。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
