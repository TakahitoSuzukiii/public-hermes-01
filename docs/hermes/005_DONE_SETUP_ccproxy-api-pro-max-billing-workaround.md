# ccproxy-api を用いた Claude Pro/Max サブスク経由の推論経路構築（billing bug 回避策）

> ステータス: DONE / カテゴリ: SETUP / 実施日 2026-08-13
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP 等は placeholder。
> 関連: `hermes-anthropic-billing-diagnostics` スキル

## 0. 背景・課題

Hermes Agent は Anthropic OAuth 経由（Claude Code 認証）で Claude モデルを呼び出す際、**Claude Max プランの「extra usage credits（従量課金の追加クレジット）」のみを消費**し、Max プラン本来の通常使用枠（セッション%・週間%）を消費しない既知の制約がある。Claude Pro プランに至っては OAuth 経路自体が利用不可（Hermes 公式ドキュメントに明記）。

この結果、Hermes を Anthropic 経由で使い続けると、Pro/Max プランの「使い放題」枠を素通りして、都度クレジットを消費してしまう。

## 1. 対応方針

[ccproxy-api](https://github.com/CaddyGlow/ccproxy-api)（OSS のローカルリバースプロキシ、plugin-based で複数 AI プロバイダを統一 API で提供）を導入し、以下の構成にする:

- **主系**: `claude` CLI（ローカルにインストールした Anthropic 公式 CLI、Pro/Max アカウントでログイン）→ ccproxy-api（ローカルプロキシ）経由で Hermes から呼び出す。**通常使用枠を正しく消費**することを実測で確認。
- **フォールバック**: 既存の `anthropic` プロバイダ（OAuth/API キー、クレジット消費）。主系が想定内エラー（レート制限・過負荷等）を返した場合、Hermes 標準の fallback 機構で自動切替。

### 追加のみ・デグレ無し

- 既存の `anthropic` プロバイダ定義は一切変更せず残置（切り戻し用）。
- 新規プロバイダ `anthropic-ccproxy` を `providers:` に追加する形で実装。
- 変更は全て `~/.hermes/scripts/versioned_edit.sh` 経由（バージョン管理・ドリフト検知付き）。

## 2. 構築手順

### 2.1 事前準備

```bash
# ccproxy-api インストール(uv tool経由)
uv tool install ccproxy-api

# claude CLI に Pro/Max アカウントでOAuthログイン(ブラウザ操作)
claude  # 初回起動時にログインフローが走る
claude auth status  # subscriptionType: pro/max を確認
```

### 2.2 ccproxy-api の systemd ユーザーサービス化

`~/.config/systemd/user/optimus-ccproxy.service`:

```ini
[Unit]
Description=Optimus CCProxy API - Claude Pro/Max subscription auth reverse proxy (Hermes billing bug workaround)
After=network-online.target
Wants=network-online.target
StartLimitIntervalSec=0

[Service]
Type=simple
ExecStart=<ccproxy実行パス> serve --port 8990
Restart=on-failure
RestartSec=5
Environment=HOME=<your-user home>

[Install]
WantedBy=default.target
```

```bash
systemctl --user daemon-reload
systemctl --user enable --now optimus-ccproxy.service
curl -s http://127.0.0.1:8990/health  # 疎通確認
```

### 2.3 Hermes config.yaml へのプロバイダ追加

`providers:` ブロックに追加（既存 `anthropic` は無変更）:

```yaml
providers:
  anthropic-ccproxy:
    # ccproxy-api経由でClaude Pro/Maxサブスク認証を使うプロバイダ(billing bug回避策)
    base_url: http://127.0.0.1:8990/claude/v1
    # 重要: OpenAI互換変換(chat_completions)ではなく、Anthropicネイティブ形式で
    # 通信させる。ccproxy-apiのOpenAI→Anthropic変換処理にバグがあり、
    # 長い会話履歴でtool_use/tool_result不整合による400エラーが発生するため。
    api_mode: anthropic_messages
    discover_models: false
    models:
      - claude-opus-5
      - claude-sonnet-5
      - claude-haiku-4-5
```

`model:` をこのプロバイダに切替、既存 `anthropic` をフォールバック登録:

```yaml
model:
  default: claude-sonnet-5
  provider: anthropic-ccproxy

fallback_providers:
  - provider: anthropic
    model: claude-sonnet-5
```

反映には `hermes gateway restart`（または `systemctl --user restart hermes-gateway.service`）が必要。**Hermes ゲートウェイは自分自身を再起動するコマンドを自ゲートウェイ上のセッションから実行できない安全ガードがあるため、実行中のエージェントとは別のシェル（ユーザー自身の手動操作）で行う。**

## 3. 発生した不具合と原因究明

### 3.1 事象

`model.provider: anthropic-ccproxy` 適用直後、長い会話履歴（ツール呼び出しを多く含むセッション）で以下のエラーが頻発:

```
Anthropic API 400: tool_use ids were found without tool_result blocks immediately after
```

ccproxy-api 側ログには `orphaned_tool_result_removed` 警告が出力されていた。

### 3.2 原因

Hermes の `custom` 系プロバイダ（`api_mode` 未指定時のデフォルト）は OpenAI 互換形式（`/chat/completions`）で通信する。ccproxy-api はこれを内部で Anthropic Messages 形式へ変換するが、**この変換処理（`openai_to_anthropic` フォーマッタ）に、長い会話・複雑な tool_use チェーンで tool_use/tool_result の対応関係が崩れるバグがある**ことが判明。短い PoC テスト（1〜2 往復）では再現せず、実運用スケールで初めて顕在化した。

### 3.3 対処

Hermes の `providers.<name>.api_mode: anthropic_messages` 設定（Hermes 側で正式サポートされている機能）を使い、**OpenAI 互換変換を経由せず Anthropic ネイティブ形式で直接通信**するよう変更。ccproxy-api 側の変換バグを丸ごとバイパスする形になり、解消を確認（tool_use を含む複数ターンの会話でエラー無く動作、`orphaned_tool_result_removed` ログも解消）。

## 4. 堅牢化（安全に使うための仕組み）

### 4.1 ヘルスチェックスクリプト

`~/.hermes/scripts/ccproxy-healthcheck.sh` — 以下を判定し `STATE=OK|DOWN|UNHEALTHY|ERROR_SPIKE` を出力:
- systemd サービスの稼働状態
- `/health` エンドポイントの HTTP ステータス
- 直近5分間の実エラー系ログ件数（400/401/403/5xx、`orphaned_tool_result_removed` 等。404 は正常運用でも探索プローブとして頻発するため対象外、閾値3件以上で異常判定）

### 4.2 自動安全装置

`~/.hermes/scripts/ccproxy-auto-safeguard.sh` — ヘルスチェックが異常を検知し、かつ現在 `model.provider` が `anthropic-ccproxy` の場合、**`versioned_edit.sh` 経由で自動的に `anthropic`（クレジット消費だが確実に動く経路）へ切り戻す**。正常時は無出力・無変更（サイレント）。

反映（ゲートウェイ再起動）は安全のため**自動実行せず**、切り戻し検知時のみユーザーに通知して手動対応を促す設計。

### 4.3 監視 cron ジョブと段階的頻度削減

| ジョブ名 | 内容 | 頻度 |
|---|---|---|
| `ccproxy-healthcheck-safeguard` | 上記スクリプトを定期実行（`no_agent` モード、LLM 不使用） | 導入時: 10分毎 |
| `ccproxy-monitor-freq-reduce-1` | 1ヶ月安定運用後、10分毎→1時間毎に変更する一回限りジョブ | 2026-09-13 実行予定 |
| `ccproxy-monitor-freq-reduce-2` | さらに3ヶ月安定運用後（導入から4ヶ月後）、1時間毎→1日1回に変更する一回限りジョブ | 2026-12-13 実行予定 |

段階的頻度削減の判断基準: 各時点で `ccproxy-healthcheck-safeguard` の実行履歴に異常検知（自動切り戻し発動）が無いことを条件とする。異常があった場合は頻度を維持し、鈴木さんに確認を仰ぐ。

## 5. 検証結果

| 検証項目 | 結果 |
|---|---|
| 通常使用枠（セッション%・週間%）の消費 | ✅ Anthropic 利用状況ページで確認（テスト実施ごとに %上昇を確認） |
| クレジット（$）の非消費 | ✅ テスト前後で変化なしを確認 |
| モデル指定機能の維持（sonnet/opus/haiku） | ✅ 全モデルで指定通りの応答を確認 |
| 長い会話・複数ツール呼び出しでの安定性 | ✅ `api_mode` 修正後、エラー無く動作確認 |
| フォールバック機構 | Hermes 標準機構を使用、想定内エラー種別（429/500/502/503/401/403/404）で自動発動する設計。今回の 400 エラーは対象外だったため、根本原因（3節）を別途修正 |

## 6. 既知の制約・今後の課題

- ccproxy-api 自体の `openai_to_anthropic` 変換バグは未修正（アップストリーム側の問題）。`api_mode: anthropic_messages` で回避しているため実害は無いが、他の用途（OpenAI 互換クライアントからの利用等）では引き続き注意が必要。
- `claude` CLI の OAuth トークン有効期限切れ時の自動再認証は未検証。将来的にヘルスチェックへ検知ロジックを追加する余地がある。
- 監視頻度削減の自動実行（cron）は日時指定の一回限りジョブのため、実行時点で異常があった場合は鈴木さんへの確認プロンプトを含む設計とした。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
