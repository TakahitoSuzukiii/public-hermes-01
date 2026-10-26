作成日: 2026-10-27 / STATUS: INFO / TOPIC: CLOUDHOT / 対象期間: 2026-10-20〜2026-10-27

# Qiita クラウド人気記事 週報（2026-10-27）

## 📌 今週のハイライト
- AWS は PHP 関連の脆弱性対応（Amazon Linux 2023 での先行ビルドなど）が、いいね・ストックとも突出して注目されました。脆弱性の詳細・スコアは CISA／JPCERT の週報を参照してください。
- Lambda Web Functions（Lambda 上で Web アプリをそのまま動かす仕組み）を扱う記事が AWS・Google Cloud 両方で登場し、Cloud Run との比較が話題です。
- Cloudflare は画像抽出モデル「Clairic」を試す記事が複数あり、Workers／D1／R2 の実践的なトラブル解決記事も目立ちました。
- Google Cloud と Azure は全体にいいね数が少なく、Cloud Run 運用・Entra ID／Defender など実務寄りの記事が中心です。

## 🔥 今週これだけ読む3本
1. **PHP脆弱性php2shell対応、7.4本番を止めずに守った夜と実際の攻撃**（いいね158／ストック100）— 今週の最多反応。本番を止めずに対応した経験談です。 https://qiita.com/kenimo49/items/30f290bf0f4fff021fb3
2. **CloudFront + AWS WAF のパストラバーサル対策 ― パス条件のルールは `../` ですり抜けられるのか検証した**（5／4）— WAF（Web Application Firewall、Web攻撃を防ぐ仕組み）の設定を検証した実用的な内容です。 https://qiita.com/k-matsu516/items/d94caff03976fb8a30f0
3. **1枚0.3秒!!Cloudflareの爆速抽出モデルClairicを試してみた**（9／3）— Cloudflare 分野の今週の注目トピックを手を動かして確認しています。 https://qiita.com/kikuziro/items/3f23603152b409d4a6ca

## 📝 タグ別ホット記事（直近7日）
※数値は取得時点の値。公開日は 2026 年。

### AWS（走査115件。宣伝色・無関係な記事など4件を除外）
- **PHP脆弱性php2shell対応、7.4本番を止めずに守った夜と実際の攻撃**（158／100、10/22）— 古いPHP環境を稼働させたまま対策した体験談。 https://qiita.com/kenimo49/items/30f290bf0f4fff021fb3
- **Amazon Linux 2023 の PHP を CVE-2026-109618 修正版へ先行ビルドする**（17／10、10/22）— 公式パッケージ提供前に修正版を自前ビルドする話題（CVE の詳細は JPCERT／CISA を参照）。 https://qiita.com/amu-kuroneko/items/46f00fbe8b5bac009c1c
- **CloudFront + AWS WAF のパストラバーサル対策**（5／4、10/26）— `../` によるルール回避の可否を検証。 https://qiita.com/k-matsu516/items/d94caff03976fb8a30f0
- **Lambda Web Functionsについて！**（8／1、10/21）— Lambda で Web アプリを動かす機能の紹介。 https://qiita.com/PDC-Kurashinak/items/510620a2938af38f319d
- **Oracle Database@AWS の Exadata Dedicated Infrastructure への接続方式を整理してみる。**（4／3、10/25）— 接続方式の整理記事（Oracle Organization）。 https://qiita.com/ora_gonsuke777/items/25bef1613f1ca7df58be

### Google Cloud（走査8件。無関係な記事など3件を除外）
- **Next.js が Lambda でそのまま動く！Lambda Web Functions を Cloud Run と比べてみた**（3／1、10/22）— Cloud Run との比較。 https://qiita.com/na-tamura/items/d5c49f26ef610d59d8e4
- **Cloud Run Jobs で「直したのに直っていない」…実行前にイメージの commit を確かめる**（1／1、10/21）— ジョブはビルド済みイメージを動かす点への注意喚起。 https://qiita.com/20051215kaito/items/f96b9649495283e0384d
- **WordPressブログをCloud Runに移行したくなったので、実際に試してみた**（0／1、10/22）— 移行の試行記録。 https://qiita.com/toshyss/items/5cdad510ba984c7e9c3d
- **terraform apply を無指定で打つと、デプロイ済みの Cloud Run が古いイメージに戻る**（0／0、10/23）— `-target` での回避を紹介。 https://qiita.com/20051215kaito/items/db19ee3be1498a4d7913
- **初めて Terraform の二重管理を踏んだ話**（0／0、10/20）— Terraform（インフラをコードで管理するツール）の失敗談。 https://qiita.com/gensan0223/items/535b9f4fc768d48b378d

### Microsoft Azure（走査11件。無関係な記事など4件を除外）
- **Entra ID で AI エージェントに ID を持たせよう！ ～ Foundry × Claude で検証（その2）**（1／1、10/25）— AIエージェントのID管理の検証。 https://qiita.com/shou-wordwright555501/items/3bd2c2453f32c1ecd25c
- **Microsoft Defender for Identity センサーを v2 から v3 へ移行してみた**（0／1、10/26）— DC 2台での所要時間・注意点を実測。 https://qiita.com/hisnakad/items/7be9fee209336832e684
- **AzureのPaaS環境にGoogle Workspace認証付きFessを構築してみる**（0／1、10/21）— 検索システムFessの構築（企業Organization）。 https://qiita.com/pmc-ko/items/5991b664cecf07006964
- **Azure FirewallとExpressRouteで実現する閉域網接続**（0／0、10/23）— Route Table設計のポイント（NTTデータ九州）。 https://qiita.com/NTTDATA-Kyushu-Cloud/items/9ac265eb1afe37432372
- **Azure Web Apps(PHP/Linux + nginx)で旧サイトから新サイトへ301リダイレクトする手順**（0／0、10/25）— 切り戻し付きの手順。 https://qiita.com/watyanabe164/items/53bf765c3c05993f95c3

### Cloudflare（走査16件。無関係な記事など4件を除外）
- **1枚0.3秒!!Cloudflareの爆速抽出モデルClairicを試してみた**（9／3、10/25） https://qiita.com/kikuziro/items/3f23603152b409d4a6ca
- **「ファイルを送信しない」をCSPとPlaywrightで保証する**（5／1、10/21）— CSP（Content Security Policy、ブラウザの通信制限）で外部送信しないことを検証。 https://qiita.com/Ruria1024/items/70c607a7899e1bda24b4
- **入力を一切送信しない「ブラウザ完結」の小さなツール集を、フレームワークなしで作った**（2／2、10/21） https://qiita.com/tool-yokocho/items/fd3a05cded0de305bd70
- **「deploy: could not read the pending D1 migrations…」の解決方法【GitHub Actions/Cloudflare】**（2／0、10/21）— D1（Cloudflareのデータベース）デプロイエラーの対処。 https://qiita.com/keikeigo/items/1f9f42de1fa05085b6d1
- **Cloudflare WorkersでIntune MDMのApple端末におけるアカウント駆動型ユーザー登録を実現する**（0／1、10/25） https://qiita.com/kouhei-ioroi/items/c6bc31105b614a8fc20e

## 📚 定番（直近30日・ストック20以上）
### AWS
- 2026年の情報漏洩を手口で分類してみた（ストック189）https://qiita.com/yama3133/items/071119dfea9ed24d0948
- CVE-2026-99999（PwnEscape）の対応状況まとめ（ストック40）※詳細はCISA／JPCERT参照 https://qiita.com/k2_naka/items/fa87685231377f15e7e3
- 判断特化型GraphRAGをJevを使って構築してみた（ストック36）https://qiita.com/kikuziro/items/6191b5ad83520d181f38
### Google Cloud
- 該当なし
### Microsoft Azure
- 該当なし
### Cloudflare
- どのようなサイトが狙われているか？Cloudflareセキュリティログから見る攻撃の傾向と対策（ストック35）https://qiita.com/shioccii/items/cf18356730534053de95
- Jev・Clef・d1・Jeff・Kev…意思決定モデル（System One）を仕組みから比較する【2026年10月版】（ストック35）https://qiita.com/nogataka/items/a2f89a94d243b1b715cb

## ℹ この記事の見方
- いいね・ストック（後で読むための保存数）は**取得時点の値**です。人気の目安であり、正確性・内容の品質を保証するものではありません。
- 要約はタイトル等から読み取れる範囲で記載しており、本文は精査していません。
- 取得できなかった情報源: なし

## 出典
- Qiita API v2（https://qiita.com/api/v2/items）

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
