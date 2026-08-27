# GitHub週次トレンド（2026-08-14）— mattpocock/skills伸び幅拡大、msitarzewski/agency-agentsとstablyai/orcaも急伸

作成日: 2026-08-14 / STATUS: INFO / TOPIC: TRENDING

> このレポートは GitHub 公式 REST Search API のみを使って取得したデータをもとに作成しています。掲載基準は「スター数10,000以上」の開発者向けリポジトリです。ただし優先トピック（go, rust, typescript, python, nextjs, claude, hermes-agent 等）は注目度が高いため、1万スター未満でも別枠で紹介します。前回スナップショット（2026-08-09）との差分がベースで、`isBaseline` は `false` のため、通常どおり増加分（前週比スター増）と新規登場を中心にまとめています。

## 今週のサマリー

- 追跡プール（GitHubスター1万以上＋優先トピック）: 446件
- 新規登場（newcomers）: 16件（うち1万スター以上13件、優先トピック枠3件）
- 前週比スター増（risers）: 412件中、上位15件を掲載
- 優先トピック該当（priorityHits）: 383件中、上位を紹介

---

## 🚀 前週比スター増（Risers）トップ10

今週も「AIコーディングエージェント向けスキル集」の勢いが継続。加えてAIゲートウェイ、Webスクレイピング基盤など、エージェント運用の周辺インフラ系の伸びも目立ちます。

### 1. mattpocock/skills
- **概要:** 実務エンジニア向けの「スキル集」。作者の `.agents` ディレクトリから直接引っ張ってきたコレクション。
- **注目理由:** 週間+7,130スターと今週最大の伸び。先週に続き首位をキープし、伸び幅も拡大しています。
- **主な特徴:** Claude Code など各種コーディングエージェント向けにすぐ使える実践的スキル集。
- **スター数:** 217,305
- **主要言語:** Shell
- **リンク:** https://github.com/mattpocock/skills

### 2. msitarzewski/agency-agents
- **概要:** フロントエンド専門家からコミュニティ運用まで、役割ごとに特化した「AIエージェント軍団」一式。
- **注目理由:** 週間+5,650スター。個性・プロセス・成果物が定義済みの専門エージェント群という切り口が引き続き支持されています。
- **主な特徴:** 役割別プロンプト設計済みエージェントのコレクション。
- **スター数:** 145,451
- **主要言語:** Shell
- **リンク:** https://github.com/msitarzewski/agency-agents

### 3. stablyai/orca
- **概要:** 複数のコーディングエージェントを並列運用するための ADE（Agent Development Environment）。デスクトップ・モバイル・VPSで動作。
- **注目理由:** 週間+5,183スター。「自分のサブスクリプションでどのエージェントも動かせる」設計が引き続き伸びを牽引。
- **主な特徴:** worktrees対応、Claude Code / Codex / OpenCode などをオーケストレーション。
- **スター数:** 45,493
- **主要言語:** TypeScript
- **リンク:** https://github.com/stablyai/orca

### 4. earendil-works/pi
- **概要:** AIエージェント向けツールキット。統一LLM API、エージェントループ、TUI、コーディングエージェントCLIを提供。
- **注目理由:** 週間+4,653スター。統一APIによる抽象化がマルチエージェント開発者に響いています。
- **主な特徴:** LLM API・エージェントループ・TUI・CLIを一体化した基盤ツール。
- **スター数:** 90,331
- **主要言語:** TypeScript
- **リンク:** https://github.com/earendil-works/pi

### 5. diegosouzapw/OmniRoute
- **概要:** 無料で使えるMIT ライセンスのAIゲートウェイ。1エンドポイントで330以上のプロバイダー（90以上が無料）、1200以上のモデルに接続可能。
- **注目理由:** 週間+4,243スター。Claude Code / Codex / Cursor / OpenCode / Cline / Copilot など主要コーディングツールに対応し、トークン節約機能も評価されています。
- **主な特徴:** クォータ検知による自動フォールバック、MCP/A2A対応、デスクトップ・PWA両対応。
- **スター数:** 47,792
- **主要言語:** TypeScript
- **リンク:** https://github.com/diegosouzapw/OmniRoute

### 6. firecrawl/firecrawl
- **概要:** Web全体を対象にした検索・スクレイピング・データ抽出用のコンテキストAPI。
- **注目理由:** 週間+3,830スター。AIエージェントのWebアクセス基盤としてさらに定番化が進んでいます。
- **主な特徴:** HTMLからMarkdownへの変換、大規模スクレイピング対応。
- **スター数:** 167,321
- **主要言語:** TypeScript
- **リンク:** https://github.com/firecrawl/firecrawl

### 7. DietrichGebert/ponytail
- **概要:** 「部屋で一番怠け者のシニアエンジニアのように考える」AIエージェント向けスキル。書かないコードが一番良いコード、という思想。
- **注目理由:** 週間+3,782スター。YAGNI原則をAIエージェントに徹底させるコンセプトが引き続き人気。
- **主な特徴:** Claude Code プラグイン対応、Cursor rules対応。
- **スター数:** 102,644
- **主要言語:** JavaScript
- **リンク:** https://github.com/DietrichGebert/ponytail

### 8. NousResearch/hermes-agent
- **概要:** 「成長し続けるエージェント」がコンセプトのAIエージェント。
- **注目理由:** 週間+2,944スター。優先トピック（python / claude / hermes-agent）に該当し、着実にスターを伸ばし続けています。
- **主な特徴:** Claude / Codex 対応、Nous Research発のオープンソースエージェント基盤。
- **スター数:** 230,526
- **主要言語:** Python
- **リンク:** https://github.com/NousResearch/hermes-agent

### 9. hugohe3/ppt-master
- **概要:** ドキュメントやトピックからネイティブなPowerPointを自動生成するAIツール。
- **注目理由:** 週間+2,833スター。ネイティブ図形・アニメーション・データ連動グラフ・音声ナレーションまで対応する完成度の高さが支持されています。
- **主な特徴:** 既存.pptxテンプレートの活用にも対応。
- **スター数:** 46,805
- **主要言語:** Python
- **リンク:** https://github.com/hugohe3/ppt-master

### 10. public-apis/public-apis
- **概要:** 無料で使えるAPIのコレクションリスト。
- **注目理由:** 週間+2,744スター。定番リストとして継続的に参照・拡散されています。
- **主な特徴:** カテゴリ別に整理された大規模なAPIカタログ。
- **スター数:** 457,869
- **主要言語:** Python
- **リンク:** https://github.com/public-apis/public-apis

---

## 🆕 新規登場（Newcomers）

今回の追跡プールに新しく入ってきたリポジトリのうち、掲載基準（1万スター以上）を満たすものです。

### DigitalPlatDev/FreeDomain
- **概要:** 誰でも使える無料ドメイン登録＆DNS学習リソース。
- **注目理由:** 実用的な無料インフラリソースとして幅広く参照されています。
- **スター数:** 192,830 / **主要言語:** Markdown
- **リンク:** https://github.com/DigitalPlatDev/FreeDomain

### Genymobile/scrcpy
- **概要:** Androidデバイスの画面表示・操作をPCから行うツール。
- **注目理由:** モバイル開発・検証の定番ツールとして長年の実績。
- **スター数:** 147,620 / **主要言語:** C
- **リンク:** https://github.com/Genymobile/scrcpy

### Anduin2017/HowToCook
- **概要:** プログラマー向けの「家で料理する」ガイド。
- **注目理由:** エンジニアコミュニティで人気の実用系ドキュメントプロジェクト。
- **スター数:** 101,798 / **主要言語:** なし（Markdown中心）
- **リンク:** https://github.com/Anduin2017/HowToCook

### deepseek-ai/deepseek-harness
- **概要:** 「すべてがプラグイン」をコンセプトにしたDeepSeekのエージェントハーネス。
- **注目理由:** 優先トピック「typescript」該当。大手AI企業発のエージェント基盤として注目。
- **スター数:** 92,655 / **主要言語:** TypeScript
- **リンク:** https://github.com/deepseek-ai/deepseek-harness

### ChatGPTNextWeb/NextChat
- **概要:** 軽量・高速なAIアシスタントクライアント（Web / iOS / macOS / Android / Linux / Windows対応）。
- **注目理由:** 優先トピック「typescript / nextjs / claude」該当。マルチプラットフォーム対応のAIチャットUIとして定番。
- **スター数:** 88,609 / **主要言語:** TypeScript
- **リンク:** https://github.com/ChatGPTNextWeb/NextChat

### tensorflow/models
- **概要:** TensorFlowで構築されたモデル・実装例集。
- **注目理由:** 優先トピック「python」該当。機械学習の定番リファレンス実装群。
- **スター数:** 77,653 / **主要言語:** Python
- **リンク:** https://github.com/tensorflow/models

### PKUFlyingPig/cs-self-learning
- **概要:** 「計算機自学指南」— コンピュータサイエンス独学ガイド。
- **注目理由:** 体系的な自学教材として中国語圏を中心に人気。
- **スター数:** 74,939 / **主要言語:** HTML
- **リンク:** https://github.com/PKUFlyingPig/cs-self-learning

### thedaviddias/Front-End-Checklist
- **概要:** モダンなWeb開発向けの必須チェックリスト（人間・AIエージェント両対応）。
- **注目理由:** フロントエンド品質担保の定番チェックリストとして継続的に参照。
- **スター数:** 73,530 / **主要言語:** MDX
- **リンク:** https://github.com/thedaviddias/Front-End-Checklist

### Asabeneh/30-Days-Of-Python
- **概要:** 30日間でPythonを学ぶステップバイステップ教材。
- **注目理由:** 優先トピック「python」該当。初学者向け教材の定番として根強い人気。
- **スター数:** 70,936 / **主要言語:** Python
- **リンク:** https://github.com/Asabeneh/30-Days-Of-Python

### emilkowalski/skills
- **概要:** デザイナー・エンジニア向けのスキル集。
- **注目理由:** AIエージェント向けスキル集トレンドの一環として急浮上。
- **スター数:** 29,201 / **主要言語:** Markdown
- **リンク:** https://github.com/emilkowalski/skills

### titanwings/colleague-skill
- **概要:** 「別れ」を「スキル」として継承する、AIエージェント向けの知識蒸留ツール。
- **注目理由:** 優先トピック「python / claude / openclaw / hermes-agent」の4つに該当。ユニークなコンセプトのスキル生成ツール。
- **スター数:** 21,974 / **主要言語:** Python
- **リンク:** https://github.com/titanwings/colleague-skill

### cft0808/edict
- **概要:** 「三省六部制」をモチーフにしたOpenClawマルチエージェント・オーケストレーションシステム。
- **注目理由:** 優先トピック「python / claude / openclaw」該当。9体の専門AIエージェント＋リアルタイムダッシュボードという構成が特徴的。
- **スター数:** 16,373 / **主要言語:** Python
- **リンク:** https://github.com/cft0808/edict

### vercel/commerce
- **概要:** Next.js製のEコマーステンプレート。
- **注目理由:** 優先トピック「typescript / nextjs」該当。Vercel公式のEコマース実装リファレンス。
- **スター数:** 14,209 / **主要言語:** TypeScript
- **リンク:** https://github.com/vercel/commerce

### 🌟 優先トピック枠（1万スター未満だが注目）

以下3件は掲載基準（1万スター以上）には届きませんが、優先トピック「typescript」「nextjs」に該当するため注目枠として紹介します。

**transitive-bullshit/nextjs-notion-starter-kit**
- **概要:** Next.jsとVercelでNotion連携サイトを数分でデプロイできるスターターキット。
- **注目理由:** Notionをそのままブログ・ポートフォリオ化する実用性の高さ。
- **スター数:** 7,028 / **主要言語:** TypeScript
- **リンク:** https://github.com/transitive-bullshit/nextjs-notion-starter-kit

**ethanniser/NextFaster**
- **概要:** Next.jsを使った高パフォーマンスなEコマーステンプレート。
- **注目理由:** パフォーマンス最適化のリファレンス実装として参考価値が高い。
- **スター数:** 4,879 / **主要言語:** TypeScript
- **リンク:** https://github.com/ethanniser/NextFaster

**saltyshiomix/nextron**
- **概要:** Next.js + Electronを組み合わせたデスクトップアプリ開発フレームワーク。
- **注目理由:** Web技術でデスクトップアプリを作る定番構成の一つ。
- **スター数:** 4,427 / **主要言語:** TypeScript
- **リンク:** https://github.com/saltyshiomix/nextron

---

## 🎯 優先トピックの動き（go / rust / typescript / python / nextjs / claude / hermes-agent 他）

優先トピックに該当するリポジトリの中から、特に動きが大きいものをピックアップします（いずれも1万スター以上）。

- **NousResearch/hermes-agent**（230,526★、+2,944） — hermes-agentトピック該当。前週に続き伸びを継続中で、Python製AIエージェント基盤として存在感を強めています。
  https://github.com/NousResearch/hermes-agent
- **anomalyco/opencode**（197,445★、TypeScript） — オープンソースのコーディングエージェント。優先トピック「typescript」該当で、着実な成長が続いています。
  https://github.com/anomalyco/opencode
- **anthropics/skills**（169,379★、Python） — Anthropic公式のAgent Skills公開リポジトリ。優先トピック「python / claude」該当、エージェントスキルの標準実装として参照価値が高いです。
  https://github.com/anthropics/skills
- **github/spec-kit**（128,216★、Python） — Spec-Driven Development（仕様駆動開発）を始めるためのGitHub公式ツールキット。優先トピック「python」該当。
  https://github.com/github/spec-kit
- **paperclipai/paperclip**（78,122★、TypeScript） — 職場でのAIエージェント管理に使われるOSSアプリ。優先トピック「typescript」該当で、エージェント運用管理系ツールとして急伸。
  https://github.com/paperclipai/paperclip
- **farion1231/cc-switch**（127,258★、Rust/TypeScript） — Claude Code / Codex / OpenCode / OpenClaw / Hermes Agent を横断管理できるデスクトップアプリ。rust・typescript・claude・openclaw・hermes-agentと複数の優先トピックに該当する注目株です。
  https://github.com/farion1231/cc-switch
- **JuliusBrussee/caveman**（98,178★、Go） — トークン消費を65%削減するClaude Codeスキル。優先トピック「go / claude」該当のユニークな最適化アプローチ。
  https://github.com/JuliusBrussee/caveman
- **infiniflow/ragflow**（88,327★、Go） — RAGとエージェント機能を融合したRAGエンジン。優先トピック「go」該当。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
