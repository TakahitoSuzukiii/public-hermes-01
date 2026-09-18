作成日: 2026-09-18 / STATUS: INFO / TOPIC: TRENDING

# GitHub週次トレンド（2026-09-18）

GitHub公式REST Search APIから、スター数10,000以上かつ開発者向けのリポジトリを対象に、前週（2026-09-11時点）との比較でスターが伸びたリポジトリ（risers）と、今回新たに掲載条件を満たしたリポジトリ（newcomers）をまとめました。加えて、注目トピック（go / rust / typescript / python / nextjs / claude / hermes-agent）関連の動きも別枠で紹介します。

> 対象プール: 453件 / 基準スター: 10,000以上 / 前回集計日: 2026-09-11

---

## 🆕 新規掲載（newcomers）

今回初めて掲載条件（スター1万以上）を満たしたリポジトリです。

### donnemartin/system-design-primer（370,629★・Python）
- **概要:** 大規模システム設計の学習リポジトリ。システム設計面接の対策資料としても有名。
- **注目理由:** 定番の学習教材として長期的に支持されており、開発者コミュニティで再注目された週。
- **主な特徴:** Ankiフラッシュカード付き、設計パターン・面接問答を体系的にカバー。
- **リンク:** https://github.com/donnemartin/system-design-primer

### microsoft/Web-Dev-For-Beginners（96,700★・JavaScript）
- **概要:** Microsoftが提供するWeb開発初学者向けの12週間カリキュラム。
- **注目理由:** 教育系コンテンツとして安定した人気を維持し、今回新規掲載入り。
- **主な特徴:** 24レッスン構成、HTML/CSS/JavaScriptの基礎を体系的に学べる。
- **リンク:** https://github.com/microsoft/Web-Dev-For-Beginners

### PaddlePaddle/PaddleOCR（89,781★・Python）
- **概要:** PDFや画像をAI処理向けの構造化データへ変換する軽量OCRツールキット。
- **注目理由:** RAG（検索拡張生成）向けのドキュメント処理需要の高まりを背景に伸長。
- **主な特徴:** 100以上の言語に対応、PP-OCR/PP-Structureなど多様なモデルを内包。
- **リンク:** https://github.com/PaddlePaddle/PaddleOCR

### macrozheng/mall（84,794★・Java）
- **概要:** Spring Boot + MyBatisで構築されたECサイト向けフルスタックシステム。
- **注目理由:** 中国圏の実務向けオープンソースとして継続的に参照されている。
- **主な特徴:** Docker対応、商品/注文/会員/決済など一般的なEC機能を一通り実装。
- **リンク:** https://github.com/macrozheng/mall

### vuejs/awesome-vue（73,546★）
- **概要:** Vue.js関連のツール・ライブラリ・学習リソースのキュレーションリスト。
- **注目理由:** Vue公式organizationのリファレンス的リポジトリとして安定した参照数。
- **主な特徴:** プラグイン、UIコンポーネント、学習素材などをカテゴリ別に整理。
- **リンク:** https://github.com/vuejs/awesome-vue

### sharkdp/fd（44,475★・Rust）
- **概要:** Unix系OSの`find`コマンドを置き換える高速・使いやすいCLIツール。
- **注目理由:** Rust製CLIツールの定番として継続的に採用が広がっている。
- **主な特徴:** 正規表現検索、直感的なデフォルト動作、クロスプラットフォーム対応。
- **リンク:** https://github.com/sharkdp/fd

### bilawalsidhu/gods-eye-view（37,567★・JavaScript）
- **概要:** ブラウザで動くスパイ衛星シミュレーター。実際の公開データを使用。
- **注目理由:** OSINT（公開情報インテリジェンス）とWebGL技術を組み合わせた話題性のあるプロジェクト。
- **主な特徴:** フォトリアルな3Dグローブ表示、フライト追跡・衛星追跡データを統合。
- **リンク:** https://github.com/bilawalsidhu/gods-eye-view

### alibaba/open-code-review（36,395★・Go）※注目トピック（go, claude）
- **概要:** アリババ発のコードレビュー支援ツール。ルールベース処理とLLMエージェントを組み合わせるハイブリッド構成。
- **注目理由:** 大規模運用で実績のあるコードレビュー自動化ツールとしてOSS公開。
- **主な特徴:** 行単位の精密コメント、多言語ルールセット（NPE/スレッド安全性/XSS/SQLインジェクション等）、OpenAI・Anthropic互換。
- **リンク:** https://github.com/alibaba/open-code-review

### JustVugg/colibri（36,069★・C）
- **概要:** 大規模MoE（混合エキスパート）モデルを一般的なハードウェア上で動かすための軽量推論エンジン。
- **注目理由:** ゼロ依存・純Cによる省メモリ実装がAI開発者コミュニティで話題化。
- **主な特徴:** ディスクからエキスパートをストリーミング読み込みし、限られたメモリでも大規模モデルを実行可能。
- **リンク:** https://github.com/JustVugg/colibri

### debpalash/VoiceStudio（32,757★・Python）※注目トピック（python）
- **概要:** ElevenLabsの代替となる、完全ローカル動作の音声合成・音声クローンツール。
- **注目理由:** ローカルAI音声処理への需要増加を反映し急速に注目度が上昇。
- **主な特徴:** 646言語対応、音声クローン・動画吹き替え・文字起こし・オーディオブック生成まで一貫対応。
- **リンク:** https://github.com/debpalash/VoiceStudio

### freestylefly/awesome-gpt-image-2（32,650★・JavaScript）
- **概要:** GPT Image 2/2.5向けのプロンプト集・テンプレート集。
- **注目理由:** 画像生成AIの実践的プロンプトエンジニアリング資料として利用が拡大。
- **主な特徴:** 530以上のケース、20以上のテンプレート、再利用可能なSkills形式で整理。
- **リンク:** https://github.com/freestylefly/awesome-gpt-image-2

### sweetalert2/sweetalert2（18,103★・JavaScript）※注目トピック（angular関連）
- **概要:** JavaScript標準のポップアップを置き換える、アクセシブルなアラート/モーダルライブラリ。
- **注目理由:** 依存ゼロでReact/Vue/Angularいずれとも組み合わせやすく、フロントエンド界で定番化。
- **主な特徴:** WAI-ARIA準拠のアクセシビリティ対応、カスタマイズ性の高いUI。
- **リンク:** https://github.com/sweetalert2/sweetalert2

### MemoriLabs/Memori（16,800★・Python）※注目トピック（typescript, python, claude, hermes等）
- **概要:** AIエージェント向けの永続的メモリ（記憶）基盤。エージェントの実行や対話を構造化された状態として保存する。
- **注目理由:** エンタープライズ向けAIエージェントの「記憶」課題を解決する基盤ツールとして急上昇。
- **主な特徴:** マネージドクラウド/専用クラウド/VPC/オンプレの各環境に対応、既存データ基盤との統合が可能。
- **リンク:** https://github.com/MemoriLabs/Memori

---

## 📈 スター急増リポジトリ（risers・前週比）

前週（2026-09-11）からスターが大きく伸びたリポジトリです（開発者向け・1万★以上）。

| リポジトリ | 増加数 | 現在★ | 言語 |
|---|---|---|---|
| deepseek-ai/deepseek-harness | +8,611 | 228,964 | TypeScript |
| tt-a1i/archify | +8,331 | 66,617 | JavaScript |
| ayghri/i-have-adhd | +7,134 | 47,885 | Python |
| DietrichGebert/ponytail | +6,292 | 141,881 | JavaScript |
| mattpocock/skills | +5,551 | 265,114 | Shell |
| affaan-m/ECC | +5,404 | 261,736 | JavaScript |
| stablyai/orca | +5,140 | 71,728 | TypeScript |
| NationalSecurityAgency/ghidra | +4,023 | 78,838 | Java |
| Panniantong/Agent-Reach | +3,619 | 83,055 | Python |
| obra/superpowers | +3,231 | 288,436 | Shell |

**代表例の詳細:**

### deepseek-ai/deepseek-harness（+8,611★、228,964★・TypeScript）
- **概要:** DeepSeek発のAIエージェント基盤。「すべてはプラグイン」という設計思想。
- **注目理由:** 今週最大の伸び。DeepSeek系エージェントツールへの関心の高まりを示す。
- **主な特徴:** プラグイン構造による拡張性、cordisベースのアーキテクチャ。
- **リンク:** https://github.com/deepseek-ai/deepseek-harness

### DietrichGebert/ponytail（+6,292★、141,881★・JavaScript）
- **概要:** AIコーディングエージェントに「無駄なコードを書かない」思考を持たせるスキル。
- **注目理由:** YAGNI原則をAIエージェントに適用するというコンセプトが開発者から共感を集めている。
- **主な特徴:** Claude Code等のプラグインとして導入可能、シンプルさを重視した設計指針を提供。
- **リンク:** https://github.com/DietrichGebert/ponytail

### NationalSecurityAgency/ghidra（+4,023★、78,838★・Java）
- **概要:** NSA公開のソフトウェアリバースエンジニアリング（解析）フレームワーク。
- **注目理由:** セキュリティ・解析分野の定番ツールとして継続的に注目を集める。
- **主な特徴:** 逆アセンブラ機能、ソフトウェア解析に必要な機能を包括的に提供。
- **リンク:** https://github.com/NationalSecurityAgency/ghidra

---

## 🎯 注目トピックの動き（go / rust / typescript / python / nextjs / claude / hermes-agent）

スター1万未満でも注目枠として扱う対象を含め、優先トピックの主な動きです。

- **hermes-agent:** `NousResearch/hermes-agent`（246,827★）が継続的に高スターを維持。新規枠では`internet-court/internet-court-skill`（5,835★、rust/typescript/claude/openclaw/hermes-agent対応のAgent Skill）が注目。既存の`farion1231/cc-switch`（133,551★）もhermes-agent対応を明記し人気継続。
- **claude:** AIエージェント向けスキル・プラグイン系が引き続き活況。`tt-a1i/archify`（+8,331）、`ayghri/i-have-adhd`（+7,134）、`DietrichGebert/ponytail`（+6,292）、`affaan-m/ECC`（+5,404）が急伸。
- **python:** `donnemartin/system-design-primer`が新規掲載トップ。既存の`vinta/awesome-python`（321,480★）、`public-apis/public-apis`（481,374★）も高水準を維持。
- **typescript:** `firecrawl/firecrawl`（181,922★、+2,821）、`anomalyco/opencode`（208,384★）が引き続き高活性。
- **rust:** `sharkdp/fd`が新規掲載。既存の`openai/codex`（125,115★）、`rustdesk/rustdesk`（123,931★）も安定的な支持を継続。
- **go:** `alibaba/open-code-review`（36,395★）が新規掲載、`avelino/awesome-go`（184,636★）は定番として継続参照。
- **nextjs:** `leerob/next-mdx-blog`（7,569★、注目枠）、`SenteLabsAI/OpenExecutive`（4,976★、注目枠、FastAPI+Next.js構成のAI executiveエージェント）が新規登場。

---

## 注目枠（1万★未満・優先トピック該当）

スター基準未達ですが、優先トピックに該当するため注目枠として紹介します。

### leerob/next-mdx-blog（7,569★・TypeScript）
- **概要:** Next.js + MDXで構築されたブログテンプレート。
- **注目理由:** Next.js/TypeScriptコミュニティで実用的な出発点として参照が増加。
- **主な特徴:** Tailwind CSS、PostgreSQL連携、Vercelデプロイ想定。
- **リンク:** https://github.com/leerob/next-mdx-blog

### internet-court/internet-court-skill（5,835★・TypeScript）
- **概要:** エージェント間コマース（agent-to-agent commerce）のための信頼レイヤー。自然言語による委任・エスクロー・紛争解決を提供。
- **注目理由:** hermes-agent/openclaw/claude等、複数のAIエージェント基盤を横断対応するSkillとして注目。
- **主な特徴:** ERC-7710委任権限、x402決済連携、Claude Code Pluginとしても提供。
- **リンク:** https://github.com/internet-court/internet-court-skill

### SenteLabsAI/OpenExecutive（4,976★・Python）
- **概要:** 8名の専門AIエージェントが支える「AI経営幹部」システム。
- **注目理由:** マルチエージェント構成による業務代行というコンセプトの新規性。
- **主な特徴:** FastAPI + Next.js構成、Anthropic Claude活用、RAGベースの意思決定支援。
- **リンク:** https://github.com/SenteLabsAI/OpenExecutive

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
