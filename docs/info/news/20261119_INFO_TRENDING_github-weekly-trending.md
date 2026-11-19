作成日: 2026-11-19 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-11-12 → 2026-11-19）

GitHub 公式 REST Search API で集めたデータを、前週（2026-11-12）と比べた差分レポートです。掲載基準はスター 10,000 以上・開発者向け。優先トピック（go / rust / typescript / python / nextjs / claude / hermes-agent）は 1 万未満でも「注目枠」に載せています。（スター数は 2026-11-19 時点）

## 今週のポイント

- AI コーディングエージェント向け「スキル（エージェントに渡す手順書・拡張）」「ハーネス（エージェントを動かす土台）」系が引き続き急増。
- DeepSeek Harness（dsh）関連（本体とプラグイン）がまとめて伸びた。
- `NousResearch/hermes-agent`（hermes-agent トピック）は 26.5 万スターで優先トピック該当。

## 1. 前週比で伸びたリポジトリ（risers・上位）

### morluto/rea（+14,891 / 469,538★ / TypeScript）
- 概要: エージェントを使い、アプリの挙動からネイティブバイナリまであらゆるものをリバースエンジニアリング（解析）するツール。
- 注目理由: 今週の増加数が最大。Claude Code 向けスキルとして使える。
- 特徴: MCP（AI が外部ツールを呼ぶ共通規格）対応、CLI、複数言語の対象に対応。
- https://github.com/morluto/rea

### Ebony-Vinyl/dsh-our-free-model（+9,674 / 80,839★）
- 概要: dsh に入れるだけで、登録・API キー不要で DeepSeek V4.1 Flash や Kimi K3 などを無料で使えるとうたうプラグイン。
- 注目理由: 「無制限・無料」の訴求で急伸。ただし提供条件・安全性は利用前に要確認。
- https://github.com/Ebony-Vinyl/dsh-our-free-model

### pingdotgg/t3code（+8,121 / 66,120★ / TypeScript）
- 概要: Claude Code や Codex を、PC やスマホからまとめて操作するツール。
- 注目理由: エージェントのオーケストレーション（複数管理）需要の高まり。
- https://github.com/pingdotgg/t3code

### stablyai/orca（+6,398 / 129,618★ / TypeScript）【優先: typescript, claude, hermes-agent】
- 概要: 自分のサブスクで複数のコーディングエージェント（Claude Code、Codex 等）を並行運用。デスクトップ／モバイル／リモート対応。
- https://github.com/stablyai/orca

### affaan-m/ECC（+5,237 / 307,062★ / JavaScript）【優先: claude】
- 概要: エージェントの性能最適化システム。スキル・記憶・セキュリティ・調査重視の開発を提供。
- https://github.com/affaan-m/ECC

### mattpocock/skills（+5,206 / 327,963★ / Shell）
- 概要: 「現場のエンジニア向けスキル集」。作者の .agents ディレクトリ由来。
- https://github.com/mattpocock/skills

### DietrichGebert/ponytail（+5,052 / 194,678★ / JavaScript）【優先: claude】
- 概要: AI エージェントを「最も怠け者のシニア開発者」のように考えさせ、書かないコードを増やす方針のスキル。
- https://github.com/DietrichGebert/ponytail

### debpalash/VoiceStudio（+5,041 / 113,989★ / Python）【優先: python】
- 概要: 完全ローカルで動く ElevenLabs 代替。音声クローン・吹き替え・文字起こし・オーディオブック作成を 646 言語で。
- https://github.com/debpalash/VoiceStudio

### cloudflare/security-audit-skill（+4,784 / 75,708★ / JavaScript）
- 概要: 多段階のセキュリティ監査を行い、検証済みで機械可読な指摘を出すエージェント用スキル。
- https://github.com/cloudflare/security-audit-skill

### Leonxlnx/taste-skill（+4,742 / 118,796★ / JavaScript）【優先: claude】
- 概要: 汎用的な「AI っぽい」ページではなく、アートディレクション・参考画像・ブラウザ確認で見た目を整えるスキル。
- https://github.com/Leonxlnx/taste-skill

### pbakaus/impeccable（113,318★ / Rust 表記）【優先: rust】
- 概要: コーディングエージェント向けのデザイン語彙集。polish / critique / audit などで「AI 臭さ」を防ぐ。
- https://github.com/pbakaus/impeccable

### deepseek-ai/deepseek-harness（+4,462 / 284,124★ / TypeScript）【優先: typescript】
- 概要: 「すべてがプラグイン」を掲げる DeepSeek のエージェントハーネス（dsh）。
- https://github.com/deepseek-ai/deepseek-harness

### alibaba/open-code-review（+4,343 / 54,336★ / Go）【優先: go, claude】
- 概要: 決定的なパイプラインと LLM エージェントを組み合わせたコードレビューツール。行単位の指摘が可能。
- https://github.com/alibaba/open-code-review

### Nutlope/hallmark（+4,077 / 57,927★ / CSS）【優先: claude】
- 概要: Claude Code / Cursor / Codex 用の「AI スロップ（粗製乱造っぽいデザイン）防止」デザインスキル。
- https://github.com/Nutlope/hallmark

### anthropics/skills（+4,027 / 197,586★ / Python）【優先: python, claude】
- 概要: Agent Skills の公式公開リポジトリ。
- https://github.com/anthropics/skills

## 2. 新規ランクイン（newcomers・今週初めて対象プールに入ったもの）

先週より集計範囲に入った既存の人気リポジトリです（新規作成とは限りません）。

- Anduin2017/HowToCook（104,131★ / 言語なし）: プログラマー向け家庭料理ガイド。https://github.com/Anduin2017/HowToCook
- tonsky/FiraCode（82,209★ / Clojure）: リガチャ付きプログラミング用等幅フォント。https://github.com/tonsky/FiraCode
- doocs/advanced-java（79,184★ / Java）: Java バックエンド面接・上級知識の解説集。https://github.com/doocs/advanced-java
- tw93/Mole（75,595★ / Shell）: Mac／Windows 向けオープンソースのクリーナー（不要ファイル掃除）。https://github.com/tw93/Mole
- Fission-AI/OpenSpec（75,259★ / TypeScript）: AI コーディング向けスペック駆動開発（SDD）。https://github.com/Fission-AI/OpenSpec
- toeverything/AFFiNE（74,933★ / TypeScript）: プライバシー重視の次世代ナレッジベース（Notion/Miro 代替）。https://github.com/toeverything/AFFiNE
- josephmisiti/awesome-machine-learning（74,851★ / Python）: 機械学習ライブラリの厳選リスト。https://github.com/josephmisiti/awesome-machine-learning
- danielmiessler/SecLists（74,840★ / PHP）: セキュリティテスト用のユーザー名・パスワード・ペイロード等のリスト集。https://github.com/danielmiessler/SecLists
- aaif-goose/goose（56,791★ / Rust）【rust】: 拡張可能なオープンソース AI エージェント。インストール・実行・編集・テストまで任意の LLM で。https://github.com/aaif-goose/goose
- jesseduffield/lazydocker（53,383★ / Go）【go】: Docker 管理を楽にするターミナル UI。https://github.com/jesseduffield/lazydocker
- ifixai-ai/iFixAi（46,340★ / Python）【python】: AI エージェントが意図どおり動いているかを 120 秒以内で監査。https://github.com/ifixai-ai/iFixAi
- yetone/magpie（39,031★ / Go）【go, claude】: メニューバーからエージェントごとのモデル（例: Codex を DeepSeek で）を切り替え。https://github.com/yetone/magpie
- storytold/craft-anything（38,141★ / Rust）【rust】: ソフトウェアの仕組みを理解し、自分用に作り直す。https://github.com/storytold/craft-anything
- anthropics/knowledge-work-plugins（36,563★ / Python）【python, claude】: Claude Cowork 向けプラグイン集。https://github.com/anthropics/knowledge-work-plugins
- h4ckf0r0day/obscura（36,528★ / Rust）【rust】: AI エージェント／スクレイピング向けヘッドレスブラウザ。https://github.com/h4ckf0r0day/obscura

## 3. 優先トピック注目枠（スター 1 万未満）

- ForeactLabs/OpenExecutive（5,834★ / Python）【typescript, python, nextjs, claude】: 8 人の専門エージェントを束ねる仮想エグゼクティブチーム（FastAPI + Next.js）。https://github.com/ForeactLabs/OpenExecutive
- vivek9patel/vivek9patel.github.io（4,322★ / JavaScript）【nextjs】: Next.js と Tailwind で作った Ubuntu 20.04 風の Web シミュレーション。https://github.com/vivek9patel/vivek9patel.github.io
- theodorusclarence/ts-nextjs-tailwind-starter（3,403★ / TypeScript）【typescript, nextjs】: Next.js + Tailwind CSS + TypeScript のスターター。https://github.com/theodorusclarence/ts-nextjs-tailwind-starter

## 4. 優先トピックの動き（主要な常連）

- hermes-agent: NousResearch/hermes-agent 264,694★（Python）。stablyai/orca も hermes-agent トピックを付与。
- claude: anthropics/skills、addyosmani/agent-skills（119,115★）、claude-mem（118,370★）、cc-switch（155,777★）など、スキル／補助ツールが多数。
- python: yt-dlp（209,144★）、markitdown（196,947★）、Scrapling（104,359★）等。
- typescript: firecrawl（203,812★）、hyperframes（86,898★）、OmniRoute（88,853★）等。
- rust / go: goose、cc-switch（Rust）、magpie、open-code-review（Go）が目立つ。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
