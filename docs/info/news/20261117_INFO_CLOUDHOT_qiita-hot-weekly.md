作成日: 2026-11-17 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-10〜2026-11-17

# Qiita クラウド人気記事 週報（AWS / Google Cloud / Azure / Cloudflare）

## 📌 今週のハイライト
- AWS は新着の走査件数が多く、いいね・ストックとも他3分野を大きく上回った。「AWS Emulator（AWSをローカルで模擬する仕組み）で CDK/Terraform（コードでインフラを構築するツール）がどこまで動くか」という検証記事が突出。
- AI 関連（RAG＝検索で補強した生成AI、Claude、Gemini）とクラウドを組み合わせた話題が各分野で目立つ。
- Google Cloud は新しい Gemini モデル（Gemini 4 シリーズ）の速報・比較記事が複数出ている。
- Azure と Cloudflare は今週の反応（いいね）が少なめ。Azure は Azure Files 同期や入門記事、Cloudflare は Workers／Zero Trust／メール受信の個人開発事例が中心。
- セキュリティ寄りの話題（脆弱性対応など）が定番に入っているが、詳細・スコアは CISA／JPCERT 週報を参照。

## 🔥 今週これだけ読む3本
1. **【AWS】AWS EmulatorでCDK/Terraformのスタックはどこまで動くか** — いいね51／ストック28。今週の新着で最も反応が大きく、ローカル検証の実用度が分かる。
   https://qiita.com/Nana_777/items/3f3c71525d867b22c9f2
2. **はじめてのAPIログ設計 — 「ログはあるのに調べられない」を防ぐには？** — いいね21／ストック3。クラウド運用で誰もが困る「ログ設計」の入門。
   https://qiita.com/masashige0904/items/22f2836485ecc25ee527
3. **AWSでゼロトラスト構成を作る手順を5つのパートに分けて整理してみた** — いいね12／ストック9。ゼロトラスト（「社内だから安全」とせず常に検証する考え方）を段階的に整理。
   https://qiita.com/yama3133/items/11a360fc97ed3ec09742

## 📝 タグ別ホット記事（直近7日）
※数値は取得時点（2026-11-17）の値。

### AWS（新着176件から選定／宣伝色・無関係な記事を中心に一部除外）
- **AWS EmulatorでCDK/Terraformのスタックはどこまで動くか**（いいね51/ストック28/2026-11-12）— AWS模擬環境でIaCの再現度を検証。https://qiita.com/Nana_777/items/3f3c71525d867b22c9f2
- **社長の一言は重い。RAGにも忖度させてみた（重み付け検索）**（19/6/11-15）— RAGの検索結果に重みを付ける試み。https://qiita.com/kikuziro/items/43b360420d0cdcbf190c
- **はじめてのAPIログ設計**（21/3/11-16）— 調べられるログの設計観点。https://qiita.com/masashige0904/items/22f2836485ecc25ee527
- **AWSでゼロトラスト構成を作る手順を5つのパートに分けて整理してみた**（12/9/11-14）— 構成手順の整理。https://qiita.com/yama3133/items/11a360fc97ed3ec09742
- **Q Developer 改め AWS assistantに、共用アカウントの「お金の犯人」を聞いてみた**（8/7/11-11）— AIアシスタントでコスト増の原因調査を試す。https://qiita.com/N-Kyo/items/e795b22a860566bc7b5b

### Google Cloud（新着25件から選定／ホット15件中、低反応・重複を除外）
- **PRの脆弱性をAIが直す「CodeMender」を見て、新卒が基礎を学ぶ理由を考えた**（9/8/11-12）— AIによる自動修正と基礎学習の関係を考察。https://qiita.com/N-Kyo/items/23697fc1e92c288b426b
- **【速報】Google「Gemini 4 Hydrogen」登場！…Gemini 4 シリーズまとめ**（4/1/11-16）— 新モデル群の比較。https://qiita.com/tomokoro/items/41cc59d0085fa03c5d52
- **【Gemini Flashシリーズの最新モデル】Gemini 4 Hydrogenとは？**（4/1/11-13）— 使ってみた結果・料金・Google Cloud対応。https://qiita.com/kentaro_kawamura/items/2d1a2f8196d0b89c0cbe
- **【AWS/GCP/Azure】オブジェクトストレージの11ナイン「実装の差」から「思想の違い」をまとめてみた**（1/0/11-16）— 11ナイン（99.999999999%の耐久性）の考え方比較。https://qiita.com/kaga-yasumitsu/items/ec09bbcd1b71c1af292a
- **BigQueryのテーブルをコマンド1つで別リージョンへコピーする**（0/0/11-16）— エクスポート不要のコピー方法。https://qiita.com/motuneko253/items/9381bd569aa81e511d64

### Microsoft Azure（新着28件から選定／広告的な内容・重複を一部除外）
- **Azure Files 間のデータ同期ができるようになったので触ってみた**（2/0/11-15）— 新機能の試用。https://qiita.com/iboy/items/bf39c22f2337deeaf439
- **【初心者向け】Azureとは何か？…基本サービスをわかりやすく解説**（0/1/11-16）— 入門。https://qiita.com/omochidafuku/items/90887e2e24194b070c67
- **【AWS/GCP/Azure】オブジェクトストレージの11ナイン…**（1/0/11-16）— 上記と同記事。https://qiita.com/kaga-yasumitsu/items/ec09bbcd1b71c1af292a
- **Microsoft Agent Framework ワークショップを v1.13.0 から v1.23.0 へ更新**（1/0/11-10）— AIエージェント開発教材の更新。https://qiita.com/nohanaga/items/0b55a722445a0981f373
- **Terraform Enterpriseを触ってみた -ローカルCLIからRemote Plan編-**（0/0/11-16）— Terraform の実行をリモート化する検証。https://qiita.com/gKhdrt_chan/items/83c27d442b732c554583

### Cloudflare（新着25件から選定／無関係な記事を除外）
- **Hono の JSX と古風なデザインで JavaScript を送らない爆速カタログサイトを作った**（3/0/11-10）— 軽量Webフレームワーク Hono でのサイト構築。https://qiita.com/AllegroMoltoV/items/d9ec82346a035b32285f
- **【個人開発】第1回：Cloudflareで独自ドメインのメール受信環境を構築する！**（2/0/11-13）— Workers でメール受信を確認するまで。https://qiita.com/kandu/items/73bfa5a8d2aedd3c0dd4
- **WordPressをAWSに組んだ（Spot・大阪/ムンバイ冗長・R2バックアップ）**（1/0/11-15）— AWS と Cloudflare R2 の組み合わせ事例。https://qiita.com/hayahide23/items/938c9d78e1d60ba96cf1
- **Workers AI の無料枠の7割で止める設計メモ**（1/0/11-14）— 無料枠を超えない振り分け設計。https://qiita.com/ishizakahiroshi/items/86662cb04a5607eb2f7e
- **ネットワーク境界の再構築：CGNAT突破とCloudflare Zero Trust二重化トンネル**（0/1/11-10）— ポート開放なしの接続構成。https://qiita.com/ubinity/items/97d6164ba34e103d2383

## 📚 定番（直近30日・ストック20以上）
### AWS
- **PHP脆弱性php2shell対応、7.4本番を止めずに守った夜と実際の攻撃**（ストック189）— 脆弱性の詳細・スコアは CISA／JPCERT 週報を参照。https://qiita.com/kenimo49/items/30f290bf0f4fff021fb3
- **AI駆動開発の次の段階: ソフトウェアファクトリー**（ストック96）https://qiita.com/Syoitu/items/9364a0a175893bb15219
- **集中力散漫＆過集中持ちエンジニアがAWS DEAを突破した「過集中スイッチ」の入れ方**（ストック61）— DEA は AWS 認定 Developer Associate 試験。https://qiita.com/kohYoung_I/items/cce40cb5b9cdfc1f8787
### Google Cloud / Microsoft Azure / Cloudflare
- 該当なし

## ℹ この記事の見方
- 「いいね」「ストック（後で読むための保存）」は**取得時点（2026-11-17）の値**です。人気の目安であり、正確性・品質を保証するものではありません。
- ホットは直近7日の新着をいいね＋ストック順、定番は直近30日でストック20以上の記事です。
- 各記事は題名・公開情報から要約しており、本文の全文は転載していません。
- 取得できなかった情報源: なし。

## 出典
- Qiita API v2（公式）: https://qiita.com/api/v2/docs

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
