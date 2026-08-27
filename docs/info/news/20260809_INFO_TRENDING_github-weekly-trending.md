# GitHub週次トレンド（2026-08-09）— mattpocock/skills首位継続、diegosouzapw/OmniRouteのAIゲートウェイが急伸

作成日: 2026-08-09 / STATUS: INFO / TOPIC: TRENDING

> このレポートは GitHub 公式 REST Search API のみを使って取得したデータをもとに作成しています。掲載基準は「スター数10,000以上」の開発者向けリポジトリです。ただし優先トピック（go, rust, typescript, python, nextjs, claude, hermes-agent 等）は注目度が高いため、1万スター未満でも別枠で紹介します。前回スナップショット（2026-08-07）との差分がベースで、`isBaseline` は `false` のため、通常どおり増加分（前週比スター増）と新規登場を中心にまとめています。

## 今週のサマリー

- 追跡プール（GitHubスター1万以上＋優先トピック）: 446件
- 新規登場（newcomers）: 6件（うち1万スター以上4件、優先トピック枠2件）
- 前週比スター増（risers）: 411件中、上位15件を掲載
- 優先トピック該当（priorityHits）: 385件中、上位を紹介

---

## 🚀 前週比スター増（Risers）トップ10

AIエージェント・コーディング支援系の伸びが目立つ週でした。特に「AIエージェント向けスキル集」「マルチプロバイダーAIゲートウェイ」系の勢いが顕著です。

### 1. mattpocock/skills
- **概要:** 実務エンジニア向けの「スキル集」。作者の `.agents` ディレクトリから直接引っ張ってきたコレクション。
- **注目理由:** 週間+1,512スターと今週最大の伸び。AIコーディングエージェント向けスキル共有の需要の高さがうかがえます。
- **主な特徴:** Claude Code など各種コーディングエージェント向けにすぐ使える実践的スキル集。
- **スター数:** 210,175
- **主要言語:** Shell
- **リンク:** https://github.com/mattpocock/skills

### 2. diegosouzapw/OmniRoute
- **概要:** 無料で使えるMIT ライセンスのAIゲートウェイ。1エンドポイントで290以上のプロバイダー（90以上が無料）、500以上のモデルに接続可能。
- **注目理由:** 週間+1,087スター。Claude Code / Codex / Cursor / OpenCode / Cline / Copilot など主要コーディングツールに対応し、トークン節約機能（15〜95%削減）も備える点が支持されています。
- **主な特徴:** クォータ検知による自動フォールバック、MCP/A2A対応、デスクトップ・PWA両対応。
- **スター数:** 43,549
- **主要言語:** TypeScript
- **リンク:** https://github.com/diegosouzapw/OmniRoute

### 3. addyosmani/agent-skills
- **概要:** AIコーディングエージェント向けの「本番品質」エンジニアリングスキル集。
- **注目理由:** 週間+852スター。Google Chrome チームで著名な addyosmani 氏によるリポジトリで信頼性が高い。
- **主な特徴:** Claude Code / Codex / Cursor / Antigravity 対応。
- **スター数:** 84,655
- **主要言語:** JavaScript
- **リンク:** https://github.com/addyosmani/agent-skills

### 4. stablyai/orca
- **概要:** 複数のコーディングエージェントを並列運用するための ADE（Agent Development Environment）。デスクトップ・モバイル・VPSで動作。
- **注目理由:** 週間+723スター。「自分のサブスクリプションでどのエージェントも動かせる」設計が支持を集めています。
- **主な特徴:** worktrees対応、Claude Code / Codex / OpenCode などをオーケストレーション。
- **スター数:** 40,310
- **主要言語:** TypeScript
- **リンク:** https://github.com/stablyai/orca

### 5. msitarzewski/agency-agents
- **概要:** フロントエンド専門家からコミュニティ運用まで、役割ごとに特化した「AIエージェント軍団」一式。
- **注目理由:** 週間+709スター。個性・プロセス・成果物が定義済みの専門エージェント群という切り口がユニーク。
- **主な特徴:** 役割別プロンプト設計済みエージェントのコレクション。
- **スター数:** 139,801
- **主要言語:** Shell
- **リンク:** https://github.com/msitarzewski/agency-agents

### 6. obra/superpowers
- **概要:** エージェント向けスキルフレームワーク＋ソフトウェア開発方法論。
- **注目理由:** 週間+683スター。総スター26万超えで継続的に人気の「開発手法そのものをスキル化する」アプローチ。
- **主な特徴:** サブエージェント駆動開発（subagent-driven development）を提唱。
- **スター数:** 269,375
- **主要言語:** Shell
- **リンク:** https://github.com/obra/superpowers

### 7. Panniantong/Agent-Reach
- **概要:** AIエージェントにインターネット全体を「見る目」を与えるツール。Twitter/Reddit/YouTube/GitHub/Bilibili/小紅書などを1つのCLIで検索・読み取り可能、API課金なし。
- **注目理由:** 週間+683スター。無料でSNS横断リサーチができる点が開発者に刺さっています。
- **主な特徴:** MCP対応、各種スクレイパーを統合。
- **スター数:** 68,989
- **主要言語:** Python
- **リンク:** https://github.com/Panniantong/Agent-Reach

### 8. DietrichGebert/ponytail
- **概要:** 「部屋で一番怠け者のシニアエンジニアのように考える」AIエージェント向けスキル。書かないコードが一番良いコード、という思想。
- **注目理由:** 週間+658スター。YAGNI原則をAIエージェントに徹底させるユニークなコンセプト。
- **主な特徴:** Claude Code プラグイン対応、Cursor rules対応。
- **スター数:** 98,862
- **主要言語:** JavaScript
- **リンク:** https://github.com/DietrichGebert/ponytail

### 9. firecrawl/firecrawl
- **概要:** Web全体を対象にした検索・スクレイピング・データ抽出用のコンテキストAPI。
- **注目理由:** 週間+635スター。AIエージェントのWebアクセス基盤として定番化しつつあります。
- **主な特徴:** HTMLからMarkdownへの変換、大規模スクレイピング対応。
- **スター数:** 163,491
- **主要言語:** TypeScript
- **リンク:** https://github.com/firecrawl/firecrawl

### 10. rasbt/LLMs-from-scratch
- **概要:** PyTorchでChatGPTライクなLLMをゼロから実装する教育コンテンツ。
- **注目理由:** 週間+625スター。LLMの内部構造を学びたい開発者から根強い支持。
- **主な特徴:** 事前学習・ファインチューニング・トークナイザーまで一貫してステップバイステップ解説。
- **スター数:** 101,518
- **主要言語:** Jupyter Notebook
- **リンク:** https://github.com/rasbt/LLMs-from-scratch

---

## 🆕 新規登場（Newcomers）

今回の追跡プールに新しく入ってきたリポジトリです。

### realworld-apps/realworld
- **概要:** 「あらゆるデモアプリの母」と呼ばれる、React・Angular・Node・Djangoなど多数のスタックで実装されたMediumクローン。
- **注目理由:** フルスタック実装比較の定番教材として長年愛用されており、今回追跡対象に加わりました。
- **スター数:** 84,048 / **主要言語:** TypeScript
- **リンク:** https://github.com/realworld-apps/realworld

### expressjs/express
- **概要:** Node.js向けの高速・ミニマルなWebフレームワーク。
- **注目理由:** Node.jsエコシステムの基盤ライブラリとして今も現役、定番中の定番。
- **スター数:** 69,364 / **主要言語:** JavaScript
- **リンク:** https://github.com/expressjs/express

### apache/echarts
- **概要:** ブラウザ向けの高機能なインタラクティブチャート・データビジュアライゼーションライブラリ。
- **注目理由:** Apacheプロジェクトとして継続的にメンテナンスされ、企業のダッシュボード実装で広く採用。
- **スター数:** 67,012 / **主要言語:** TypeScript
- **リンク:** https://github.com/apache/echarts

### tobi/qmd
- **概要:** ドキュメントやナレッジベース、議事録などをローカルで検索できるミニCLI検索エンジン。
- **注目理由:** 最新のSOTA（最先端）検索アプローチを追いながら、すべてローカル完結という設計思想が支持を集めています。
- **スター数:** 28,700 / **主要言語:** TypeScript
- **リンク:** https://github.com/tobi/qmd

### 🌟 優先トピック枠（1万スター未満だが注目）

以下2件は掲載基準（1万スター以上）には届きませんが、優先トピック「typescript」「nextjs」に該当するため注目枠として紹介します。

**KuekHaoYang/KVideo**
- **概要:** Next.js 16製のモダンな動画集約プラットフォーム。「Liquid Glass」デザイン言語を採用。
- **注目理由:** Next.js最新版（16）を使った実践的なUI実装例として参考になります。
- **スター数:** 3,946 / **主要言語:** TypeScript
- **リンク:** https://github.com/KuekHaoYang/KVideo

**theodorusclarence/ts-nextjs-tailwind-starter**
- **概要:** Next.js + Tailwind CSS + TypeScriptのスターターボイラープレート。
- **注目理由:** ESLint・Jest・GitHub Actions・Huskyなど開発に必要な設定一式が最初から揃っている実用性の高さ。
- **スター数:** 3,417 / **主要言語:** TypeScript
- **リンク:** https://github.com/theodorusclarence/ts-nextjs-tailwind-starter

---

## 🎯 優先トピックの動き（go / rust / typescript / python / nextjs / claude / hermes-agent 他）

優先トピックに該当するリポジトリの中から、特に動きが大きいものをピックアップします（いずれも1万スター以上）。

- **NousResearch/hermes-agent**（227,582★、+538） — hermes-agentトピック該当。Python製AIエージェント。「成長し続けるエージェント」がコンセプトで、今週も着実にスター増加。
  https://github.com/NousResearch/hermes-agent
- **farion1231/cc-switch**（125,756★、Rust/TypeScript） — Claude Code / Codex / OpenCode / OpenClaw / Hermes Agent を横断管理できるデスクトップアプリ。rust・typescript・claude・hermes-agentと複数の優先トピックに該当する注目株です。
  https://github.com/farion1231/cc-switch
- **Graphify-Labs/graphify**（104,395★、Python） — コードベースをローカルで解析しナレッジグラフ化する `/graphify` スキル。Claude Code / Cursor / Codex / Gemini CLI対応。openclawトピックにも該当。
  https://github.com/Graphify-Labs/graphify
- **anomalyco/opencode**（195,152★、TypeScript、+422） — オープンソースのコーディングエージェント。着実に成長を続けています。
  https://github.com/anomalyco/opencode
- **TauricResearch/TradingAgents**（96,566★、Python、+493） — マルチエージェントLLM金融取引フレームワーク。金融分野でのエージェント活用例として注目。
  https://github.com/TauricResearch/TradingAgents

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
