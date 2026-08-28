# 技術検討: Home Assistant Companionアプリ（2026-08-28）

## これは何か

**Home Assistant**は、自宅に設置したサーバー（PCやRaspberry Pi等）上で動く、オープンソースのスマートホーム統合プラットフォームです。「Home Assistant Companionアプリ」は、そのHome Assistant本体とスマートフォンを連携させるための公式モバイルアプリ（Android/iOS対応、無料）で、スマホの各種センサー（位置情報、バッテリー残量、通知等）をHome Assistant本体に取り込んだり、逆にHome Assistant側からスマホへ通知・操作指示を送ったりする「橋渡し役」です。

Home Assistant本体は自前でホストする必要があり（自宅のPCやサーバーに構築）、Companionアプリ単体では完結しません。

## どんな機能を実現するものか

| 機能カテゴリ | 内容 |
|---|---|
| 通知連携 | Home Assistant側からスマホへプッシュ通知を送信（クリック時のアクション設定も可能） |
| センサー連携 | 位置情報、バッテリー残量、Wi-Fi接続状態などをHome Assistant側で取得・自動化に利用 |
| **音声アシスタント（Assist）** | Home Assistant独自の音声アシスタント機能。**2026年3月のアップデートで、スマホ単体でのオンデバイス・ウェイクワード検出**に対応（「OK Nabu」等のフレーズで起動、カスタムフレーズも学習可能） |
| ウィジェット・自動化 | ホーム画面ウィジェットからの操作、位置情報に基づく自動化（帰宅検知等） |

## 今回のユースケース（本タスクでの使い方）

「Get up Optimus」のようなカスタムフレーズをBluetoothイヤホン越しに話しかけると、Home Assistant Companionアプリがオンデバイスでこれを検出し、Home Assistant本体（自宅PC上のDockerコンテナ）へ音声を送信、そこから`webhook-conversation`というカスタム統合を経由してHermes Agent（Optimus）へ処理を委譲し、音声で応答を受け取る——という構成の「入口（ウェイクワード検出センサー）」として活用します。

## 導入の条件・制約

| 項目 | 内容 |
|---|---|
| 必要なもの | Home Assistant本体の稼働環境（自宅PCにDocker等で新規構築）、Companionアプリ（Android/iOS、無料） |
| 対応OS | Android / iOS 双方対応。最新のAndroidバージョンであれば問題なし |
| ネットワーク | スマホ⇄Home Assistant本体間の通信経路が必要（今回Tailscale経由を想定） |
| カスタムウェイクワード | 標準搭載の「OK Nabu」以外を使う場合、openWakeWord Training Center等で独自モデルを学習する追加作業が必要（数分〜、精度チューニングに数回の試行を要する場合あり） |

## 導入時のデメリット・リスク

- **新規ミドルウェアの追加**: Home Assistant本体を新たに自宅PCへ構築する必要があり、以降の保守対象（アップデート・セキュリティパッチ管理）が1つ増える
- **セットアップの複雑さ**: Home Assistant本体の構築＋`webhook-conversation`統合の導入＋Hermes側のwebhook設定と、複数コンポーネントの連携設定が必要
- **カスタムフレーズの精度**: 独自のウェイクワードフレーズは、標準搭載フレーズに比べ誤検出・未検出が発生しやすく、チューニングが必要になる場合がある

## 運用時のデメリット・リスク

- **常時マイクON**: バックグラウンドで常時、ウェイクワード検出のためマイクを監視する状態になる（音声自体はオンデバイス処理のみで外部送信されないが、常駐処理としてスマホのバッテリー消費が増える。目安としてはGoogleアシスタント等の常時待ち受け機能と同程度）
- **Home Assistant本体の可用性依存**: 自宅PCが停止・再起動中は、ウェイクワード起動機能も一時的に使えなくなる
- **アップデートの影響**: Home Assistant・Companionアプリ・`webhook-conversation`統合のいずれかがアップデートで仕様変更された場合、連携が壊れる可能性がある（コミュニティ製の統合であるため、公式サポートの保証はない）

---

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
