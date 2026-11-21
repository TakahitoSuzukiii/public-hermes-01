作成日: 2026-11-22 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-11-15〜2026-11-22

# Zenn クラウド人気記事 週報（AWS / Google Cloud / Azure / Cloudflare）

## 📌 今週のハイライト
- AWS は生成AI関連（Amazon Bedrock、AgentCore＝AIエージェントを動かす基盤）の検証記事が多く、IaC（Infrastructure as Code：インフラをコードで管理する手法）の移行事例も注目されました。
- Cloudflare は「Claude Code の利用ログ収集」「自宅サーバーの安全な公開（Tunnel + Access）」など、実用的な運用ネタが上位でした。
- Google Cloud は AI 活用の学習システム事例が最多いいね。Azure は全体的にいいね数が控えめで、Microsoft Fabric 導入連載が目立ちました。
- 「Cloudflare と AWS の費用比較」のように、コスト観点の記事が複数分野で話題になっています。

## 🔥 今週これだけ読む3本
1. **OpenTelemetry×Cloudflareで組織のClaude Code利用ログを収集する**（19いいね）
   - 理由: 今週の4分野で最多いいね。AI開発ツールの利用状況を Cloudflare 上で集める実践例とみられます。
   - https://zenn.dev/gemcook/articles/claude-code-otel-cloudflare
2. **AI時代の新卒、実務で技術が身につきづらいので自分でなんとかする── Google Cloudで作った「AI禁止×音声口頭試問」学習システム**（13いいね）
   - 理由: Google Cloud 分野の最多。学習用システムを自作した事例で、発想が参考になります。
   - https://zenn.dev/acntechjp/articles/bfefba399ab42d
3. **CDKからTerraformへ：所有権移譲による本番インフラ無停止のIaC移行**（11いいね）
   - 理由: 本番を止めずに IaC ツールを移行する話で、実務への示唆が大きそうです。
   - https://zenn.dev/levtech/articles/14befd8e727f32

## 💬 トピック別ホット記事

### AWS
※新着100件から選定。いいね数はすべて取得時点の値。
- **AWSから見たSnowflake Storage for Iceberg**（12いいね / 2026-11-14）: Iceberg（大規模データ向けテーブル形式）をAWS側から見た解説。 https://zenn.dev/penginpenguin/articles/36a822bfd124d7
- **CDKからTerraformへ：所有権移譲による本番インフラ無停止のIaC移行**（11 / 2026-11-20）: 無停止でのIaC移行事例。 https://zenn.dev/levtech/articles/14befd8e727f32
- **インフラ＆CI/CD（GitHub Actionsの自動デプロイ）〜化石時代のFTPから脱却〜**（9 / 2026-11-16）: FTPからGitHub Actionsによる自動デプロイへの移行。 https://zenn.dev/dgft/articles/da631c5758aa6a
- **Cloudflareは本当に安いのか？…AWSと費用を比べてみた【2026年版】**（6 / 2026-11-19）: 3パターンでの費用比較。 https://zenn.dev/emoba_tech/articles/975672e3c122ac
- **アクセスキー不要！ Claude Desktop から Amazon Bedrock にインタラクティブサインインで接続する**（6 / 2026-11-19）: 長期アクセスキーを使わない接続方法。 https://zenn.dev/aws_japan/articles/claude-desktop-bedrock-interactive-signin
- 除外: 宣伝色の強い・クラウド非中心の記事 1件程度（うちわ制作裏話などは同率で次点）。

### Google Cloud
- **AI時代の新卒…「AI禁止×音声口頭試問」学習システム**（13 / 2026-11-17）: Google Cloud 製の学習システム事例。 https://zenn.dev/acntechjp/articles/bfefba399ab42d
- **Weekly Google Cloud アップデート情報 - 2026年11月17日**（3 / 2026-11-17）: 週次の更新情報まとめ。 https://zenn.dev/softbank/articles/82456e956dd3e8
- **AI 時代のセキュリティ入門：入口と出口**（3 / 2026-11-20）: AI利用時のセキュリティ入門。 https://zenn.dev/densan_techblog/articles/e6474ff2209dad
- **Cloud Run express links で ID トークン取得コードは消せるか**（2 / 2026-11-16）: 導入前の判断ポイント整理。 https://zenn.dev/nabeyan_dev/articles/fsfn-cloud-run-express-links
- **SpannerのRepeatable Readによるレイテンシ改善効果と仕組み**（2 / 2026-11-19）: Spanner（Google の分散DB）の分離レベルに関する解説。 https://zenn.dev/google_cloud_jp/articles/b112447edb6af8
- 除外: ゲーム/ガジェット系などクラウドと関連の薄い記事。全体にいいね数が少ない週でした。

### Microsoft Azure
- **エンタープライズシステムへのMicrosoft Fabric導入(第１回)**（9 / 2026-11-20）: Fabric（データ分析統合基盤）導入連載の初回。 https://zenn.dev/nttdata_tech/articles/c4213a272224fe
- **App Service Planを停止して課金を止められるようになった🚀**（2 / 2026-11-16）: App Service の課金停止に関する話題。 https://zenn.dev/mrt/articles/2d08720364c50a
- **Weekly Azure アップデート情報 - 2026/10/19**（2 / 2026-11-16）: 週次更新まとめ。 https://zenn.dev/softbank/articles/6b8bc2d54a5033
- **Weekly Azure アップデート情報 - 2026/10/27**（2 / 2026-11-17）: 同上。 https://zenn.dev/softbank/articles/042d355535ea9c
- **Azure Blob Storage - コンテナーごとにライフサイクルを設定する方法**（0 / 2026-11-21）: ストレージの自動削除・階層化設定。 https://zenn.dev/headwaters/articles/3ab4ac0684e3f7
- 除外: クラウド色の薄い記事 1件。

### Cloudflare
- **OpenTelemetry×CloudflareでClaude Code利用ログを収集する**（19 / 2026-11-17）: 上記「3本」参照。 https://zenn.dev/gemcook/articles/claude-code-otel-cloudflare
- **週刊Cloudflare - 2026/11/15週**（11 / 2026-11-19）: Cloudflare 週次ニュースまとめ。 https://zenn.dev/gemcook/articles/weekly-cloudflare_2026_1108-1114
- **自宅サーバー上のアプリを Cloudflare Tunnel + Access で安全に公開する**（7 / 2026-11-20）: 外部公開を安全に行う構成例。 https://zenn.dev/bisque/articles/home-server-cloudflare-tunnel-access
- **Cloudflareは本当に安いのか？…AWSと費用を比べてみた【2026年版】**（6 / 2026-11-19）: AWSとの費用比較。 https://zenn.dev/emoba_tech/articles/975672e3c122ac
- **認証基盤を入れても、APIから情報は抜ける。…認可が残る**（5 / 2026-11-20）: 認証と認可の違いに関する注意喚起。個別の脆弱性は扱わず詳細は元記事参照。 https://zenn.dev/aeyesec/articles/d17f8a333b79c3
- 除外: ロボット制作などクラウドと無関係な記事（17いいね）ほか数件。

## ℹ この記事の見方
- いいね数は**取得時点の値**です。人気の目安であり、正確性・内容の品質を保証するものではありません。
- 要約はタイトルと概要から読み取れる範囲の紹介で、本文の全文転載はしていません。
- 脆弱性の話題は、詳細・スコアは CISA / JPCERT 週報を参照してください。
- 取得できなかった情報源: なし。

## 出典
- Zenn 公式フィード・API（トピック別 trending / 新着）: https://zenn.dev/ ／ https://zenn.dev/api/articles
- 記事の各URLは本文中に記載。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
