# AL2023 セキュリティアドバイザリ週次レポート（2026-09-19）

作成日: 2026-09-19 / STATUS: INFO / TOPIC: ALAS / 対象: Critical+Important

> ALAS（Amazon Linux Security Advisory、Amazon Linux セキュリティ勧告）は、AWS が提供する Amazon Linux 2023（AL2023）向けのセキュリティ情報です。本レポートは AWS 公式 ALAS RSS フィードを情報収集目的で監視した結果をまとめたものです。

## 今週の新規アドバイザリ件数（重大度別）

| 重大度 | 件数 |
|---|---|
| Critical | 1 |
| Important | 86 |
| Medium | 9 |
| Low | 2 |

対象期間: 2026-09-12 〜 2026-09-19

> ⚠️ 今週は Important 案件が異例に多く（86件）、その大半は kernel-livepatch（カーネルの再起動なしパッチ適用機能）の個別ビルド向けアドバイザリです。詳細取得は上限30件までのため、reportable（Critical+Important）87件のうち先頭30件のみ詳細を取得しています（`reportableTruncated=true`）。

---

## 注目アドバイザリ（重大度順）

### 1. ALAS2023-2026-3101（[リンク](https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3101.html)） — Critical

- **重大度:** Critical（緊急）
- **対象パッケージ:** unbound（DNS キャッシュサーバ／リゾルバ）
- **関連 CVE（共通脆弱性識別子）:** CVE-2026-81642
- **概要:** NLnet Labs Unbound（バージョン 1.26.0 以下）の DNSSEC（DNS Security Extensions、DNS 応答の改ざん検知の仕組み）バリデータに脆弱性が見つかりました。DNSKEY レコード（DNSSEC で使う公開鍵情報）が自身のデータ領域を指す圧縮ポインタを持つ場合、ダイジェスト（ハッシュ値計算用）バッファがオーバーフロー（許容量を超えてはみ出す）する可能性があります。悪意あるゾーン（DNS の管理領域）を用意した攻撃者が、脆弱な Unbound に問い合わせをさせることで、サービス拒否（DoS）や、条件次第ではリモートコード実行（攻撃者が任意のコードを実行できる状態）にまで至る恐れがあります。
- **対処方法:** `sudo dnf check-release-update` および `sudo dnf update unbound` 等による更新が必要です。本タスクは情報収集のみを目的としており、`sudo`（管理者権限）を要するコマンドの実行は行っておりません。実際の適用は管理者権限を持つ方が実施してください。
- **出典:** https://alas.aws.amazon.com/AL2023/ALAS2023-2026-3101.html

### 2. kernel-livepatch 関連アドバイザリ群（Important、29件）

今週の Important の大半は、kernel-livepatch（Linux カーネルを再起動せずにパッチ適用する仕組み）の各カーネルビルド版に対する個別アドバイザリです（ID 例: `ALAS2023LIVEPATCH-2026-360` 〜 `388`）。対象パッケージ名（`kernel-livepatch-<バージョン>`）はカーネルビルドごとに異なりますが、修正内容は概ね以下2種類のCVEの組み合わせです。

- **CVE-2026-80844:** Linux カーネルの xfrm（IPsec 関連サブシステム）ah6（IPv6 用 AH: Authentication Header プロトコル）処理で、ルーティングヘッダーの `segments_left`（残りセグメント数）フィールドの検証不備。
- **CVE-2026-81000:** Linux カーネルの tun（仮想ネットワークデバイス）ドライバで、受信ヘッダー用の余白（headroom）サイズが未検証な問題。
- 一部ビルド（`ALAS2023LIVEPATCH-2026-366`以降）は、さらに以下2件も含みます:
  - **CVE-2026-68121:** pppoe（PPP over Ethernet）で `dev_hard_header()` 呼び出し後にヘッダーポインタを再読込していない不具合。
  - **CVE-2026-74469:** sctp（Stream Control Transmission Protocol）でピア（接続相手）のトランスポート数がオーバーフローしうる不具合。
- **対処方法:** livepatch は通常、`sudo yum update` や livepatch 管理コマンドの実行環境で自動適用される運用が一般的ですが、本タスクは情報収集のみを目的としており `sudo` を要するコマンドの実行は行っておりません。実際の適用状況・要否は管理者権限を持つ方が確認してください。
- **出典（代表）:** https://alas.aws.amazon.com/AL2023/ALAS2023LIVEPATCH-2026-360.html （他、`361`〜`388` 番台に同種のアドバイザリが多数存在）

> 上記2件で詳細取得済み30件のうち29件（kernel-livepatch）をカバーしています。残る57件（reportable 87件 − 詳細取得30件）は今回のツール制約上、個別の詳細を取得できていません。次回以降の取得上限調整、または AWS 公式の該当週まとめページでの確認を推奨します。

---

## その他

- Medium: 9件（例: valkey, cups-filters, nerdctl, curl, libheif, runc, nodejs24, jsoup, composer）/ Low: 2件（mount-s3, perl-Socket）※いずれも件数のみの記録で詳細は割愛
- 一覧の切り詰め（truncated）: あり。reportable（Critical+Important）87件のうち、詳細取得は先頭30件までです。

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
