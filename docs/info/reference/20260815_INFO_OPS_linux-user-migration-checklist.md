# Linuxユーザーアカウント移行チェックリスト(Amazon Linux 2 → Amazon Linux 2023)

> ステータス: INFO / カテゴリ: OPS / 作成日 2026-08-15
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP 等は placeholder（例: `<user>`）。
> 出典: 自己リポジトリ `public`(user-migration/) を再構成し、最新情報を検証のうえまとめ直したもの。

## 1. これは何か

Linux サーバーを移行する（例: Amazon Linux 2 → Amazon Linux 2023）際に確認すべき設定項目と、ユーザーアカウントを段階的に移行する手順のチェックリストです。踏み台サーバー経由で移行元・移行先へアクセスする構成を想定しています。

> 補足（最新情報の確認）: Amazon Linux 2（AL2）のサポート終了（EOL）は **2026年6月30日** です（AWS公式アナウンス）。この記事作成時点で既にEOLを迎えている、または間近に迫っている前提となります。AL2からの移行先は Amazon Linux 2023（AL2023）が公式に案内されており、AWSは2025〜2026年に新しいAmazon Linuxメジャーバージョンをリリースする予定はないとしています。AL2をまだ運用中の場合は、本チェックリストを参考に速やかな移行計画の実行を推奨します。

## 2. 移行の全体フロー

1. **設定確認**: 移行先（新規のAL2023）でバックアップを取得し、コマンドを実行して出力・エラーワードの有無を確認
2. **Linuxアカウント移行（テスト）**: 新規AL2023から特定の1ユーザー（例: `<user>`）を一旦削除し、踏み台経由で当該1ユーザーのみを移行（動作確認目的）
3. **設定確認（既存環境側）**: 既存のAL2でコマンドを実行し、出力・エラーワードを確認。同様に1ユーザーのみ踏み台経由で移行
4. **Linuxアカウント全体移行**: 踏み台でコマンドを実行し、出力・エラーワードを確認したうえで、既存AL2から新規AL2023へ全ユーザーを移行

段階的に「1ユーザーだけ試す→問題なければ全ユーザー」という進め方をすることで、移行時の事故を最小化します。

## 3. Linux設定確認チェックリスト

参考: [Linux OSを移行する時に確認する設定まとめ](https://dev.classmethod.jp/articles/linux-os-migration-checklist/)

### 3.1 基本情報

```bash
# OSバージョン
cat /etc/os-release

# カーネルバージョン
cat /proc/version
uname -a

# OSホスト名
cat /etc/hostname
hostnamectl
hostname
```

### 3.2 ネットワーク関連

```bash
# /etc/hosts
cat /etc/hosts

# 参照しているDNSサーバー
cat /etc/resolv.conf
dig

# /etc/nsswitch.conf（名前解決の順序設定）
cat /etc/nsswitch.conf

# NIC毎のIPアドレスとMTU
ip a
ifconfig -a  # 非推奨だが互換のため併記

# 静的ルート
ip route show
ip route show table all
```

> 補足: `ifconfig` / `netstat` は net-tools パッケージに含まれる旧来のコマンドで、近年の多くのディストリビューションでは非推奨（deprecated）扱いです。代わりに iproute2 パッケージの `ip` / `ss` コマンドの利用が推奨されます（Amazon Linux 2023ではデフォルトで net-tools が含まれない場合があるため注意）。

※ Route 53 Resolver を使用する予定の場合は、現在参照している DNS サーバーの条件付きフォワーダーも確認しておくと良い。

### 3.3 時刻・ロケール

```bash
# 参照しているNTPサーバー
chronyc sources -v
cat /etc/chrony.conf

# タイムゾーン
cat /etc/localtime
timedatectl
date

# システムロケール
cat /etc/locale.conf
localectl
```

### 3.4 ストレージ

```bash
# マウントしている領域
cat /etc/fstab
df -h
findmnt
mount

# デバイスパーティション
parted -l
lsblk

# swap設定
swapon -s
cat /proc/swaps
```

### 3.5 ユーザー・権限

```bash
# OSユーザーとOSグループ
cat /etc/passwd
cat /etc/group

# sudoers設定
cat /etc/sudoers
ls -lR /etc/sudoers.d/

# 各OSユーザーの環境変数・エイリアス設定
ls -l /home/*/.bash*
```

※ `/home` 配下は個々のユーザーの設定を含むため、必要に応じて `tar` で固めてバックアップすることを推奨。

### 3.6 SSH / PAM

```bash
cat /etc/ssh/sshd_config
ls -l /home/*/.ssh/authorized_keys

# PAM設定
ls -l /etc/pam.d
cat /etc/pam.d/sshd
```

### 3.7 サービス・起動設定

```bash
# 有効化されているサービスの一覧確認
for service in $(systemctl list-unit-files --type=service --no-legend | awk '{print $1}'); do
    current=$(systemctl list-unit-files "$service" --no-legend | awk '{print $2}')
    printf "%-40s %-15s\n" "$service" "$current"
done

ls -l /etc/systemd/system
```

### 3.8 その他の確認項目

```bash
# プロセス一覧
ps -ej uf

# 使用しているポート一覧
ss -antup

# logrotate / rsyslog
cat /etc/logrotate.conf
cat /etc/rsyslog.conf

# cron・systemd-timer
cat /var/spool/cron/*
systemctl list-timers

# ファイアウォール（iptables / firewalld）
iptables -L
firewall-cmd --state

# SELinux
getenforce
sestatus

# 参照しているリポジトリ
dnf repolist -v

# カーネルパラメーター
cat /etc/sysctl.conf
sysctl -a

# リソース制限
cat /etc/security/limits.conf
```

## 4. バックアップ

移行前に以下を必ずバックアップします。

**グループ1（アカウント関連ファイル）**
- `/etc/passwd`
- `/etc/group`
- `/etc/shadow`
- `/etc/gshadow`

**グループ2（ユーザーデータ）**
- `/home/<user>` ディレクトリ
- `/var/spool/mail` ディレクトリ

> 補足: `/etc/shadow` / `/etc/gshadow` にはパスワードハッシュが含まれるため、バックアップファイルの保管・転送経路は暗号化・アクセス制限を徹底してください（機密情報として扱う）。

## 5. ユーザーアカウント移行手順

### 5.1 差分の抽出

既存環境と新規環境の `/etc/passwd` の差分を確認し、移行したいアカウントのみを抽出したファイルを作成します（例: `etc_passwd_migration<YYYYMMDD>.txt`）。

### 5.2 新規サーバーへの反映

```bash
# passwdへの追記
cat etc_passwd_migration<YYYYMMDD>.txt >> /etc/passwd

# shadowの更新（追記したユーザー分のシャドウエントリを生成）
pwconv

# 整合性チェック
pwck
```

同様に `/etc/group` についても差分抽出 → 追記 → `grpconv` → `grpck` の手順で移行します。

## 6. 20250502追記: ネットワーク確認コマンド集

```bash
ip
ip route
ip neigh
ss

ip a
ip addr show
ip route show
ip neigh show
netstat -antup  # 非推奨、ssコマンド推奨
```

## 7. まとめ

Linuxサーバーの移行、特にユーザーアカウントの移行は「①事前の設定確認とバックアップ → ②1ユーザーでのテスト移行 → ③問題なければ全ユーザー移行」という段階的なアプローチが安全です。特に `/etc/shadow` を含むバックアップの取り扱いと、移行後の `pwck`/`grpck` による整合性確認は省略しないようにしましょう。

Amazon Linux 2 は2026年6月30日にEOLを迎えているため、本記事の内容は移行計画の初期チェックリストとして活用してください。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
