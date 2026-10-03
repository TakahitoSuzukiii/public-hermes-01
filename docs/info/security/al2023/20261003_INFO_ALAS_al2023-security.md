# AL2023 セキュリティアドバイザリ週次レポート（2026-10-03）

作成日: 2026-10-03 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 1 |
| Important | 84 |
| Medium | 4 |
| Low | 1 |

対象期間: 2026-09-26 〜 2026-10-03

> ⚠️ 今週も Important 案件が非常に多く（84件）、その大半は kernel-livepatch（カーネルの再起動なしパッチ適用機能）の個別ビルド向けアドバイザリです。詳細取得には上限（30件）があるため、reportable（Critical+Important）85件のうち先頭30件のみ詳細を取得しています（`reportableTruncated=true`）。

---

## 注目アドバイザリ（重大度順）

### 1. ALAS2023-2026-3149（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3149.html)） — Critical

- **重大度:** Critical（緊急）
- **対象パッケージ:** amazon-ssm-agent（AWS Systems Manager Agent。EC2インスタンス等をリモート管理するためのエージェント）
- **関連 CVE（共通脆弱性識別子）:** CVE-2026-42505, CVE-2026-71556, CVE-2026-71557, CVE-2026-89049
- **概要:** ECH（Encrypted Client Hello、TLSハンドシェイクの暗号化拡張）を使った通信が、暗号化されないクライアントハロー内に事前共有鍵（PSK）の識別子が漏れていたことで、通信を傍受する第三者（パッシブな観測者）に匿名性を破られる恐れがありました（CVE-2026-42505）。また、go-git（Go言語で書かれたgit実装ライブラリ、バージョン5.19.2/6.0.0-alpha.5未満が対象）には、ワークツリー操作（checkout・status・add等）がシンボリックリンクの解決をワークツリーの範囲内に限定していない問題があり、悪意あるリポジトリをクローンして操作すると、意図したディレクトリ外のファイルを読み書きされる恐れがありました。
- **対処方法:** `sudo dnf check-release-update` および `sudo dnf update amazon-ssm-agent` 等による更新が必要です。本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドの実行は行っておりません。実際の適用は管理者権限を持つ方が実施してください。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3149.html

### 2. kernel-livepatch 関連アドバイザリ群（Important、30件）

今週の Important のうち詳細取得済み分はすべて、kernel-livepatch（Linux カーネルを再起動せずにパッチ適用する仕組み）の各カーネルビルド版に対する個別アドバイザリです（ID 例: `ALAS2023LIVEPATCH-2026-389` 〜 `418`）。対象パッケージ名（`kernel-livepatch-<バージョン>`）はカーネルビルドごとに異なりますが、修正内容は今週取得分すべてが同一のCVEでした。

- **CVE-2026-80521:** Linux カーネルの af_unix（UNIXドメインソケット関連サブシステム）で、`unix_del_edge()` 処理時に SCC（強連結成分、ソケット間の循環参照検出に使うデータ構造）エントリのリンク解除漏れがあり、不整合な状態を引き起こす恐れがある不具合。
- **対処方法:** livepatch は通常、`sudo yum update` や livepatch 管理コマンドの実行環境で自動適用される運用が一般的ですが、本タスクは情報収集のみを目的としており `sudo` を要するコマンドの実行は行っておりません。実際の適用状況・要否は管理者権限を持つ方が確認してください。
- **出典（代表）:** https://alas.aws.amazon.com/AL2023/ALAS2023LIVEPATCH-2026-389.html （他、`390`〜`418` 番台に同種のアドバイザリが多数存在）

> 上記2件で詳細取得済み30件のうち29件（kernel-livepatch）＋1件（Critical本体）をカバーしています。残る55件（reportable 85件 − 詳細取得30件）は今回のツール制約上、個別の詳細を取得できていません。次回以降の取得上限調整、または AWS 公式の該当週まとめページでの確認を推奨します。

---

## その他

- Medium: 4件（libssh, ImageMagick, libxml2, awscli-2）/ Low: 1件（amazon-efs-utils）※いずれも件数のみの記録で詳細は割愛
- 一覧の切り詰め（truncated）: あり。reportable（Critical+Important）85件のうち、詳細取得は先頭30件までです。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
