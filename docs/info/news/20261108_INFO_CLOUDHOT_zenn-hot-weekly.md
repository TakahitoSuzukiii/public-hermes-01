作成日: 2026-11-08 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-01〜2026-11-08

# Zenn クラウド人気記事 週報（2026-11-08）

## 📌 今週のハイライト
- AWS は「サーバーレス移行によるコスト削減」「Web公開時の守り方（オリジン保護）」「Bedrock AgentCore（AIエージェント基盤）」が目立ちました。
- Azure 分野では Microsoft Foundry の Copilot Harness と GitHub Copilot のモデル自動ルーティング（Fusion）など、AI 関連が上位でした。
- Google Cloud は個別技術（DLP＝機密情報検出、IAM ロール移行）に加え、3大クラウドのシェア動向を論じた記事が注目されました。
- Cloudflare は週刊まとめと、Workers を使った自動化・セキュリティ点検系の記事が中心です（いいね数は全体に小さめ）。

## 🔥 今週これだけ読む3本
1. **ECS + RDS → Lambda + Aurora DSQL の移行で社内アプリのインフラ費用がほぼゼロになった話**（18いいね）— 全分野で最多。具体的な移行と費用削減の事例。
   https://zenn.dev/wogo_techblog/articles/4c21661707f8c8
2. **AWSでWebリクエストを受ける8パターンと「オリジンを裸にしない」設定プラクティス**（16いいね）— 公開構成の選択肢と守り方を整理した、実務で役立つ内容。
   https://zenn.dev/anfangd/articles/aws-web-ingress-origin-protection
3. **Microsoft Copilot Harness が Foundry にきた！ハーネスって何？何が嬉しいの？**（15いいね）— 新機能を入門的に解説。Azure 分野の最多。
   https://zenn.dev/nomhiro/articles/microsoft-copilot-harness-foundry

## 💬 トピック別ホット記事
（いいね数は取得時点の値。複数の分野に出た同一記事は最も関連の深い節にのみ掲載）

### AWS（新着100件から選定／除外2件：分野違い・関連が薄いもの）
- ECS + RDS → Lambda + Aurora DSQL の移行（18／2026-11-04）— コンテナ+RDS構成からサーバーレス構成へ移し費用を削減した事例。 https://zenn.dev/wogo_techblog/articles/4c21661707f8c8
- AWSでWebリクエストを受ける8パターンと「オリジンを裸にしない」設定プラクティス（16／2026-11-06）— 受け口の構成パターンと、直接アクセスを防ぐ設定の紹介。 https://zenn.dev/anfangd/articles/aws-web-ingress-origin-protection
- 逆引き！ Bedrock AgentCore gateway ユースケース38選（9／2026-11-05）— AIエージェント基盤の Gateway 機能を用途別に整理。 https://zenn.dev/aws_japan/articles/agentcore-gateway-usecase-reverse-lookup
- aidlc-workflowsのbugfixスコープでバグ修正してみた（9／2026-11-05〜06）— AI主導の開発手法でバグ修正を行った記録。 https://zenn.dev/canly/articles/5056c5ca674e80
- Security Hub の SBOM インベントリで、Athena を使わずに組織全体のソフトウェアを調べてみた（8／2026-11-06）— SBOM（ソフトウェア部品表）を Security Hub で確認する方法。 https://zenn.dev/cscloud_blog/articles/securityhub-sbom-inventory

### Google Cloud（走査24件／除外2件：他分野の記事・関連が薄いもの）
- PII検出導入にあたって、DLP の likelihood を深掘りしてみた（12／2026-11-06）— 機密情報検出 API の「確からしさ」指標の挙動を検証。 https://zenn.dev/actbe_tech/articles/d9b796184277e3
- 3大クラウドで市場に勝ったのはGoogleだけ（6／2026-11-06）— クラウド市場でのシェア動向を論じた記事。 https://zenn.dev/acntechjp/articles/zenn-gcp-cloud-share-why-growing
- Editorはもう古い。新ロールへ安全に移る768試行（4／2026-11-04）— 基本ロール（Editor）から細かいロールへ移行する検証。 https://zenn.dev/acntechjp/articles/zenn-gcp-basic-roles-migration
- Weekly Google Cloud アップデート情報 - 2026年11月3日（4／2026-11-03）— 週次の更新情報まとめ。 https://zenn.dev/softbank/articles/16e8c12c4da944
- Bigtableへのバッチ書き込みをValkeyで制御する（3／2026-11-06）— 書き込み量の制御にValkey（Redis互換）を使う設計。 https://zenn.dev/dmmdata/articles/bigtable-batch-write-rate-limiting

### Microsoft Azure（走査14件／除外2件：他クラウド記事・重複）
- Microsoft Copilot Harness が Foundry にきた！（15／2026-10-31）— 新機能の入門解説。 https://zenn.dev/nomhiro/articles/microsoft-copilot-harness-foundry
- AI モデル自動ルーティング機能 GitHub Copilot Fusion 登場！（11／2026-11-04）— 複数モデルを自動で使い分ける機能の紹介。 https://zenn.dev/microsoft/articles/261104-copilot-fuison
- FoundryのCopilot Harnessを動かして、ハーネスなしと比べてみた（8／2026-10-31）— 実際に動かして比較した検証記事。 https://zenn.dev/nomhiro/articles/microsoft-copilot-harness-foundry-try
- AWS・Azure・OCIを比較する ― 用語・管理単位・課金・得意領域の違い（6／2026-11-01）— 3クラウドの用語や課金の違いの整理。 https://zenn.dev/banana/articles/1b74d746d2c2ea
- Claude-MemはSIerで安全に使える？仕組みとプロジェクト間のメモリ分離をコードから調査（5／2026-11-03）— AIメモリツールの安全性調査（Azure直接の話題ではない可能性あり）。 https://zenn.dev/headwaters/articles/61e035581d7c9b

### Cloudflare（走査23件／除外0件）
- 週刊Cloudflare - 2026/11/01週（11／2026-11-05）— 週次のCloudflare関連ニュースまとめ。 https://zenn.dev/gemcook/articles/weekly-cloudflare_2026_1025-1031
- Cloudflare Zero Wire × GitHub Actions × Claude で公開サーバーの脆弱性チェックを自動化（7／2026-11-07）— 点検の自動化事例。個別の脆弱性詳細・スコアは CISA/JPCERT 週報を参照してください。 https://zenn.dev/tomipetit/articles/zero-wire-github-actions
- hono/jsx で作るOGPイメージの作成、Cloudflare Workers で縦書きや Mermaid を出力（3／2026-11-02）— Workers 上で画像を生成する実装例。 https://zenn.dev/sora_kumo/articles/wasm-html-to-image-hono-jxs
- 「APIキーをローテーションしてください」を実際にやったら、鍵1本が5か所にあった（2／2026-11-03）— 鍵の更新作業で見えた散在の問題。 https://zenn.dev/hakumaigenki/articles/api-key-rotation-5-places
- 安全なステージング環境を IaC でつくろう（2／2026-11-02）— IaC（コードによるインフラ構築）で検証環境を作る話。 https://zenn.dev/yasuakiomokawa/articles/5f8498996e5e1b

## ℹ この記事の見方
- いいね数・コメント数は**取得時点（2026-11-08）の値**です。人気の目安であり、正確性を保証しません。
- 「新着100件から選定」はAWSのみ該当（走査が上限100件に達したため）。他分野は走査件数が上限未満です。
- 要約はタイトル・フィード情報から読み取れる範囲で書いており、本文の詳細は各記事でご確認ください。
- 脆弱性に関する話題の詳細・スコアは CISA／JPCERT 週報を参照してください。
- 取得できなかった情報源：なし。

## 出典
- Zenn 公式フィード/API（トピック別トレンド・新着）: https://zenn.dev/topics/aws ほか、google-cloud・azure・cloudflare の各トピックのフィード
- 各記事のURLは上記本文に記載

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
