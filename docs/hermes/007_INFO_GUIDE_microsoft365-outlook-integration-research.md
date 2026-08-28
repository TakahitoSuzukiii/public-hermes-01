# Microsoft 365 / Outlook 連携 — 調査・検討記録(未実施・保留)

- **記録日:** 2026-08-28
- **ステータス:** 検討のみ完了。着手は保留(鈴木さん判断)
- **関連タスク:** #144「Microsoft連携: Outlookをoptimusに接続」(task-board、状態: on_hold)

## 背景・目的

Prime(Hermes Agent)にMicrosoft 365 / Outlookのメールアカウントを連携し、**読み取り専用(参照のみ)**でメール内容を扱えるようにしたいという要望があった。送信・書き込みなど外部への操作は行わない前提。

対象アカウントは `<your-email>`(Outlook形式)の**個人アカウント**(組織アカウントではない)。

## 調査結果

### 1. Hermes Agent公式ドキュメントでの対応状況

公式ドキュメント([Email | Hermes Agent](https://hermes-agent.nousresearch.com/docs/user-guide/messaging/email/))によると、Hermesには2つの異なるメール関連機能がある。

| 用途 | 使う機能 | 外部依存 |
|---|---|---|
| 人からのメールを受信し、Hermesが返信する(ゲートウェイ) | Emailゲートウェイアダプター(標準IMAP/SMTP、Python標準ライブラリのみ) | なし |
| エージェントがターミナルツールからメールボックスを操作(閲覧・整理等) | himalayaスキル | 外部CLI `himalaya` + 設定ファイル必須 |

今回の「読み取り専用で参照したい」という要望には、**himalayaスキル(IMAP読み取りのみで運用)** の方が用途に合致すると考えられる(ゲートウェイアダプターは「受信して自動返信する」用途がメインのため)。

### 2. Outlook / Microsoft 365 の認証方式

公式ドキュメントに明記されている手順:

1. Microsoftアカウントの[セキュリティ設定](https://account.microsoft.com/security)へアクセス
2. 2段階認証(2FA)を有効化(未設定の場合)
3. 「追加のセキュリティオプション」から**アプリパスワード**を新規作成
4. IMAPホスト: `outlook.office365.com`、SMTPホスト: `smtp.office365.com`

Microsoftは近年、IMAP/SMTP/POPに対するBasic認証(単純なパスワード直接入力)を段階的に廃止しており、**2FA有効化＋アプリパスワード発行**が事実上必須の接続方式になっている(Microsoft公式サポート情報より)。

### 3. 個人アカウント(Outlook.com/Hotmail.com/Live.com等)での連携可否

**結論: 連携可能。**

- Microsoft公式サポートページ「Settings for IMAP4 access to Microsoft personal email accounts」にて、`@outlook.com`/`@hotmail.com`/`@live.com`/`@msn.com`等の個人アカウントでのIMAP4アクセスが公式にサポートされていることを確認
- 組織アカウント(Microsoft 365 Business/Enterprise)向けの制約(管理者によるIMAP無効化等)は、個人アカウントには基本的に適用されない
- ただし、2FA未設定のまま接続しようとすると認証エラーになるケースが多数報告されており、**2FA＋アプリパスワードの組み合わせが前提**となる

## 検討した実現方針(案・未実施)

読み取り専用の方針に基づく想定構成:

1. 鈴木さんご本人が、対象Microsoftアカウントで2FA有効化・アプリパスワード発行を実施(パスワード管理に関わる操作のため本人実施必須)
2. himalayaスキル経由でIMAP接続のみを設定(SMTP送信設定は行わない、または無効化)
3. 認証情報(アプリパスワード)は `~/.hermes/.env` または himalaya設定ファイルにのみ保存し、ドキュメント・ログ・コミットには一切残さない
4. 受信トレイの一覧取得・閲覧など、読み取り系の動作確認のみ実施
5. 本ドキュメントを更新し、実施結果を追記

## 現状の判断

2026-08-28時点で、鈴木さんの判断により**着手は保留**。理由・再開時期の指定は特になし。再開する場合は task-board のタスク#144(状態: on_hold)を参照し、本ドキュメントの「検討した実現方針」に沿って進める想定。

## 参考リンク

- [Hermes Agent公式ドキュメント: Email](https://hermes-agent.nousresearch.com/docs/user-guide/messaging/email/)
- [Microsoft公式: Settings for IMAP4 access to Microsoft personal email accounts](https://support.microsoft.com/en-us/outlook/settings-for-imap4-access-to-microsoft-personal-email-accounts)
- [Microsoft公式: POP, IMAP, and SMTP settings for Outlook.com](https://support.microsoft.com/en-us/outlook/pop-imap-and-smtp-settings-for-outlook-com)
