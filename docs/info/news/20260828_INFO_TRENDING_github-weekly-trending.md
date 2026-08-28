# GitHub週次トレンド（2026-08-28）— deepseek-ai/deepseek-harnessが依然トップ急伸、AIエージェント関連が引き続き活発

作成日: 2026-08-28 / STATUS: INFO / TOPIC: TRENDING

> 掲載基準: スター数10,000以上・開発者向けリポジトリ。前週（2026-08-21）比でスターが増えた「急上昇（risers）」と、今回新たに基準を満たした「新登場（newcomers）」を中心に紹介します。優先トピック（go, rust, typescript, python, nextjs, claude, hermes-agent）は1万未満でも注目枠として別途掲載しています。

---

## 🚀 今週の急上昇（risers）

前週スナップショット（2026-08-21）と比較して、スターが大きく伸びたリポジトリです。

### 1. deepseek-ai/deepseek-harness（+21,557）｜優先トピック（typescript）
- **概要:** DeepSeekが公開したプラグイン中心設計のAIエージェントハーネス。「Everything is a Plugin」を掲げる。
- **注目理由:** 先週から引き続き急伸中。18万→20万スターを突破し、依然トップの伸び幅。
- **主な特徴:** プラグイン拡張前提のアーキテクチャ、AIエージェント構築向け。
- **スター数:** 201,777 / **言語:** TypeScript
- **リンク:** https://github.com/deepseek-ai/deepseek-harness

### 2. mattpocock/skills（+11,230）
- **概要:** エンジニア向けの実践的スキル集（`.agents`ディレクトリ由来）。
- **注目理由:** 先週に続き大幅増。AIコーディングエージェント向けスキル文化の広がりが加速。
- **主な特徴:** 実務で使えるスキル定義をそのまま公開。
- **スター数:** 239,973 / **言語:** Shell
- **リンク:** https://github.com/mattpocock/skills

### 3. openai/codex（+8,516）｜優先トピック（rust）
- **概要:** OpenAI製、ターミナルで動作する軽量コーディングエージェント。
- **注目理由:** Rust実装移行後も安定した支持を継続、着実に増加。
- **主な特徴:** ターミナル常駐型、軽量・高速。
- **スター数:** 119,503 / **言語:** Rust
- **リンク:** https://github.com/openai/codex

### 4. DietrichGebert/ponytail（+7,798）｜優先トピック（claude）
- **概要:** 「最も怠惰なシニアエンジニアのように考える」AIエージェント補助ツール。
- **注目理由:** 「書かないコードが一番良いコード」というYAGNI志向が引き続き支持され急伸。
- **主な特徴:** Claude Code連携、プロンプトエンジニアリング支援。
- **スター数:** 115,035 / **言語:** JavaScript
- **リンク:** https://github.com/DietrichGebert/ponytail

### 5. stablyai/orca（+5,364）｜優先トピック（typescript, claude）
- **概要:** 複数のコーディングエージェントを並列運用するためのADE（Agent Development Environment）。
- **注目理由:** デスクトップ／モバイル／VPS対応で、複数AIエージェントの並行運用ニーズに応え続けている。
- **主な特徴:** 既存サブスクリプションのエージェントをそのまま利用可能、ワークツリー管理。
- **スター数:** 55,922 / **言語:** TypeScript
- **リンク:** https://github.com/stablyai/orca

### 6. diegosouzapw/OmniRoute（+4,931）｜優先トピック（typescript, claude）
- **概要:** 340以上のプロバイダーに対応する無料AIゲートウェイ（1endpoint・1200以上モデル）。
- **注目理由:** Claude CodeやCodex等の主要エージェントから利用でき、トークン節約機能が引き続き人気。
- **主な特徴:** 自動フォールバック、MCP/A2A対応、450人以上のコントリビューター。
- **スター数:** 57,395 / **言語:** TypeScript
- **リンク:** https://github.com/diegosouzapw/OmniRoute

### 7. MadsLorentzen/ai-job-search（+4,780）｜優先トピック（python, claude）
- **概要:** Claude Code上で動くAI求職支援フレームワーク。求人評価・CV調整・カバーレター作成・面接準備まで自分のPC上で完結。
- **注目理由:** ローカル完結・フォーク前提の設計が、求職支援ツール需要の高まりの中で急伸。
- **主な特徴:** LaTeX出力対応、求人評価から面接準備まで一気通貫。
- **スター数:** 37,521 / **言語:** Python
- **リンク:** https://github.com/MadsLorentzen/ai-job-search

### 8. Alishahryar1/free-claude-code（+4,666）｜優先トピック（python, claude, openclaw）
- **概要:** Claude Code、Codex、Pi、OpenCode等を無料枠（13億トークン以上）で使えるようにするツール。
- **注目理由:** OpenClaw同様の使い勝手（音声対応・ToS配慮）を掲げ、無料利用ニーズを取り込み急伸。
- **主な特徴:** 端末・アプリ・IDE・スマホなど複数経路からの利用に対応。
- **スター数:** 51,098 / **言語:** Python
- **リンク:** https://github.com/Alishahryar1/free-claude-code

### 9. public-apis/public-apis（+4,394）｜優先トピック（python）
- **概要:** 無料で使えるAPIをまとめた定番リスト。
- **注目理由:** 定番リポジトリながら安定して伸び続けている。
- **主な特徴:** カテゴリ別に整理された膨大なAPI一覧。
- **スター数:** 472,185 / **言語:** Python
- **リンク:** https://github.com/public-apis/public-apis

### 10. harry0703/MoneyPrinterTurbo（+4,318）｜優先トピック（python）
- **概要:** AIとワークフロー自動化でテーマ・キーワードから高解像度ショート動画を一発生成するツール。
- **注目理由:** 動画生成AIの需要拡大を背景に継続的な人気上昇。
- **主な特徴:** FFmpeg連携、字幕・音声合成対応、TikTok/YouTube Shorts向け出力。
- **スター数:** 117,978 / **言語:** Python
- **リンク:** https://github.com/harry0703/MoneyPrinterTurbo

### 11. calesthio/OpenMontage（+3,863）｜優先トピック（python, claude）
- **概要:** オープンソースのエージェント型動画制作システム。12種類の制作パイプライン、100以上のツール、700以上のスキル・知識ファイルを搭載。
- **注目理由:** コーディングエージェントを本格的な動画制作スタジオに変えるという野心的なアプローチが支持を集める。
- **主な特徴:** Remotion、Stable Diffusion、ElevenLabs等の連携。
- **スター数:** 53,082 / **言語:** Python
- **リンク:** https://github.com/calesthio/OpenMontage

### 12. NousResearch/hermes-agent（+3,785）｜優先トピック（python, claude, hermes-agent）
- **概要:** 本Optimusの基盤でもあるNous Research製AIエージェント。
- **注目理由:** 自プロジェクトの動向として継続監視。着実にスターを伸ばしている。
- **主な特徴:** Claude/Codex等マルチLLM対応、拡張可能なエージェント基盤。
- **スター数:** 237,657 / **言語:** Python
- **リンク:** https://github.com/NousResearch/hermes-agent

### 13. earendil-works/pi（+3,738）｜優先トピック（typescript）
- **概要:** 統一LLM APIとエージェントループ、TUIを備えたAIエージェントツールキット。
- **注目理由:** コーディングエージェントCLI基盤として採用が広がっている。
- **主な特徴:** TUI付き、複数LLMを統一APIで扱える。
- **スター数:** 98,699 / **言語:** TypeScript
- **リンク:** https://github.com/earendil-works/pi

### 14. multica-ai/andrej-karpathy-skills（+3,549）｜優先トピック（claude）
- **概要:** Andrej Karpathy氏のLLMコーディングに関する知見から作られた、Claude Codeの挙動を改善する単一のCLAUDE.mdファイル。
- **注目理由:** シンプルな設定ファイル一枚という手軽さで支持を集めている。
- **主な特徴:** 導入が容易、Claude Code特化。
- **スター数:** 208,353 / **言語:** （未設定）
- **リンク:** https://github.com/multica-ai/andrej-karpathy-skills

### 15. obra/superpowers（+3,475）
- **概要:** エージェント向けスキルフレームワーク兼ソフトウェア開発方法論。
- **注目理由:** 27万超スターの大型リポジトリが依然として伸び続けている。
- **主な特徴:** サブエージェント駆動開発（SDLC）を提唱。
- **スター数:** 278,957 / **言語:** Shell
- **リンク:** https://github.com/obra/superpowers

---

## 🆕 新登場（newcomers・スター1万以上）

今回のプール（母集団）に新たに登場したリポジトリです。

| リポジトリ | スター数 | 言語 | 概要 |
|---|---|---|---|
| [github/gitignore](https://github.com/github/gitignore) | 175,483 | - | 各種言語・環境向けの`.gitignore`テンプレート集 |
| [papers-we-love/papers-we-love](https://github.com/papers-we-love/papers-we-love) | 109,059 | Shell | 読んで議論する価値のあるコンピュータサイエンス論文集 |
| [Developer-Y/cs-video-courses](https://github.com/Developer-Y/cs-video-courses) | 83,194 | - | 動画講義付きコンピュータサイエンス講座リスト |
| [Z4nzu/hackingtool](https://github.com/Z4nzu/hackingtool)｜優先トピック（python） | 79,152 | Python | ハッキングツールをオールインワンでまとめたツール集 |
| [doocs/advanced-java](https://github.com/doocs/advanced-java) | 79,088 | Java | Javaバックエンドエンジニア向け上級面接対策・知識まとめ |
| [hakimel/reveal.js](https://github.com/hakimel/reveal.js) | 72,226 | JavaScript | HTMLベースのプレゼンテーションフレームワーク |
| [expressjs/express](https://github.com/expressjs/express) | 69,401 | JavaScript | Node.js向け定番の軽量Webフレームワーク |
| [prisma/orm](https://github.com/prisma/orm)｜優先トピック（typescript） | 47,567 | TypeScript | Node.js/TypeScript向け次世代ORM |
| [Asabeneh/30-Days-Of-JavaScript](https://github.com/Asabeneh/30-Days-Of-JavaScript)｜優先トピック（typescript, angular） | 46,742 | JavaScript | 30日間でJavaScriptを学ぶ実践チャレンジ教材 |
| [helix-editor/helix](https://github.com/helix-editor/helix)｜優先トピック（rust） | 45,963 | Rust | ポストモダンなモーダルテキストエディタ |
| [mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)｜優先トピック（python, claude） | 31,477 | Python | AIエージェント向けサイバーセキュリティスキル集（MITRE ATT&CK等主要フレームワーク対応） |
| [block/buzz](https://github.com/block/buzz)｜優先トピック（rust） | 31,255 | Rust | ハイブマインド型コミュニケーションプラットフォーム |
| [CloakHQ/CloakBrowser](https://github.com/CloakHQ/CloakBrowser)｜優先トピック（python） | 30,918 | Python | ボット検知を回避するステルスChromium、Playwrightの代替 |
| [titanwings/distilly](https://github.com/titanwings/distilly)｜優先トピック（python, claude, openclaw, hermes-agent） | 24,081 | Python | 同僚の思考パターンを再利用可能なスキルに蒸留するツール（旧Colleague Skill） |
| [codesandbox/codesandbox-client](https://github.com/codesandbox/codesandbox-client)｜優先トピック（angular） | 13,638 | JavaScript | Web開発向けオンラインIDE |
| [al1abb/invoify](https://github.com/al1abb/invoify)｜優先トピック（typescript, nextjs） | 6,349 | TypeScript | Next.js製の請求書作成アプリ（注目枠として掲載） |
| [ipetkov/crane](https://github.com/ipetkov/crane)｜優先トピック（rust, nix） | 1,451 | Nix | Cargoプロジェクトをビルドするためのライブラリ（注目枠として掲載） |

**注目ピックアップ:**
- **titanwings/distilly** — hermes-agent含む複数の優先トピックに該当。Optimusのようなエージェントの「思考パターン」を再利用可能なスキルへ蒸留する試みで、今後の動向を継続監視。
- **mukul975/Anthropic-Cybersecurity-Skills** — 鈴木さんのバグバウンティ学習に関連しうるセキュリティ特化スキル集。29のセキュリティ領域をカバー。
- **prisma/orm** — TypeScriptエコシステムの定番ORMとして再度プールに登場。

---

## 🎯 優先トピック注目枠（スター1万未満）

上記表内の`al1abb/invoify`・`ipetkov/crane`に加え、以下も動きが見られました。

（今週は上記新登場一覧内に優先トピック該当の1万未満リポジトリを含めて掲載しています。）

---

## 📊 優先トピックの動向まとめ

今回のプール（450件）のうち385件が優先トピック（go/rust/typescript/python/nextjs/claude/hermes-agent等）に該当しており、AIコーディングエージェント関連（claude, hermes-agent）の話題が引き続き非常に活発でした。急上昇・新登場のほか、以下のような大型リポジトリも安定した人気を維持しています。

- **anomalyco/opencode**（202,140★・TypeScript）— オープンソースのコーディングエージェント
- **affaan-m/ECC**（243,909★・JavaScript）— Claude Code/Codex等向けエージェントハーネス性能最適化システム
- **nexu-io/open-design**（92,322★・優先トピック: claude, hermes-agent）— コーディングエージェントをデザインエンジンに変えるデスクトップアプリ
- **firecrawl/firecrawl**（173,510★・TypeScript）— LLM向けWebスクレイピング・検索コンテキストAPI
- **volcengine/OpenViking**（34,086★・Python）— エージェント向け自己進化型コンテキストDB
- **santifer/career-ops**（69,057★・優先トピック: go, claude）— オープンソースのAI求職支援ツール
- **herdrdev/herdr**（33,140★・Rust）— コーディングエージェントを動かすランタイム／ターミナルマルチプレクサ
- **Panniantong/Agent-Reach**（76,292★・Python）— AIエージェントにSNS・Web横断の検索能力を与えるCLIツール
- **nextlevelbuilder/ui-ux-pro-max-skill**（122,473★・Python）— UI/UXデザインインテリジェンスを提供するAIスキル

hermes-agentトピックでは、本体（NousResearch/hermes-agent）に加え、`nexu-io/open-design`・`titanwings/distilly`など、周辺エコシステムのリポジトリも継続的に伸びています。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
