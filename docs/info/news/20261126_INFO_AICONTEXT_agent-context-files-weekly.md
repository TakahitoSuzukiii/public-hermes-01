作成日: 2026-11-26 / STATUS: INFO / TOPIC: AICONTEXT / 対象期間: 2026-11-19〜2026-11-26

# AIエージェント設定ファイル（CLAUDE.md / AGENTS.md / MEMORY.md）週次ウォッチ

## 📌 今週のハイライト
- Claude Code が v2.1.328〜v2.1.332 の5連続リリース。**MCPサーバー由来のスキル（ベータ）** と、スキル読み込み時のシェル実行を拒否できる **`PreSkillShellCommand` フック** が追加。
- 圧縮（コンパクション。長い会話を要約してコンテキストを節約する処理）関連の不具合修正が多数。長時間セッションの安定性が向上。
- CLAUDE.md が worktree 移動・再開時に**二重にモデルへ送られる問題**が修正。
- OpenAI Codex は正式版 v0.171.0 / v0.172.0。`codex exec resume` がサンドボックス権限や作業ディレクトリを復元。
- AGENTS.md 規格リポジトリ自体は今週コミットなし（最終更新 2026-09-10）。

## 📝 Claude Code の更新（設定ファイル・メモリ・フック・サブエージェント関連）
リリース一覧: https://github.com/anthropics/claude-code/releases

- **v2.1.332（11/25）**
  - MCP（Model Context Protocol。AIと外部ツールをつなぐ規格）サーバーからスキルを提供可能に（ベータ）。`/` メニューに `server:skill` 形式で表示。
  - `PreSkillShellCommand` フック追加: スキルやコマンド内のインラインシェル実行を読み込み時に拒否できる。**注意:** 2.1.331以前では、設定ファイルにこの名前があると起動時にダイアログが出る。
  - CLAUDE.md／rules が worktree（`.claude/worktrees`）移動や再開で二重送信される問題を修正（トークン節約に直結）。
  - 圧縮が失敗し続けて "Prompt is too long" になる問題、要約が長すぎて失敗する問題を修正。
  - フックが無限に出力する場合のフリーズ・メモリ暴走、巨大ログ（約5万字超は切り詰め）による文脈溢れを修正。
  - `.env` が名前付きパイプ（秘密管理ツールのマウント等）の場合の読み取りハングを、20秒で失敗する形に修正。
  https://github.com/anthropics/claude-code/releases/tag/v2.1.332
- **v2.1.331（11/23）**: プラグインマニフェストに `optionalDependencies`。圧縮時にXMLタグを含む要約が欠ける問題、Stopフックが最後の返信を読めない問題、`Skill(name:*)` 許可ルールが保存されない問題などを修正。 https://github.com/anthropics/claude-code/releases/tag/v2.1.331
- **v2.1.330（11/20）**: Enterprise Admin Console 管理組織へのサインインに対応。複数プロセス同時保存でユーザー設定が失われる問題、サブエージェントが宣言したMCPサーバーが他の使用中に停止する問題を修正。 https://github.com/anthropics/claude-code/releases/tag/v2.1.330
- **v2.1.329（11/19）**: 信頼ダイアログで「フックがどこで宣言されたか」を警告表示（不審なリポジトリのフックに気づきやすくなる）。`autoCompactWindow` 設定が事前起動プロセスで無視される問題を修正。 https://github.com/anthropics/claude-code/releases/tag/v2.1.329
- **v2.1.328（11/19）**: Bedrock/Google Cloud/Foundry 上の Opus 4.6・Sonnet 4.6 で auto mode 対応。`mcp_tool` フックに `"onFailure": "block"`（失敗時に操作をブロック）。自動圧縮が古いシステムプロンプトを再利用する問題を修正。 https://github.com/anthropics/claude-code/releases/tag/v2.1.328

**運用への影響（筆者の見立て）:** フック・圧縮・設定保存の堅牢化が中心。フックを使っている場合は出力量の上限が安全側になり、安心して使える方向。

## 🤖 OpenAI Codex の更新
リリース一覧: https://github.com/openai/codex/releases
今週は正式版2件のほか、0.173/0.174 系のアルファ（プレリリース）が多数。アルファは触れず、正式版のみ記載。
- **rust-v0.172.0（11/24）**: `codex exec resume` が保存済みのサンドボックス権限・作業ディレクトリ・ワークスペースルートを復元（明示指定で上書き可）。同梱の `openai-docs` スキルが GPT-6.2 への移行情報に対応。 https://github.com/openai/codex/releases/tag/rust-v0.172.0
- **rust-v0.171.0（11/20）**: TUI（ターミナルUI）ワークスペースが標準で有効（文書・画像プレビュー、サブエージェントの会話表示）。作業ディレクトリ変更時も権限プロファイルを維持。 https://github.com/openai/codex/releases/tag/rust-v0.171.0

## 📐 AGENTS.md 規格の動き
- 規格リポジトリ agentsmd/agents.md: 今週コミットなし。最終 push は 2026-09-10。Star 25,709 / ライセンス MIT / 作成 2025-08-19 / Organization。 https://github.com/agentsmd/agents.md
- 対応ツールは広い。Cursor はルート・サブディレクトリの AGENTS.md に対応し、深い階層ほど優先（https://cursor.com/docs/rules）。GitHub Copilot も AGENTS.md / CLAUDE.md / GEMINI.md を読む（https://docs.github.com/en/copilot/reference/custom-instructions-support）。
- VS Code の公式リファレンスによると、対応ファイルは「モデルではなくエージェント環境（ハーネス）で決まる」。Claude は `CLAUDE.md`、Codex は `AGENTS.md`。ツール横断では優先順位の共通ルールがないため、**矛盾する記述を避けるのが基本**（https://code.visualstudio.com/docs/agents/reference/custom-instructions-reference）。
- 次に見る点: 規格側の更新が止まっているため、各ツールの読み込み仕様差（上書きファイル、サイズ上限）の動き。

## 🧭 書き方・運用のベストプラクティス
1. **サイズ上限を意識する**: Codex は AGENTS.md の合計が既定 32 KiB（`project_doc_max_bytes`）に達すると以降を読み込まない。大きいなら階層に分割（https://learn.chatgpt.com/docs/agent-configuration/agents-md）。
2. **肥大化は逆効果**: 2026年の研究を紹介するブログによれば、LLM生成の文脈ファイルはタスク成功率を下げ、人手作成でも効果は小さい（出典記事の主張。原論文は未確認）。https://codex.danielvaughan.com/2026/03/27/agents-md-bloat-problem/
3. **目安は200行程度、1つを正とする**: 指示の原本を1つにし、他ツール向けはインポート等で共有する構成が推奨されている。https://notes.hasanarief.dev/guides/agents-md-best-practices/
4. **設定の「臭い」を知る**: AGENTS.md/CLAUDE.md の典型的な誤りを分類した研究論文（arXiv）。 https://arxiv.org/html/2606.15828v2
5. **安全面**: フック／スキルのシェル実行は、今週の `PreSkillShellCommand` や信頼ダイアログの警告のように、**読み込み時に検査する仕組み**が整いつつある。外部由来のスキル・リポジトリの指示文は「データ」として扱い、機密や破壊的操作は文脈ファイルではなく権限設定で制限するのが堅実（筆者の見立て）。

参考（第三者リポジトリ。導入前に信頼性チェック（コード目視・作者・ライセンス）を）:
- affaan-m/ECC — Star 310,699 / MIT / 作成 2026-01-18 / 最終更新 2026-11-23 / User
- NousResearch/hermes-agent — Star 266,106 / MIT / 作成 2025-07-22 / 最終更新 2026-11-25 / Organization
- Graphify-Labs/graphify — Star 153,359 / Apache-2.0 / 作成 2026-04-03 / 最終更新 2026-11-25 / Organization

## 🔧 鈴木さんの環境への示唆
- （筆者の見立て）システムプロンプト系ファイルは肥大化しやすいため、定期的に行数・重複を点検し、詳細は別ファイルへ逃がす運用が有効。
- フックを使う場合、出力量の上限やブロック挙動が改善されているので、最新版への更新を検討する価値あり。
- 外部スキル・MCP由来スキルを入れる際は、既存の信頼性チェック手順に加え、読み込み時のシェル実行有無を確認すると安全。

## ℹ この記事の見方
- 取得方法: GitHub 公式API（Releases・リポジトリ情報）の自動取得＋公式ドキュメントの Web 検索。
- 数値（Star 等）は取得時点（2026-11-26 朝）の値。
- 取得できなかった情報源: なし（6/6 成功）。
- 原論文・ブログの主張は一次確認していないものを含む。

## 出典
- https://github.com/anthropics/claude-code/releases
- https://github.com/openai/codex/releases
- https://github.com/agentsmd/agents.md
- https://cursor.com/docs/rules
- https://docs.github.com/en/copilot/reference/custom-instructions-support
- https://code.visualstudio.com/docs/agents/reference/custom-instructions-reference
- https://learn.chatgpt.com/docs/agent-configuration/agents-md
- https://codex.danielvaughan.com/2026/03/27/agents-md-bloat-problem/
- https://notes.hasanarief.dev/guides/agents-md-best-practices/
- https://arxiv.org/html/2606.15828v2

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
