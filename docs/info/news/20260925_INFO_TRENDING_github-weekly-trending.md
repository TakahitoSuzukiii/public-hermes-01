作成日: 2026-09-25 / STATUS: INFO / TOPIC: TRENDING

# GitHub週次トレンド（2026-09-25）

GitHub公式REST Search APIから、スター数10,000以上かつ開発者向けのリポジトリを対象に、前週（2026-09-18時点）との比較でスターが伸びたリポジトリ（risers）と、今回新たに掲載条件を満たしたリポジトリ（newcomers）をまとめました。加えて、注目トピック（go / rust / typescript / python / nextjs / claude / hermes-agent）関連の動きも別枠で紹介します。

> 対象プール: 450件 / 基準スター: 10,000以上 / 前回集計日: 2026-09-18

---

## 🆕 新規掲載（newcomers）

今回初めて掲載条件（スター1万以上）を満たしたリポジトリです。

### OpenCut-app/OpenCut（90,658★・TypeScript）
- **概要:** オープンソース版のCapCut（動画編集アプリ）代替ツール。
- **注目理由:** 商用動画編集アプリの無料オルタナティブとして一気に注目度が上昇。
- **主な特徴:** ブラウザ完結の動画編集UI、OSSならではのカスタマイズ性。
- **リンク:** https://github.com/OpenCut-app/OpenCut

### janhq/jan（44,650★・Rust）
- **概要:** ChatGPTのオープンソース代替。完全オフラインでPC上で動作する。
- **注目理由:** ローカルLLM実行環境への関心の高まりを背景に新規掲載入り。
- **主な特徴:** llama.cpp連携、Tauri製デスクトップアプリ、セルフホスト志向。
- **リンク:** https://github.com/janhq/jan

### can1357/oh-my-pi（33,273★・TypeScript）※注目トピック（typescript, rust, claude）
- **概要:** IDEと一体化したコーディングエージェント。Stencil Labsが開発。
- **注目理由:** Claude/OpenAI等マルチプロバイダー対応のターミナル型コーディングエージェントとして話題化。
- **主な特徴:** MCP対応、TUI（ターミナルUI）、Bunベースの高速実行。
- **リンク:** https://github.com/can1357/oh-my-pi

### vercel-labs/skills（32,463★・TypeScript）※注目トピック（typescript）
- **概要:** Vercel製のオープンなエージェントスキル管理ツール。`npx skills`で利用可能。
- **注目理由:** Vercel公式によるAIエージェント向けスキル配布基盤として急速に浸透。
- **主な特徴:** npx一発導入、エージェントスキルの共有・再利用を簡素化。
- **リンク:** https://github.com/vercel-labs/skills

### primefaces/primeng（12,485★・TypeScript）※注目トピック（typescript, angular）
- **概要:** Angular向けの最も網羅的なUIコンポーネントライブラリ。
- **注目理由:** 長年の実績を持つAngular UIライブラリとして今回新規掲載入り。
- **主な特徴:** チャート・データグリッド・テーブル等、MITライセンスの豊富なコンポーネント群。
- **リンク:** https://github.com/primefaces/primeng

### EKKOLearnAI/ekko-studio（11,188★・TypeScript）※注目トピック（typescript, hermes-agent）
- **概要:** マルチエージェントのチャット・コーディング・ビジュアルワークフローに対応するローカルファーストAIワークスペース。デスクトップ／Web両対応。
- **注目理由:** Hermes Agent関連トピックを冠する新規プロジェクトとして注目。
- **主な特徴:** Vue3製UI、マルチモデル・マルチプラットフォーム対応、自己ホスト可能。
- **リンク:** https://github.com/EKKOLearnAI/ekko-studio

---

## 📈 スター急増リポジトリ（risers・前週比）

前週（2026-09-18）からスターが大きく伸びたリポジトリです（開発者向け・1万★以上、対象426件中の上位）。

| リポジトリ | 増加数 | 現在★ | 言語 |
|---|---|---|---|
| deepseek-ai/deepseek-harness | +6,887 | 235,851 | TypeScript |
| stablyai/orca | +6,372 | 78,100 | TypeScript |
| affaan-m/ECC | +5,584 | 267,320 | JavaScript |
| bilawalsidhu/gods-eye-view | +5,302 | 42,869 | JavaScript |
| tt-a1i/archify | +4,954 | 71,571 | JavaScript |
| alibaba/open-code-review | +4,806 | 41,201 | Go |
| mattpocock/skills | +4,421 | 269,535 | Shell |
| DietrichGebert/ponytail | +3,974 | 145,855 | JavaScript |
| ayghri/i-have-adhd | +3,256 | 51,141 | Python |
| farion1231/cc-switch | +3,251 | 136,802 | Rust |
| obra/superpowers | +3,086 | 291,522 | Shell |
| paperclipai/paperclip | +3,044 | 84,036 | TypeScript |
| addyosmani/agent-skills | +2,781 | 99,011 | JavaScript |
| firecrawl/firecrawl | +2,672 | 184,594 | TypeScript |
| debpalash/VoiceStudio | +2,650 | 35,407 | Python |

**代表例の詳細:**

### deepseek-ai/deepseek-harness（+6,887★、235,851★・TypeScript）
- **概要:** DeepSeek発のAIエージェント基盤。「すべてはプラグイン」という設計思想。
- **注目理由:** 2週連続で最大級の伸び。DeepSeek系エージェントツールへの関心が継続的に拡大。
- **主な特徴:** プラグイン構造による拡張性、cordisベースのアーキテクチャ。
- **リンク:** https://github.com/deepseek-ai/deepseek-harness

### stablyai/orca（+6,372★、78,100★・TypeScript）
- **概要:** 並列コーディングエージェント群を扱うためのADE（Agent Development Environment）。
- **注目理由:** 自前サブスクリプションで任意のコーディングエージェントを実行できる柔軟性がYC系スタートアップ発として注目。
- **主な特徴:** デスクトップ・モバイル・リモートランタイム対応、Claude Code/Codex/Cursor Agent等と連携。
- **リンク:** https://github.com/stablyai/orca

### affaan-m/ECC（+5,584★、267,320★・JavaScript）
- **概要:** Claude Code・Codex・Opencode・Cursor等向けのエージェントハーネス性能最適化システム。
- **注目理由:** スキル・記憶・セキュリティを統合した「研究優先」開発フレームワークとして支持拡大。
- **主な特徴:** マルチエージェント基盤横断対応、開発者生産性向上ツール群。
- **リンク:** https://github.com/affaan-m/ECC

### bilawalsidhu/gods-eye-view（+5,302★、42,869★・JavaScript）
- **概要:** ブラウザで動くスパイ衛星シミュレーター。実データを使用した公開情報インテリジェンス（OSINT）デモ。
- **注目理由:** 先週の新規掲載に続き、今週も引き続き大きく伸びている話題プロジェクト。
- **主な特徴:** フォトリアルな3Dグローブ、フライト追跡・衛星追跡データの統合表示。
- **リンク:** https://github.com/bilawalsidhu/gods-eye-view

### alibaba/open-code-review（+4,806★、41,201★・Go）
- **概要:** アリババ発のコードレビュー支援ツール。ルールベース処理とLLMエージェントを組み合わせるハイブリッド構成。
- **注目理由:** 先週の新規掲載に続き、大規模運用実績のあるコードレビュー自動化ツールとして支持継続。
- **主な特徴:** 行単位の精密コメント、多言語ルールセット（NPE/スレッド安全性/XSS/SQLインジェクション等）、OpenAI・Anthropic互換。
- **リンク:** https://github.com/alibaba/open-code-review

---

## 🎯 注目トピックの動き（go / rust / typescript / python / nextjs / claude / hermes-agent）

スター1万未満でも注目枠として扱う対象を含め、優先トピックの主な動きです。

- **hermes-agent:** `NousResearch/hermes-agent`（248,902★）が高水準を維持しつつ着実に増加。新規枠では`EKKOLearnAI/ekko-studio`（11,188★）、注目枠では`spinabot/brigade`（6,126★、AIエージェントランタイム）が新規登場。`farion1231/cc-switch`（136,802★、+3,251）もhermes-agent対応を明記し引き続き急伸。
- **claude:** AIエージェント向けスキル・プラグイン系が今週も活況。`stablyai/orca`（+6,372）、`affaan-m/ECC`（+5,584）、`tt-a1i/archify`（+4,954）、`alibaba/open-code-review`（+4,806）が急伸。
- **python:** `ayghri/i-have-adhd`（51,141★、+3,256）、`debpalash/VoiceStudio`（35,407★、+2,650）が伸長。既存の`anthropics/financial-services`（37,504★）、`public-apis/public-apis`（483,131★）も高水準を維持。
- **typescript:** 新規掲載が特に多い週。`OpenCut-app/OpenCut`（90,658★）、`can1357/oh-my-pi`（33,273★）、`vercel-labs/skills`（32,463★）が新規登場、`firecrawl/firecrawl`（184,594★、+2,672）も継続的に伸長。
- **rust:** `janhq/jan`（44,650★）が新規掲載トップ。注目枠では`ipetkov/crane`（1,466★、Nix向けCargoビルドライブラリ）が登場。既存の`farion1231/cc-switch`（136,802★）も高い伸びを維持。
- **go:** `alibaba/open-code-review`（41,201★、+4,806）が引き続き急伸中。
- **nextjs:** 注目枠で`vvo/iron-session`（4,144★、Next.js向けセッション管理ライブラリ）、`nandorojo/solito`（4,095★、React Native+Next.js統合）が新規登場。

---

## 注目枠（1万★未満・優先トピック該当）

スター基準未達ですが、優先トピックに該当するため注目枠として紹介します。

### spinabot/brigade（6,126★・TypeScript）
- **概要:** 「あなた専用のインテリジェンス」をエンタープライズ品質で構築するAIエージェントランタイム。
- **注目理由:** openclaw/hermes-agent双方に対応するマルチエージェント基盤として新規登場。
- **主な特徴:** 自律エージェント運用、複数エージェント連携（agent crew）機能。
- **リンク:** https://github.com/spinabot/brigade

### vvo/iron-session（4,144★・TypeScript）
- **概要:** Next.jsをはじめ各種JavaScriptフレームワーク向けの、安全でステートレスなCookieベースセッションライブラリ。
- **注目理由:** Next.jsコミュニティで実用的な認証基盤として参照が増加。
- **主な特徴:** サーバーレス対応、Express.js等とも組み合わせ可能。
- **リンク:** https://github.com/vvo/iron-session

### nandorojo/solito（4,095★・TypeScript）
- **概要:** React NativeとNext.jsを統合するためのライブラリ。
- **注目理由:** クロスプラットフォーム開発（Web+モバイル）の実践的ソリューションとして継続参照。
- **主な特徴:** 単一コードベースでWeb/モバイルの両方に対応するルーティング統合。
- **リンク:** https://github.com/nandorojo/solito

### hercules-ci/flake-parts（1,477★・Nix）
- **概要:** Nix Flakesをモジュールシステムでシンプルにするツール。
- **注目理由:** Nixエコシステムの定番モジュール化ツールとして新規掲載。
- **主な特徴:** モジュール分割による設定の見通し向上、Flakeの再利用性向上。
- **リンク:** https://github.com/hercules-ci/flake-parts

### ipetkov/crane（1,466★・Nix）
- **概要:** Cargoプロジェクトのビルドに使うNixライブラリ。インクリメンタルなアーティファクトキャッシュにより二重ビルドを回避。
- **注目理由:** Rust+Nix開発環境における効率化ツールとして新規掲載。
- **主な特徴:** ビルドキャッシュの自動管理、Rust/Nix両コミュニティで利用実績あり。
- **リンク:** https://github.com/ipetkov/crane

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
