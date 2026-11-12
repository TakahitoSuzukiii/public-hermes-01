作成日: 2026-11-12 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-11-05 → 2026-11-12）

GitHub 公式 REST Search API で集めたデータを、前週（2026-11-05）と比べた差分レポートです。
- **掲載基準:** スター数 10,000 以上、開発者向けのリポジトリ。
- **risers（ライザー）:** 前週よりスターが大きく増えたもの。
- **newcomers（ニューカマー）:** 今週はじめて集計対象（今回の調査範囲）に入ったもの。リポジトリ自体が新規とは限りません（古い定番も含みます）。
- 今週は基準データではなく通常の差分週です。

## 今週の傾向（要点）

- **「Agent Skills（エージェントスキル）」ブーム継続。** AI コーディングエージェントに知識・作法を教える部品（スキル）系が上位を占めています。
- **DeepSeek Harness（DSH）エコシステムが急拡大。** 本体、デスクトップ版、無料モデルプラグインが同時に登場・上昇。
- **定番の学習系リポジトリ**（build-your-own-x など）が集計に入ってきました。

## 1. 急上昇（risers）：前週比スター増

- **morluto/rea** — TypeScript / ★454,647（+21,192）
  - 概要: エージェントを使い、アプリの挙動からネイティブバイナリまで「何でもリバースエンジニアリング」するツール。
  - 注目理由: 今週最大の伸び。Claude Code 等と組み合わせる前提。
  - リンク: https://github.com/morluto/rea
- **sherlock-project/sherlock** — Python / ★110,495（+14,146）
  - 概要: ユーザー名から各 SNS のアカウントを探す OSINT（公開情報調査）CLI。
  - 注目理由: 定番ツールが再燃。セキュリティ・調査系で人気。
  - リンク: https://github.com/sherlock-project/sherlock
- **pingdotgg/t3code** — TypeScript / ★57,999（+10,241）
  - 概要: Claude Code や Codex を PC・スマホから操作する UI。
  - リンク: https://github.com/pingdotgg/t3code
- **cloudflare/security-audit-skill** — JavaScript / ★70,924（+10,152）
  - 概要: 多段階のセキュリティ監査を行うエージェント用スキル。結果は機械可読で、独立検証つき。
  - リンク: https://github.com/cloudflare/security-audit-skill
- **Ebony-Vinyl/dsh-our-free-model** — JavaScript / ★71,165（+9,063）
  - 概要: DSH に入れるだけでログインや API キー不要で複数の最新モデルを使えるとうたうプラグイン。
  - 注意: 提供元・利用規約・データの送信先が不明確です。導入前に必ず中身を確認してください（個人的には様子見を推奨）。
  - リンク: https://github.com/Ebony-Vinyl/dsh-our-free-model
- **mattpocock/skills** — Shell / ★322,757（+8,127）
  - 概要: 開発者 Matt Pocock が自分のエージェント設定ディレクトリを公開したスキル集。
  - リンク: https://github.com/mattpocock/skills
- **debpalash/VoiceStudio** — Python / ★108,948（+7,298）
  - 概要: 完全ローカルで動く ElevenLabs 代替。音声クローン、動画吹き替え、文字起こし等。
  - 注目理由: ローカル完結で無料志向の人に合う。
  - リンク: https://github.com/debpalash/VoiceStudio
- **stablyai/orca** — TypeScript / ★123,220（+6,837）
  - 概要: 自分の契約で Claude Code / Codex を複数同時に動かす「エージェント艦隊」管理アプリ（デスクトップ・モバイル対応）。
  - 注目理由: topics に hermes-agent を含む（優先トピック）。
  - リンク: https://github.com/stablyai/orca
- **deepseek-ai/deepseek-harness** — TypeScript / ★279,662（+6,056）
  - 概要: 「すべてがプラグイン」を掲げる DeepSeek のエージェント基盤（DSH）。
  - リンク: https://github.com/deepseek-ai/deepseek-harness
- **anthropics/skills** — Python / ★193,559（+5,902）
  - 概要: Anthropic 公式の Agent Skills 公開リポジトリ。
  - リンク: https://github.com/anthropics/skills
- **Nutlope/hallmark** — CSS / ★53,850（+5,318）
  - 概要: 「AI っぽい量産デザイン」を避けるためのデザインスキル（Claude Code / Cursor / Codex 対応）。
  - リンク: https://github.com/Nutlope/hallmark
- **pbakaus/impeccable** — Rust / ★108,812（+5,204）
  - 概要: コーディングエージェントにデザイン用語（polish, critique, audit 等）で指示するためのスキル集。
  - リンク: https://github.com/pbakaus/impeccable
- **DietrichGebert/ponytail** — JavaScript / ★189,626（+4,592）
  - 概要: 「一番良いコードは書かないコード」の考えでエージェントを動かすスキル。
  - リンク: https://github.com/DietrichGebert/ponytail
- **vercel-labs/agent-browser** — Rust / ★50,227（+4,519）
  - 概要: AI エージェント向けブラウザ自動操作 CLI。
  - リンク: https://github.com/vercel-labs/agent-browser
- **Gathin23/cleanyourtv** — Python / ★56,876（+4,416）
  - 概要: Android / Google TV を Wi-Fi 経由で不要アプリ削除し軽くするツール。
  - リンク: https://github.com/Gathin23/cleanyourtv

## 2. 新規ランクイン（newcomers）：スター1万以上

- **codecrafters-io/build-your-own-x** — Markdown / ★562,068: 好きな技術をゼロから作り直して学ぶチュートリアル集。https://github.com/codecrafters-io/build-your-own-x
- **jwasham/coding-interview-university** — ★364,308: ソフトウェアエンジニアになるための CS 学習計画。https://github.com/jwasham/coding-interview-university
- **ossu/computer-science** — HTML / ★211,046: 無料で学べる CS 独学カリキュラム。https://github.com/ossu/computer-science
- **datawhalechina/hello-agents** — Python / ★86,845: 「ゼロから作るエージェント」の中国語チュートリアル。https://github.com/datawhalechina/hello-agents
- **OpenMontageInc/OpenMontage** — Python / ★79,939: オープンソースのエージェント型動画制作システム（12 パイプライン、100 以上のツール）。https://github.com/OpenMontageInc/OpenMontage
- **usestrix/strix** — Python / ★75,137: AI による脆弱性発見（ペネトレーションテスト）ツール。https://github.com/usestrix/strix
- **shanraisshan/claude-code-best-practice** — HTML / ★69,001: Claude Code のベストプラクティス集。https://github.com/shanraisshan/claude-code-best-practice
- **LadybirdBrowser/ladybird** — Rust(主要言語は C++ 含む) / ★67,084: 独立系の新しい Web ブラウザエンジン。https://github.com/LadybirdBrowser/ladybird
- **obsidianmd/obsidian-skills** — Shell / ★51,922: Obsidian 用エージェントスキル（CLI・Markdown・Canvas 対応）。https://github.com/obsidianmd/obsidian-skills
- **mudler/LocalAI** — Go / ★50,336: GPU 不要で LLM・画像・音声を動かすローカル AI エンジン。https://github.com/mudler/LocalAI
- **Dokploy/dokploy** — TypeScript / ★38,443: Vercel / Netlify / Heroku の OSS 代替（セルフホスト用デプロイ基盤）。https://github.com/Dokploy/dokploy
- **anywhere-labs/dsh-desktop** — TypeScript / ★35,848: DSH のデスクトップ版（デスクトップ自体もプラグイン）。https://github.com/anywhere-labs/dsh-desktop
- **freestylefly/awesome-gpt-image-2** — JavaScript / ★35,752: GPT Image 2 / 2.5 のプロンプト・事例集。https://github.com/freestylefly/awesome-gpt-image-2
- **a2ui-project/a2ui** — TypeScript / ★17,177: エージェントがレイアウトデータを流し、アプリが描画する生成 UI フレームワーク。https://github.com/a2ui-project/a2ui

※ massgravel/Microsoft-Activation-Scripts（ライセンス回避系ツール）は、法的・安全上の理由から詳細紹介を省略しました。

## 3. 優先トピック注目枠（1万未満も含む）

優先トピック: go / rust / typescript / python / nextjs / claude / hermes-agent（ほか openclaw, angular, docker, nix も集計）

- **stablyai/orca**（hermes-agent タグ）: 上記のとおり急上昇中。Hermes 系の話題として注目。
- **alchaincyf/zhangxuefeng-skill** — ★10,754 / 言語なし（claude, openclaw, hermes-agent タグ）: 進路・キャリア相談の思考枠組みを再現するスキル。hermes-agent タグ付きの新規ランクイン。https://github.com/alchaincyf/zhangxuefeng-skill
- **khuedoan/homelab** — HCL / ★9,729（docker, nix）【1万未満】: 空のディスクからサービス稼働まで全自動のセルフホスト基盤。https://github.com/khuedoan/homelab
- **amannn/next-intl** — TypeScript / ★4,391（nextjs）【1万未満】: Next.js 向け国際化（i18n）ライブラリ。https://github.com/amannn/next-intl
- **Go:** LocalAI が新規入り。**Rust:** Ladybird・agent-browser・impeccable が登場。**TypeScript:** t3code・orca・Dokploy・a2ui が活発。**Python:** sherlock・VoiceStudio・strix・hello-agents など。**Claude:** スキル系が圧倒的多数。

## 掲載件数

risers 15 件 + newcomers 14 件（1 件は省略）+ 優先注目枠 2 件（1万未満・新規）。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
