# NEXUSホーム(task-board) → Prime Task Board 移行記録

> ステータス: DONE / カテゴリ: SETUP / 実施日 2026-08-09
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP/Discord ID 等は placeholder。
> 関連: `public-openclaw-01` の `docs/hermes/004`（OpenClaw→Hermes全体移行）／`006`（現状サマリ）

## 0. 概要

OpenClaw時代のEC2サーバー上で稼働していたNode.js製Webダッシュボード「NEXUSホーム」（タスクボード／キャリア／ドキュメント／トレーニング／ヘルスケア／チャットの6画面＋ホーム）を、WSL上のHermes環境（`~/optimus/`配下）へ完全移行した記録。EC2は本移行完了後に廃止予定。

- 移行元: `<EC2ホスト>` 上の `~/.openclaw/workspace/tasks/task-board/`（Amazon Linux 2023）
- 移行先: WSL（Ubuntu）上 `~/optimus/task-board/`
- アプリ構成: 4層アーキテクチャ（domain/application/infra/repository/interface）、Node標準ライブラリのみ（npm依存ゼロ、`node:sqlite`使用）
- 名称変更: NEXUS → **Prime**（画面表示・コード内コメント全て）

## 1. 事前バックアップ

破壊的変更に備え、着手前に移行元一式をバックアップ（byte-exact照合用にsha256併記）。

```bash
tar -czf ~/.hermes/backups/pre-nexus-migration-task-board-<timestamp>.tar.gz -C <migration-src>/tasks task-board
tar -czf ~/.hermes/backups/pre-nexus-migration-career-private-<timestamp>.tar.gz -C ~ career-private
sha256sum ~/.hermes/backups/pre-nexus-migration-*.tar.gz
```

デグレ発生時は上記tar.gzから復元し、`~/optimus/task-board/` を削除すれば作業前状態に戻せる（移行元ディレクトリ自体は今回一切書き換えていない）。

## 2. アプリ本体の移行

```bash
cp -r <migration-src>/.openclaw/workspace/tasks/task-board ~/optimus/task-board
```

`data/tasks.db`（実タスク95件）・`data/reports/`（Excelレポート）を含め実データごと引き継ぎ。

### OpenClaw依存の置き換え（追加のみ・デグレ無し方針）

| ファイル | 変更内容 |
|---|---|
| `src/infra/system.mjs` | `openclaw` CLI→`hermes` CLI、`~/.openclaw/openclaw.json`→`~/.hermes/config.yaml`（正規表現で`model.default`/`provider`抽出、YAMLパーサ依存追加なし）。`getCrons()`は`hermes cron list --all`のテキスト出力をパースする方式に変更（該当サブコマンドに`--json`が無いため）。`CLAUDE_BIN`は`which claude`で動的解決するよう変更。config summary（mcp/skills/plugins/agents/hooks）も`hermes mcp list`・`hermes skills list --enabled-only`・`hermes profile list`・`hermes plugins list --json`のパースに置き換え |
| `src/infra/infoDocs.mjs` | 参照先を`~/optimus/docs`単一ルートに簡素化（旧`/opt/docs/openclaw-news`との2ルート統合ロジックを削除） |
| `poller-healthcheck.mjs` | `openclaw cron list --json`→`hermes cron list --all`＋対応パーサに変更 |
| `public/home.html` | cron名→日本語ラベル対応表を更新（`openclaw-autoupdate-timer`→`hermes-autoupdate-timer`等） |
| 全ファイル | 「NEXUS」→「Prime」置換（画面表示・コメント。`deploy/`のCaddy設定は対象外＝後述の理由で不要になるため） |

## 3. 動作検証

```bash
cd ~/optimus/task-board && node server.mjs   # 127.0.0.1:18790 で待受
```

- 8画面すべてHTTP 200確認: `/` `/dashboard` `/info` `/training` `/training/dashboard` `/body` `/career` `/chat`
- `NEXUS`文字列の残存ゼロ（grep確認、`deploy/`除く）
- `/api/home`が実cron 8件（移植済みジョブ）を正しく返すことを確認
- `/api/system-status`でHermesのmcp/skills/plugins/agents構成が正しく取得できることを確認

## 4. 常駐化（systemdユーザーサービス）

`hermes-gateway.service`と同様の方式で常駐化。ログオン不要（`loginctl` linger有効済み）。

```ini
# ~/.config/systemd/user/optimus-taskboard.service
[Unit]
Description=Prime Task Board - Home Dashboard Web App
After=network-online.target
Wants=network-online.target
StartLimitIntervalSec=0

[Service]
Type=simple
ExecStart=/home/<your-user>/.local/bin/node /home/<your-user>/optimus/task-board/server.mjs
WorkingDirectory=/home/<your-user>/optimus/task-board
Restart=always
RestartSec=5
KillMode=mixed
KillSignal=SIGTERM
TimeoutStopSec=30
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=default.target
```

```bash
systemctl --user daemon-reload
systemctl --user enable --now optimus-taskboard.service
systemctl --user status optimus-taskboard.service --no-pager
```

## 5. 外部公開（Tailscale Serve、Caddyから置き換え）

旧EC2構成ではCaddy（リバースプロキシ）＋Tailscaleでの公開だったが、WSL2の**localhost forwarding**（標準機能）により、WSL内`127.0.0.1:18790`はWindows側から`localhost:18790`として透過的にアクセス可能。Windows本体に導入済みのTailscaleで直接Serveできるため、**Caddyは不要**になった。

### Windows側作業（鈴木さん実施、PowerShell）

```powershell
# 疎通確認（WSL2 localhost forwarding）
curl http://localhost:18790/

# Tailscale Serve設定
tailscale serve --bg --https=443 http://localhost:18790

# 状態確認
tailscale serve status

# 停止する場合
tailscale serve --https=443 off
```

公式: https://tailscale.com/kb/1242/tailscale-serve

### 注意

- 旧EC2版は「社外向け限定公開（転職ポートフォリオ）」用にCaddy側で`/career`・`/chat`を遮断する多層防御（`deploy/`配下）を実装していたが、今回は個人利用前提のため未移植。将来的に社外公開が必要になった場合は改めて対応する。
- `deploy/`（旧Caddyfile一式）は不要になったため、後日削除して差し支えない。

## 6. 残タスク・注記

- `/api/home`のJSONキー名が`openclawVersion`のまま（値は正しくHermesのバージョンが入っている）。動作に支障はないが、将来的なリネームは検討の余地あり。
- `career-private`（個人の転職活動資料、機微情報）はこのマシン上に既に存在しており、パスは変更せず引き継ぎ。アクセスはloopback/Tailscale経由のみを維持。

## 参考（公式）

- WSL2 localhost forwarding: https://learn.microsoft.com/ja-jp/windows/wsl/networking
- Tailscale Serve: https://tailscale.com/kb/1242/tailscale-serve
- Hermes context files: https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files/

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
