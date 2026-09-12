# AL2023 セキュリティアドバイザリ週次レポート（2026-09-12）

作成日: 2026-09-12 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 0 |
| Important | 2 |
| Medium | 0 |
| Low | 0 |

対象期間: 2026-09-05 〜 2026-09-12

---

## 注目アドバイザリ（重大度順）

### 1. ALAS2023-2026-2130（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2130.html)）

- **重大度:** Important（重要）
- **対象パッケージ:** nginx
- **関連 CVE（共通脆弱性識別子）:** 記載なし（本アドバイザリでは個別の CVE 番号が未公開）
- **概要:** nginx に HTTP/2 のサービス拒否（DoS: Denial of Service、サーバを応答不能にさせる攻撃）の脆弱性が発見されました。修正前は、クライアントが送信できるリクエストヘッダー数に制限がなく、攻撃者が HPACK（HTTP/2 のヘッダー圧縮方式）動的テーブルに1つのヘッダーを仕込んだ後、大量のインデックス参照ヘッダーを送りつけることで、サーバ側の処理負荷を異常に増大させる可能性がありました。
- **対処方法:** `sudo dnf check-release-update` および `sudo dnf update nginx` 等による更新が必要です。本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドの実行は行っておりません。実際の適用は管理者権限を持つ方が実施してください。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2130.html

### 2. ALAS2023-2026-2131（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2131.html)）

- **重大度:** Important（重要）
- **対象パッケージ:** containerd（コンテナランタイム）
- **関連 CVE:** CVE-2026-10722, CVE-2026-39822, CVE-2026-42505
- **概要:** containerd の CRI（Container Runtime Interface）プラグインにおいて、チェックポイント・リストア（コンテナの状態保存・復元機能）がセキュリティコンテキストのチェックを回避してしまう問題（GHSA-p7v4-vr35-mj6f）が修正されました。また CVE-2026-10722 は cilium ebpf（0.21.0 以下）の `loadRawSpec` 関数に起因する整数オーバーフロー（数値が扱える範囲を超えてしまう不具合）で、ローカル環境からのみ悪用可能とされていますが、既に攻撃コードが公開されており悪用のリスクがあります。パッチ（修正差分）は既に適用済みとして公開されています。加えて、Unix 系システムで `os.Root` 使用時にシンボリックリンク（別ファイルへの参照）を不適切にたどってしまう問題も含まれています。
- **対処方法:** `sudo dnf check-release-update` および `sudo dnf update containerd` 等による更新が必要です。本タスクは情報収集のみを目的としており、`sudo` を要するコマンドの実行は行っておりません。実際の適用は管理者権限を持つ方が実施してください。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-2131.html

---

## その他

- Medium: 0件 / Low: 0件（今週は該当なし）
- 一覧の切り詰め（truncated）: なし（すべてのCritical/Importantアドバイザリを掲載済み）

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
