作成日: 2026-09-11 / STATUS: INFO / TOPIC: TRENDING

# GitHub週間トレンド（2026-09-11号）

GitHub公式REST Search APIから取得した、開発者向けの注目リポジトリまとめです。掲載基準は「スター1万以上」。前週（2026-09-04）比でスターが伸びた「上昇銘柄（risers）」と、今回新たに基準を満たした「新規ランクイン（newcomers）」を中心に紹介します。優先トピック（go, rust, typescript, python, nextjs, claude, hermes-agent など）は1万未満でも注目枠として別途掲載します。

> 用語メモ: 「スター」はGitHub上の「いいね」的な指標です。「フォーク」は元リポジトリを複製して自分の環境で改造できるようにする機能です。

---

## 🆕 新規ランクイン（スター1万以上、今回初登場）

### massgravel/Microsoft-Activation-Scripts
- **概要:** Windows/Officeのオープンソース版アクティベーター（HWID・Ohook・TSforge・オンラインKMS対応）。
- **注目理由:** 定番の実用ツールとして根強い人気があり、今回初めて追跡プールに登場。
- **主な特徴:** 複数のアクティベーション方式を1つにまとめ、トラブルシューティング機能も搭載。
- **スター数:** 190,193 / **主要言語:** Batchfile
- **リンク:** https://github.com/massgravel/Microsoft-Activation-Scripts

### abi/screenshot-to-code
- **概要:** スクリーンショットを取り込むとHTML/Tailwind/React/Vueのコードに変換してくれるツール。
- **注目理由:** 「デザインをそのままコード化する」というAI活用の分かりやすい事例。
- **主な特徴:** 複数のフロントエンド技術スタックへの出力に対応。
- **スター数:** 78,554 / **主要言語:** Python（優先トピック該当）
- **リンク:** https://github.com/abi/screenshot-to-code

### PKUFlyingPig/cs-self-learning
- **概要:** 中国語で書かれたコンピュータサイエンス独学ガイド。
- **注目理由:** 体系立った学習ロードマップとして継続的に支持を集めている。
- **主な特徴:** 大学レベルのCS科目を独学するための教材・書籍・講義リストをまとめている。
- **スター数:** 75,550 / **主要言語:** HTML
- **リンク:** https://github.com/PKUFlyingPig/cs-self-learning

### pallets/flask
- **概要:** Pythonの定番軽量Webフレームワーク「Flask」本体リポジトリ。
- **注目理由:** 老舗フレームワークながら継続的にメンテナンスが行われ、今回追跡対象に入った。
- **主な特徴:** Jinjaテンプレート・Werkzeugと組み合わせたシンプルなWSGI構成。
- **スター数:** 74,273 / **主要言語:** Python（優先トピック該当）
- **リンク:** https://github.com/pallets/flask

### OpenBB-finance/OpenBB
- **概要:** アナリスト・クオンツ・AIエージェント向けのオープンデータプラットフォーム。
- **注目理由:** 金融データ分析とAIエージェントの接続という需要の高い分野。
- **主な特徴:** 株式・暗号資産・デリバティブなど幅広い金融データをPythonで扱える。
- **スター数:** 72,885 / **主要言語:** Python（優先トピック該当）
- **リンク:** https://github.com/OpenBB-finance/OpenBB

### base/node
- **概要:** Base（Coinbase系のL2チェーン）のノードを自前で立てるための一式。
- **注目理由:** ブロックチェーンインフラを個人・組織で運用したい層から支持。
- **主な特徴:** シェルスクリプトベースでセットアップを簡略化。
- **スター数:** 68,385 / **主要言語:** Shell
- **リンク:** https://github.com/base/node

### Fission-AI/OpenSpec
- **概要:** AIコーディングアシスタント向けの「仕様駆動開発（SDD）」ツール。
- **注目理由:** AIエージェント時代の開発フロー標準化を狙う動きの一つ。
- **主な特徴:** 要件定義・計画・仕様書作成を構造化して支援。
- **スター数:** 67,993 / **主要言語:** TypeScript（優先トピック該当）
- **リンク:** https://github.com/Fission-AI/OpenSpec

### leonardomso/33-js-concepts
- **概要:** JavaScript開発者が知っておくべき33の概念をまとめた学習リポジトリ。
- **注目理由:** 定番の学習コンテンツとして長期的に人気を維持。
- **主な特徴:** クロージャ・ES6・プロトタイプなど基礎から実践までカバー。
- **スター数:** 66,525 / **主要言語:** JavaScript（Angularトピックにも関連）
- **リンク:** https://github.com/leonardomso/33-js-concepts

### QuantumNous/new-api
- **概要:** 複数のLLM（OpenAI/Claude/Gemini互換）を統合するAIゲートウェイ。
- **注目理由:** 個人・企業向けのモデル一元管理ニーズに応える構成。
- **主な特徴:** OpenAI互換APIとして各種LLMプロバイダーを束ねる中継役。
- **スター数:** 47,919 / **主要言語:** Go（優先トピック該当・Claude関連）
- **リンク:** https://github.com/QuantumNous/new-api

### ayghri/i-have-adhd
- **概要:** コーディングエージェントの回答が冗長にならないようにするスキル。
- **注目理由:** AIエージェントの「要点が埋もれる」問題への実用的な解決策。
- **主な特徴:** ADHDフレンドリーな簡潔出力を強制する仕組み。
- **スター数:** 40,751 / **主要言語:** Python（優先トピック該当・Claude関連）
- **リンク:** https://github.com/ayghri/i-have-adhd

### cathrynlavery/diagram-design
- **概要:** Claude Code・Codex・Pi向けの図解テンプレート集（38種類）。
- **注目理由:** AIエージェントが生成する図の質を底上げする実用スキル。
- **主な特徴:** HTML+SVGで自己完結、Mermaidに頼らない見た目重視の設計。
- **スター数:** 38,350 / **主要言語:** HTML（Claude関連）
- **リンク:** https://github.com/cathrynlavery/diagram-design

### vercel-labs/skills
- **概要:** Vercel製のオープンなエージェントスキル管理ツール。
- **注目理由:** `npx skills` で手軽に導入できる点が支持されている。
- **主な特徴:** エージェントスキルの配布・利用を簡単にするCLI。
- **スター数:** 31,403 / **主要言語:** TypeScript（優先トピック該当）
- **リンク:** https://github.com/vercel-labs/skills

---

## 📈 上昇銘柄（前週比スター増加数トップ）

### tt-a1i/archify（+10,718）
- **概要:** アーキテクチャ図・シーケンス図などを自動生成するエージェントスキル。
- **注目理由:** 今週最大の伸び幅。AIコーディングエージェント向け図解ツール需要の高さを示す。
- **主な特徴:** モーション付きの自己完結HTML出力、クリアなエクスポート機能。
- **スター数:** 58,286 / **主要言語:** JavaScript（Claude関連）
- **リンク:** https://github.com/tt-a1i/archify

### DietrichGebert/ponytail（+10,642）
- **概要:** AIエージェントに「怠惰なベテランエンジニア」のように考えさせるスキル。
- **注目理由:** 「書かなくていいコードは書かない」という思想が共感を呼んでいる。
- **主な特徴:** YAGNI原則をベースにしたClaude Code向けプラグイン。
- **スター数:** 135,589 / **主要言語:** JavaScript（Claude関連）
- **リンク:** https://github.com/DietrichGebert/ponytail

### mattpocock/skills（+9,990）
- **概要:** 個人の`.agents`ディレクトリから公開されたエンジニア向けスキル集。
- **注目理由:** 著名開発者の実践ノウハウがそのまま公開されている点が支持を集める。
- **主な特徴:** シェルベースの実用スキルを幅広く収録。
- **スター数:** 259,563 / **主要言語:** Shell
- **リンク:** https://github.com/mattpocock/skills

### deepseek-ai/deepseek-harness（+8,293）
- **概要:** DeepSeek製のエージェントハーネス。「すべてがプラグイン」という設計思想。
- **注目理由:** 大手AI企業発のエージェント基盤として急速に採用が広がっている。
- **主な特徴:** プラグイン機構によって拡張しやすいアーキテクチャ。
- **スター数:** 220,353 / **主要言語:** TypeScript（優先トピック該当）
- **リンク:** https://github.com/deepseek-ai/deepseek-harness

### affaan-m/ECC（+8,254）
- **概要:** Claude Code・Codex・Cursorなど複数のエージェントハーネスを最適化するシステム。
- **注目理由:** スキル・記憶・セキュリティを統合したエージェント性能改善の取り組み。
- **主な特徴:** リサーチファーストな開発アプローチを採用。
- **スター数:** 256,332 / **主要言語:** JavaScript（Claude関連）
- **リンク:** https://github.com/affaan-m/ECC

### stablyai/orca（+5,048）
- **概要:** 複数のコーディングエージェントを並列で動かすためのADE（Agent Development Environment）。
- **注目理由:** デスクトップ・モバイル・リモートで動作する柔軟性が評価されている。
- **主な特徴:** 自分のサブスクリプションでどのコーディングエージェントも動かせる。
- **スター数:** 66,588 / **主要言語:** TypeScript（優先トピック該当・Claude関連）
- **リンク:** https://github.com/stablyai/orca

### heygen-com/hyperframes（+5,027）
- **概要:** HTMLを書くだけで動画をレンダリングできる、エージェント向けフレームワーク。
- **注目理由:** 動画生成の自動化ニーズとAIエージェントの相性の良さを示す事例。
- **主な特徴:** FFmpeg・GSAPを組み合わせたアニメーション対応。
- **スター数:** 48,964 / **主要言語:** TypeScript（優先トピック該当）
- **リンク:** https://github.com/heygen-com/hyperframes

### microsoft/markitdown（+4,502）
- **概要:** Microsoft製、各種ファイル・Office文書をMarkdownに変換するツール。
- **注目理由:** LLMへの文書投入前処理として定番化しつつある。
- **主な特徴:** PDF・Office文書など幅広い形式に対応。
- **スター数:** 182,628 / **主要言語:** Python（優先トピック該当）
- **リンク:** https://github.com/microsoft/markitdown

### blader/humanizer（+4,441）
- **概要:** AI生成文章特有の「らしさ」を除去するエージェントスキル。
- **注目理由:** AI文章の質に対する不満が根強く、実用的な解決ニーズが高い。
- **主な特徴:** Claude Code・Codex・Cursorから呼び出し可能。
- **スター数:** 46,828 / **主要言語:** Python（優先トピック該当・Claude関連）
- **リンク:** https://github.com/blader/humanizer

### THU-MAIC/OpenMAIC（+4,414）
- **概要:** 清華大学発、マルチエージェント型のインタラクティブ教室システム。
- **注目理由:** 教育分野でのマルチエージェント活用という新しい切り口。
- **主な特徴:** ワンクリックで没入型の学習体験を構築できる。
- **スター数:** 35,806 / **主要言語:** TypeScript（優先トピック該当）
- **リンク:** https://github.com/THU-MAIC/OpenMAIC

### public-apis/public-apis（+3,689）
- **概要:** 無料で使えるAPIのまとめリスト。
- **注目理由:** 定番リポジトリながら着実にスターを積み増している。
- **主な特徴:** カテゴリ別に整理された巨大なAPIカタログ。
- **スター数:** 478,913 / **主要言語:** Python（優先トピック該当）
- **リンク:** https://github.com/public-apis/public-apis

### NousResearch/hermes-agent（+3,181）
- **概要:** 本アシスタント（Prime）の実行基盤であるHermes Agent本体。
- **注目理由:** 優先トピック「hermes-agent」自身が着実に成長中。
- **主な特徴:** 「成長し続けるエージェント」をコンセプトに、拡張性の高い設計。
- **スター数:** 244,508 / **主要言語:** Python（優先トピック該当・Claude関連）
- **リンク:** https://github.com/NousResearch/hermes-agent

---

## 🔎 優先トピック注目枠（スター1万未満だが要チェック）

### mnfst/llm-gateway
- **概要:** エージェント・ハーネスを任意のLLMプロバイダーに接続するゲートウェイ。
- **注目理由:** hermes-agentタグを含む数少ない新興プロジェクト。
- **主な特徴:** コスト・トークン使用量の追跡機能を搭載。
- **スター数:** 7,517 / **主要言語:** TypeScript
- **リンク:** https://github.com/mnfst/llm-gateway

### Devin-AXIS/iPolloWork
- **概要:** Codex/DeepSeek Harness/OpenCode横断で動くローカルファーストなAgent Workbench。
- **注目理由:** 複数エージェントエンジンの統合ワークスペースという意欲的な設計。
- **主な特徴:** プラグイン・スキル・マルチエージェントプロジェクト管理を統一UIで提供。
- **スター数:** 5,795 / **主要言語:** TypeScript
- **リンク:** https://github.com/Devin-AXIS/iPolloWork

### vvo/iron-session
- **概要:** Next.js等向けのステートレス・Cookieベースセッションライブラリ。
- **注目理由:** nextjs/typescriptトピックでの定番ユーティリティとして継続的に利用。
- **主な特徴:** サーバーレス環境でも扱いやすい軽量設計。
- **スター数:** 4,140 / **主要言語:** TypeScript
- **リンク:** https://github.com/vvo/iron-session

---

## 📋 その他、優先トピックで話題のリポジトリ（参考・簡易掲載）

スター1万以上かつ優先トピック該当だが、上記の新規/上昇枠に含まれなかったものを簡易リストで紹介します。

| リポジトリ | スター数 | 主要言語 | 優先トピック |
|---|---|---|---|
| [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) | 212,291 | - | claude |
| [yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp) | 190,441 | Python | python |
| [anthropics/skills](https://github.com/anthropics/skills) | 175,805 | Python | python, claude |
| [github/spec-kit](https://github.com/github/spec-kit) | 135,628 | Python | python |
| [clash-verge-rev/clash-verge-rev](https://github.com/clash-verge-rev/clash-verge-rev) | 143,827 | Rust | rust |
| [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | 126,860 | Python | python, claude |
| [openai/codex](https://github.com/openai/codex) | 123,371 | Rust | rust |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 122,445 | Python | python |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 116,938 | Python | python, claude |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 114,202 | Python | python |
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | 104,945 | Go | go, claude |
| [earendil-works/pi](https://github.com/earendil-works/pi) | 104,107 | TypeScript | typescript |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 104,654 | Python | python |
| [nexu-io/open-design](https://github.com/nexu-io/open-design) | 95,581 | TypeScript | typescript, claude, hermes-agent |
| [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | 86,225 | JavaScript | claude |
| [D4Vinci/Scrapling](https://github.com/D4Vinci/Scrapling) | 80,254 | Python | python |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 79,436 | Python | python, claude |
| [datawhalechina/hello-agents](https://github.com/datawhalechina/hello-agents) | 78,439 | Python | python |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 71,541 | Python | typescript, python, claude |
| [ruvnet/ruflo](https://github.com/ruvnet/ruflo) | 72,097 | TypeScript | typescript, claude |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 179,101 | TypeScript | typescript |
| [vinta/awesome-python](https://github.com/vinta/awesome-python) | 319,982 | Python | python |

---

## 📝 まとめ

- 今週は新規ランクイン12件（1万スター以上）、上昇銘柄11件を中心に掲載しました。
- 優先トピックでは特に **claude** 関連（AIコーディングエージェント向けスキル・ハーネス）の勢いが顕著で、archify・ponytail・deepseek-harness・ECCなど、いずれも「AIエージェントの作業効率を上げるツール」が上位に並びました。
- **hermes-agent** タグ自体は本体リポジトリ（NousResearch/hermes-agent）が+3,181と堅調な伸び。関連プロジェクト（mnfst/llm-gateway、Devin-AXIS/iPolloWork、nexu-io/open-design）も継続的に登場しており、エコシステムの広がりが感じられます。
- 今回は基準日（2026-09-11）と前週（2026-09-04）の比較データです。次週以降も継続してウォッチします。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
