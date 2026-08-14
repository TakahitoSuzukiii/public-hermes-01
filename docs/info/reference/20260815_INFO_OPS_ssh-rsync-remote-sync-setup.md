# SSH/rsyncによるリモート環境間ファイル同期の基本セットアップ

> ステータス: INFO / カテゴリ: OPS / 作成日 2026-08-15
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP 等は placeholder。
> 出典: 自己リポジトリ `public`(ssh/) を再構成し、最新情報を検証のうえまとめ直したもの。

## 1. これは何か

SSH 経由でリモートサーバーとファイルを同期する（`rsync` / `WinSCP` を使う）際の、最低限必要なセットアップ手順のメモです。初めてリモートサーバーへの同期環境を構築する際のチェックリストとして使えます。

## 2. リモート側の準備

### 2.1 SSHサーバーのインストール・起動

```bash
sudo apt update
sudo apt install openssh-server
sudo service ssh start
```

> 補足: 上記は Debian/Ubuntu 系のコマンド例です。Amazon Linux 2023 など RHEL 系ディストリビューションでは `dnf install openssh-server` かつ `systemctl start sshd`（サービス名が `sshd` である点に注意）となります。また近年の systemd 環境では `service` コマンドより `systemctl` の利用が推奨されています。

### 2.2 SSH関連ディレクトリ/ファイルの権限設定

`~/.ssh` ディレクトリと `authorized_keys` ファイルは、パーミッションが緩いと SSH がログインを拒否する仕様になっているため、以下のように厳格に設定する必要があります。

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

- `~/.ssh`: 所有者のみ read/write/execute 可能（700）
- `authorized_keys`: 所有者のみ read/write 可能（600）

### 2.3 rsync のインストール

```bash
sudo apt update
sudo apt install rsync
```

rsync は SSH をトランスポート層として利用してファイルを転送するため、リモート側にも rsync 本体がインストールされている必要があります（ローカル・リモート双方に rsync が必要）。

### 2.4 接続確認

```bash
ssh user@remote
```

`user@remote` の部分は実際のユーザー名・ホスト名に置き換えてください。公開鍵認証を使う場合は、事前にリモート側の `~/.ssh/authorized_keys` へ公開鍵を登録しておきます。

### 2.5 転送先ディレクトリの権限確認

```bash
chmod 755 /remote/destination
```

書き込み先ディレクトリに適切な権限が付与されているか確認します。

## 3. 同期コマンドの例

### 3.1 rsync でのリモート同期

```bash
rsync -avPzh --delete /local/source/ user@remote:/remote/destination/
```

主なオプションの意味:

| オプション | 意味 |
|---|---|
| `-a` | アーカイブモード（パーミッション・タイムスタンプ等を保持し再帰的にコピー） |
| `-v` | verbose（詳細出力） |
| `-P` | 進捗表示 + 中断時の再開を可能にする（`--partial --progress` の短縮） |
| `-z` | 転送時に圧縮 |
| `-h` | 数値を人間が読みやすい単位で表示 |
| `--delete` | 転送先にのみ存在するファイルを削除し、送信元と完全一致させる（**破壊的操作のため注意**） |

> 注意: `--delete` オプションは転送先の余分なファイルを削除する破壊的な操作です。誤って送信元・宛先を逆に指定すると、データを失う可能性があります。初回実行時は `--dry-run`（`-n`）オプションを併用し、実際に削除・上書きされるファイルを事前確認することを強く推奨します。

### 3.2 WinSCP でのリモート同期（Windows環境向け）

```cmd
winscp.com /command "open sftp://user@remote" "synchronize remote C:\local\source /remote/destination" "exit"
```

WinSCP のコマンドラインインターフェース（`winscp.com`）を使うと、GUIを介さずスクリプトから同期処理を実行できます。Windows のタスクスケジューラ等と組み合わせた定期同期の構築にも利用できます。

> 補足（最新情報の確認）: rsync・OpenSSH・WinSCP はいずれも2026年時点で活発にメンテナンスが続いているOSS/フリーソフトウェアです。rsync は将来的に `rsync://` プロトコルではなく SSH トランスポートの利用が主流であり、本記事の手順もその前提に沿っています。セキュリティの観点では、パスワード認証よりも公開鍵認証（可能であれば ed25519 鍵）の利用が推奨されます。

## 4. まとめ

SSH+rsync によるファイル同期の最小構成は「①リモート側にSSHサーバーとrsyncを用意する → ②鍵/権限を正しく設定する → ③接続確認 → ④同期コマンドを実行する」という4ステップです。`--delete` を使う破壊的同期は特に事前のドライラン確認を徹底しましょう。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
