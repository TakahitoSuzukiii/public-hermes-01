作成日: 2026-11-26 / STATUS: INFO / TOPIC: MCP / 対象期間: 2026-11-19〜2026-11-26

# MCP（Model Context Protocol）週次動向 2026-11-26

> MCP（Model Context Protocol）＝AIアプリと外部ツール・データをつなぐ共通の接続規格。

## 📌 今週のハイライト

- **Events拡張（SEP-3415）が正式採用**：サーバ側で起きた出来事（新着メール、push、障害など）をAIエージェントが購読して反応できる仕組み。現在はベータ。
- **公式レジストリが公開パッケージのマルウェア照合を開始**：公開時と毎日、OSV（オープンな脆弱性・マルウェア情報DB）の記録と突き合わせる。
- 仕様本体（2026-07-28版）は誤記修正中心で、破壊的変更なし。MCP公開2周年の記念記事も出た。
- 公式サーバ集（servers）・TypeScript/Python SDK は今週リリースなし。

## 📐 仕様・公式の動き

**仕様リポジトリ（modelcontextprotocol/modelcontextprotocol）**：今週のコミットは13件、中心は次の3テーマ。
- **Events拡張の登録**：SEP-3415（SEP＝仕様拡張提案）がFinalになり、拡張として登録。クライアントとサーバの双方が明示的にオプトインして使う。要プロトコル版 `2026-07-28` 以降。
  - 3つの配信方式：Poll（クライアントが定期的に問い合わせ）、Push（接続を開いたまま受信）、Webhook（コールバックURLへ署名付きPOST）。サーバは各イベントで対応方式を選べる。
  - カーソルで切断後の再開が可能（ただし再開位置を提供できない場合は `truncated: true` で欠落を通知）。
  - 安全面：イベントのペイロードは外部由来の「信頼できないデータ」で、プロンプトインジェクションを含み得るため、ツール結果と同様にモデルへ渡す前に無害化する、と明記されている。
  - 開発者がやること：サーバは `server/discover` で拡張を宣言し `events/list` で種類を公開。クライアントはカーソルを永続保存し、`eventId` で重複排除。
- **ドキュメント整備**：2026-07-28版とドラフトの誤記修正、拡張対応クライアント表の更新（Skills対応としてClaude / Claude Code / VS Codeを記載、Archestra.AI・mcp-useを追加）。
- **ガバナンス文書**：Core Primitives作業部会の憲章追加、各Interest Groupの憲章をSEP後援ガイドラインに整合、Discord招待リンク更新、2周年ブログ。

**レジストリ（modelcontextprotocol/registry）**：v1.8.10〜v1.8.16の7リリース。
- **マルウェア監視**：公開時と日次でOSVのマルウェア記録と照合、パッケージが消えた登録の報告、アラートメール件名にクラスタ名付与（v1.8.12〜v1.8.14）。
- **運用基盤**：利用状況コレクタの導入、Grafanaダッシュボード/アラートのリポジトリ管理、共有の利用状況認証情報を廃止しGKE（Google Kubernetes Engine）のIDに切替。
- **性能/運用**：サーバ一覧クエリの改善（v1.8.10。DB運用者は置換インデックスを事前作成する手順あり）、取り下げ済みバージョンのモデレータ保留を維持（v1.8.16）。
- サーバ公開者への影響：v1.8.10に「HTTP認証リトライ」「複数証明の検証」の修正と、公開用秘密鍵のファイル/環境変数指定が含まれる。

**SDK**：TypeScript SDK（Star 13,822・最終push 2026-11-25）、Python SDK（Star 24,968・MIT・最終push 2026-11-17）ともに今週のリリースなし。

## 🖥 公式サーバ集（servers）の動き

今週のコミット・リリースはなし（Star 92,250、最終push 2026-11-25）。ライセンス表記はAPI上「NOASSERTION」（判別不能）。

## 🌱 新着・急上昇のMCPサーバ

> 第三者製です。**導入前に信頼性チェック（コード目視・作者・ライセンス）を。** 値は取得時点。

今週作成（Star順、取得ソース上でMCP関連とされたもの）：
- **INK-Q/agy-fast**：Google Antigravity向けMCP高速化プラグイン（LLMターン・トークン消費の削減を謳う）。Star 1,502／MIT／作成 2026-11-19／最終更新 2026-11-25／User。https://github.com/INK-Q/agy-fast
- **w1ccc/sap-data-mcp**：SAP S/4HANAを読み取り専用で照会するMCPサーバ群。Star 151／MIT／作成 2026-11-20／最終更新 2026-11-24／User。https://github.com/w1ccc/sap-data-mcp
- **jasonmello/pocket-design-mcp**：アイコン・フォント・デザイントークン等を提供する無料MCPサーバ。Star 24／Apache-2.0／作成 2026-11-20／最終更新 2026-11-21／User。https://github.com/jasonmello/pocket-design-mcp
- ※fast-anything（Star 3,939）など、Starが急増しているが内容がMCPサーバとして不明瞭・短期間で急増しているものは、Star数の信頼性が不明なため紹介を見送りました（筆者の見立て）。

今週更新・Star多数（既存の定番）：
- **upstash/context7**：AIエージェント向け最新ドキュメント提供。Star 65,461／MIT／作成 2025-03-26／最終更新 2026-11-25／Organization。https://github.com/upstash/context7
- **ChromeDevTools/chrome-devtools-mcp**：コーディングエージェント向けChrome DevTools。Star 59,345／Apache-2.0／作成 2025-09-11／最終更新 2026-11-25／Organization。https://github.com/ChromeDevTools/chrome-devtools-mcp
- **n8n-io/n8n**：AI機能付きワークフロー自動化（MCP対応）。Star 212,133／ライセンス判別不能(NOASSERTION、fair-code)／作成 2019-06-22／最終更新 2026-11-25／Organization。https://github.com/n8n-io/n8n
- **google-gemini/gemini-cli**：ターミナルで動くGeminiエージェント。Star 109,107／Apache-2.0／作成 2025-04-17／最終更新 2026-11-25／Organization。https://github.com/google-gemini/gemini-cli

## 🛡 MCPの安全面

- 公式レジストリがマルウェア照合を始めたのは前進だが、**全てのサーバの安全を保証するものではありません**。
- Events拡張の仕様自体が「イベント内容は信頼しない」ことを求めており、受信データ経由のプロンプトインジェクションに注意。
- 今週のMCP関連の脆弱性は、金曜のAIセキュリティ動向記事を参照（ここでは個別解説しません）。

## 🔧 使いどころ(筆者の見立て)

- Eventsは「メールや障害に自動で反応する常駐エージェント」向け。ただしベータで、対応クライアントがまだ限られるため、まずは検証用途で。
- 外部のMCPサーバを入れるなら、レジストリ掲載＋Organization運営＋ライセンス明記のものから。
- 自作サーバの公開者は、公開用鍵の扱いとレジストリのマルウェア照合結果に注意。

## ℹ この記事の見方

- 取得方法：GitHub公式API（リポジトリのコミット・リリース・メタ情報・検索）を使い、補助として公式サイトを検索。
- 数値（Star等）は取得時点の値。ライセンス「NOASSERTION」は判別不能の意味。
- 取得できなかった情報源：なし（15/15成功）。

## 出典

- https://github.com/modelcontextprotocol/modelcontextprotocol
- https://github.com/modelcontextprotocol/registry
- https://github.com/modelcontextprotocol/servers
- https://github.com/modelcontextprotocol/typescript-sdk
- https://github.com/modelcontextprotocol/python-sdk
- https://modelcontextprotocol.io/extensions/events/overview
- https://modelcontextprotocol.io/seps/3415-events-extension
- https://blog.modelcontextprotocol.io/posts/mcp-turns-two/
- https://api.github.com/ （検索・リポジトリ情報）

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
