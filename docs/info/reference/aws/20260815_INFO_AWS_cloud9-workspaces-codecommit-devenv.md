# クラウド開発環境ガイド：Cloud9 / WorkSpaces と CodeCommit 連携（ローカルPCに制約がある場合）

> **対象**: ローカルPCにVSCodeをインストールできない・SSHも使えないという制約下で、AWS上に開発環境を構築したい人向け。
> **作成日**: 2026-08-15（JST） / **ステータス**: INFO（情報提供・構築ガイド）
> **一次情報**: [AWS Cloud9 ユーザーガイド](https://docs.aws.amazon.com/cloud9/)、[AWS CodeCommit — Cloud9統合](https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/setting-up-ide-c9.html)、[AWS CodeCommit 提供再開のお知らせ（AWS公式ブログ, 2025-11）](https://aws.amazon.com/blogs/devops/aws-codecommit-returns-to-general-availability/)
> **元記事**: public2リポジトリ `env/dev-env.md` を再構成（内容はweb_searchで裏取りし加筆修正）

---

## ⚠️ 重要な鮮度情報（元記事からのアップデート）

元記事は AWS CodeCommit の利用を前提にしていましたが、**CodeCommitはAWSが2024年7月に「新規顧客への提供を終了する」と発表し、事実上の非推奨状態にありました**。その後、2025年11月にAWSは方針を転換し、**CodeCommitの一般提供（GA）を再開**したと公式発表しています（[AWS DevOps Blog](https://aws.amazon.com/blogs/devops/aws-codecommit-returns-to-general-availability/)）。

このため本記事作成時点（2026年8月）では CodeCommit は新規利用可能な状態に戻っていますが、**実際に採用する際は必ず最新のAWS公式アナウンスを確認**してください。一時的にせよ「廃止予定→復活」という異例の経緯を辿ったサービスであるため、長期的な採用判断は公式ロードマップを都度確認することを強く推奨します。恒久的な代替としては GitHub / GitLab 等の外部Gitホスティングも検討候補です。

---

## 用語ミニ解説（初心者向け）

- **AWS Cloud9**: ブラウザだけで使えるAWS製の統合開発環境（IDE）。実体はEC2インスタンス上で動く。
- **Amazon WorkSpaces**: AWS上にクラウド仮想デスクトップ（Windows/Linux）を持てるサービス。ローカルPCは「画面を映すだけの端末」として使う。
- **AWS CodeCommit**: AWSが提供するフルマネージドGitリポジトリサービス。

---

## 1. Cloud9：AWSネイティブのブラウザIDE

### 特徴

- ブラウザだけで開発でき、ローカルに何もインストール不要
- 裏側はEC2インスタンスのため、Node/Python等のランタイムを自由に導入可能
- VSCodeやCursorなどローカルインストール型のエディタ・AIコーディングツールは使えない

### メリット・デメリット

| 項目 | 内容 |
|---|---|
| メリット | ローカル制約下でも使える／ブラウザさえあればどこでも同一環境／自動休止でコスト抑制可能 |
| デメリット | エディタとしてVSCodeに劣る／Cursor等ローカル型AIコーディングツールは使用不可 |

### 構築手順

1. AWSコンソール → Cloud9 → Create environment
2. 環境名を設定（例: `dev-env-cloud9`）
3. Environment type: EC2
4. Instance type: t3.small 等
5. Platform: Amazon Linux 2 / Ubuntu
6. Cost-saving setting: 30分で自動休止（コスト観点で推奨）
7. 作成後、ブラウザでIDEにアクセスして開発開始

### 概算コスト（t3.smallを1か月フル稼働させた場合の目安）

- EC2（t3.small）: 約 0.026 USD/h × 720h ≈ 約19 USD
- EBS 50GB: 約4 USD
- 合計: 数千円/月程度（自動休止を使えばさらに削減可能）

> ⚠️ AWSの料金は改定されるため、実際の見積もりは必ず [AWS料金計算ツール](https://calculator.aws/) で最新値を確認してください。

---

## 2. WorkSpaces：クラウド上の自分専用PC

### 特徴

- AWS上にクラウドPC（Windows/Linux）を持ち、その中にVSCode/Cursor/Git等を自由にインストール可能
- ローカルPCはWorkSpaces Clientアプリを動かすだけの「画面転送端末」として使う

### メリット・デメリット

| 項目 | 内容 |
|---|---|
| メリット | VSCode/Cursorが普通に使える／ローカルPC制約を完全回避／開発体験が自然 |
| デメリット | 月額固定でCloud9より高くつきやすい／ネットワーク品質に依存／GPU用途には不向き |

### 構築手順

1. AWSコンソール → WorkSpaces → Launch WorkSpaces
2. Directory（Simple AD等）を作成
3. ユーザーを作成しWorkSpaceを割り当て
4. Bundle（スペック）を選択（Standard以上推奨）
5. 登録メール受信後、ローカルPCにWorkSpaces Clientをインストール
6. クラウドPCにログインし、VSCode/Cursor等をインストールして利用開始

---

## 3. Cloud9 vs WorkSpaces：比較表

| 項目 | Cloud9 | WorkSpaces |
|---|---|---|
| ローカル制約への強さ | ◎（ブラウザのみ） | ◎（クライアントのみ） |
| VSCode/Cursor利用 | ✕ | ◎ |
| 開発体験 | △（ブラウザIDE） | ◎（クラウドPC） |
| AIコーディングツール | △（ブラウザIDEの制約内） | ◎（Cursor等が普通に使える） |
| コスト傾向 | 比較的安い | やや高め |
| 向いている用途 | AWS中心の開発・コスト重視 | VSCode/Cursorを使いたい・快適さ重視 |

**結論の目安**: 開発体験（特にAIコーディングツールの利用）を重視するならWorkSpaces、コストを抑えたい・AWSリソース操作中心ならCloud9、という判断軸になる。

---

## 4. ソース管理: CodeCommitとの連携（AWS内で完結するGit運用）

CodeCommitはAWSが提供するフルマネージドGitリポジトリで、Cloud9とは公式に統合されている（[AWS公式ドキュメント](https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/setting-up-ide-c9.html)）。

### 最小運用フロー

**① リポジトリ作成**: AWSコンソール → CodeCommit → Create repository（Cloud9から直接作成も可能）

**② Git認証情報の作成（HTTPS）**: SSHが使えない環境ではHTTPS Git認証情報を使う。IAM → 対象ユーザー → 認証情報タブ → 「AWS CodeCommit の HTTPS Git 認証情報」を生成。

**③ Cloud9 / WorkSpaces から clone**

```bash
git clone https://git-codecommit.<region>.amazonaws.com/v1/repos/<repo-name>
```

Cloud9はGit・AWS CLIがプリインストールされているためそのまま使える。

**④ commit / push**

```bash
git add .
git commit -m "first commit"
git push
```

**⑤ pull で同期**

```bash
git pull
```

---

## まとめ

- ローカルPCに制約がある場合の開発環境は「Cloud9（ブラウザ完結・低コスト）」か「WorkSpaces（クラウドPC・高い開発体験）」の二択が基本線。
- ソース管理をAWS内で完結させたい場合はCodeCommitとCloud9の組み合わせが公式にサポートされている。
- **CodeCommitは2024年に新規提供終了→2025年11月にGA復活という経緯があるサービス**。採用判断時は必ず最新のAWS公式アナウンスを確認すること。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
