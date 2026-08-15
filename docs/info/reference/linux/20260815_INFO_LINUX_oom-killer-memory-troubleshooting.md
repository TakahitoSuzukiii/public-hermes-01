# Linuxサーバーのメモリ管理・OOM Killer・障害調査ガイド

> **対象**: Linuxサーバーでのメモリ不足（OOM）・フリーズ・カーネルパニックの原因調査と対策を知りたいインフラ担当者向け。
> **作成日**: 2026-08-15（JST） / **ステータス**: INFO（情報提供・トラブルシューティングガイド）
> **一次情報**: カーネルドキュメント（[Linux kernel documentation — OOM killer](https://www.kernel.org/doc/html/latest/admin-guide/mm/concepts.html)）、各種manページ（`dmesg`, `journalctl`, `vmstat`, `free`）
> **元記事**: public2リポジトリ `oom/oom.md` `linux/linux.md` を再構成（内容はweb_searchで裏取りし加筆修正）

---

## 用語ミニ解説（初心者向け）

- **OOM（Out of Memory）**: システムの物理メモリとスワップ領域が枯渇した状態。
- **OOM Killer**: OOM状態になった際、カーネルが特定のプロセスを強制終了してシステムの動作を維持する仕組み。
- **cgroup（control group）**: プロセスグループ単位でCPU・メモリ等のリソースを制限する Linux カーネルの機能。Dockerコンテナのリソース制限にも使われる。
- **ソフトロックアップ／ハードロックアップ**: CPUが長時間割り込みを処理できない（ソフト）／CPUが完全停止する（ハード）異常状態。
- **カーネルパニック**: カーネルが致命的エラーを検出し、システムの動作を停止する状態。

---

## 1. OOM Killerの仕組みと発動条件

Linuxではプロセスがメモリを要求すると、カーネルが適切なメモリ領域を割り当てる。物理メモリとスワップ領域が枯渇すると、OOM Killerがメモリ消費量の多い（かつ優先度の低い）プロセスを選んで強制終了し、システム全体のクラッシュを防ぐ。

### 発動条件

- 物理メモリ・スワップ領域の枯渇
- メモリのオーバーコミット（実際のメモリ量以上の割り当てを許可する仕組み）下で複数プロセスが同時にメモリを大量消費
- メモリリーク（解放されないメモリが蓄積する不具合）の発生

### 対策

- スワップ領域を増やす（下記4章参照）
- 物理メモリを増設する
- `oom_score_adj` でプロセスごとの優先度を調整し、重要なプロセスが誤って終了されないようにする

> ⚠️ **cgroup v2時代の補足**: コンテナ環境（Docker/Kubernetes）ではcgroup単位でメモリ上限を設定するのが一般的です。cgroupのメモリ上限に達した場合も、システム全体のOOM Killerとは別に「cgroup内のOOM Killer」が働き、そのcgroup内のプロセスを終了させます。近年はカーネルのメモリ回収ロジックの改善により、cgroup v2環境でのOOM Killer挙動はv1と異なる点があるため、コンテナ基盤を運用する場合は使用しているカーネルバージョンでの挙動を個別に確認することが推奨されます。

---

## 2. メモリ使用状況を確認する主要コマンド

| コマンド | 用途 | 主なオプション |
|---|---|---|
| `top` | プロセス・リソースをリアルタイム監視 | `-b`（バッチモード）, `-o %MEM`（ソート） |
| `htop` | `top`の視覚的強化版 | `-u <user>`（ユーザー絞り込み） |
| `free -h` | メモリ・スワップの使用状況を一覧表示 | `-m`（MB単位）, `-t`（合計表示） |
| `vmstat 1 10` | メモリ・CPU・I/Oの統計を継続表示 | `-s`（詳細情報） |
| `dmesg \| grep -i oom` | OOM発生ログの確認 | `-T`（人間可読タイムスタンプ） |

---

## 3. 障害調査時のログ・キーワード早見表

| 事象 | 確認コマンド | 代表的なログキーワード |
|---|---|---|
| OOM発生 | `dmesg -T \| grep -i oom` | `Out of memory`, `Killed process`, `oom-killer`, `memory cgroup out of memory` |
| フリーズ・ハングアップ | `dmesg \| grep -i "task blocked"` | `Task blocked for more than 120 seconds`, `soft lockup`, `hard lockup` |
| カーネルパニック | `journalctl -k \| grep -i "kernel panic"` | `Kernel panic - not syncing`, `hung_task: blocked tasks` |
| NULLポインタ参照エラー | `dmesg \| grep -i "NULL pointer"` | `BUG: unable to handle kernel NULL pointer dereference`, `Segmentation fault (core dumped)` |
| シャットダウン履歴 | `last -x shutdown reboot` | `shutdown`, `reboot`, `system halted` |
| 再起動履歴 | `journalctl -b -1 \| grep -i reboot` | `Restarting system`, `systemd-shutdown` |

### 各事象の対策の要点

- **タスクブロック**: `iotop` でディスクI/O負荷を調査。過負荷なプロセスを特定して対処。
- **ロックアップ**: `journalctl -k | grep -i lockup` でログ確認、`top`/`htop` でCPU負荷を監視。
- **カーネルパニック**: ハードウェア診断、カーネルアップデートの実施。
- **NULLポインタ参照**: アプリケーション/カーネルモジュール側のコード修正が必要（ハードウェア問題の場合は `memtest86+` 等でメモリ診断）。

---

## 4. スワップ領域の設定手順

```bash
# 現状確認
free -h
swapon --show

# 1GBのスワップファイルを作成
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024

# 権限を600に制限（他ユーザーからのアクセス防止）
sudo chmod 600 /swapfile

# スワップ領域としてフォーマット
sudo mkswap /swapfile

# 有効化
sudo swapon /swapfile

# 永続化（再起動後も有効にする）
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab

# 確認
free -h
```

> ⚠️ **注記**: `dd` によるスワップファイル作成は伝統的な手法ですが、近年のディストリビューション（Ubuntu 22.04以降等）では `fallocate` コマンドの方が高速に処理できる場合があります。ファイルシステムがBtrfsの場合はスワップファイル作成に追加の考慮（Copy-on-Write無効化等）が必要になるため、事前にディストリビューション公式ドキュメントを確認してください。

---

## まとめ

- OOM Killerはメモリ枯渇時にプロセスを強制終了してシステム全体のクラッシュを防ぐカーネル機構。cgroup環境ではcgroup単位のOOM Killerも別途働く。
- 障害調査は `dmesg` / `journalctl` のキーワード検索（OOM / blocked / lockup / panic 等）が基本の切り分け手段。
- スワップ領域の追加は簡易な緩和策だが、根本対策は物理メモリ増設やメモリリークの特定・修正。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
