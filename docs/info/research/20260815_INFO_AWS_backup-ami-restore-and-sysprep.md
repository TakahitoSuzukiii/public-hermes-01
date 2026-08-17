作成日: 2026-08-15 / STATUS: INFO / TOPIC: AWS

# AWSでのバックアップ・イメージ取得・リストア、およびWindows Sysprepの基礎知識

> ⚠️ マスキング規約準拠。個人情報（氏名・所属・連絡先等）は一切記載しない。

## 0. 背景・この記事の狙い

AWS（Amazon Web Services、Amazonが提供するクラウドサービス群）でサーバー（EC2インスタンス）を運用していると、「壊れたときに戻せるようにしておく」「同じ構成のサーバーを複数台作りたい」という場面が必ず出てきます。この記事では、そのための3つの手段——**AMI（マシンイメージ）**・**EBSスナップショット**・**AWS Backup**——の違いと使い分け、そしてWindowsサーバーの複製時に欠かせない**Sysprep（システム準備ツール）**についてまとめます。

## 1. まず全体像：3つのバックアップ手段の違い

| 手段 | 対象 | 何ができるか |
|---|---|---|
| **EBSスナップショット** | ディスク（EBSボリューム）単位 | ディスクの中身をある時点でまるごと保存。裏側ではAmazon S3（オブジェクトストレージ）に保存される |
| **AMI（Amazon Machine Image）** | サーバー（EC2インスタンス）まるごと | OS・ミドルウェア・アプリまで含めた「起動可能な設計図」。複数のEBSスナップショットの組み合わせで構成される |
| **AWS Backup** | EC2・EBS・RDS・S3・DynamoDB等、複数サービス横断 | バックアップの取得・保持期間・削除ルールを一元管理できる専用サービス |

出典: [AWS Backup 公式ドキュメント「とは」](https://docs.aws.amazon.com/ja_jp/aws-backup/latest/devguide/whatisbackup.html)

### AMIとEBSスナップショットの関係

AMIは「空っぽの入れ物」ではなく、**内部的にはEBSスナップショットの集合体**です。たとえばOS用ディスクとデータ用ディスクの2つを持つサーバーのAMIを作ると、その裏では2つのEBSスナップショットが作られ、それらを「このAMIはこの2つのスナップショットで構成される」という形で紐づけています。

- **EBSスナップショットだけ**取得した場合 → 元と同じ構成でボリュームを復元することはできるが、そこから直接サーバーを起動することはできない（一度ボリュームをEC2にアタッチする作業が必要）
- **AMI**を作成した場合 → そのAMIを選ぶだけで、同じ構成のサーバーをすぐに起動できる

## 2. AWS Backupとは何か

**AWS Backup**は、上記の個別のバックアップ機能（EC2はDLM＝Data Lifecycle Manager、RDSは自動バックアップ、S3はバージョニング…）が**サービスごとにバラバラに存在している**という課題を解決するための、一元管理サービスです。

出典: [Qiita「AWS Backup完全ガイド」](https://qiita.com/OhkuboT/items/77be1e798244319bc9c0)、[AWS公式「バックアップボールト」](https://docs.aws.amazon.com/ja_jp/aws-backup/latest/devguide/vaults.html)

### 主要な用語

- **バックアップボールト（Vault）**: バックアップデータを安全に保管する「金庫」のような場所。元のEC2インスタンスやEBSボリュームを削除しても、ボールト内のバックアップは保持ポリシーに従って残る（誤削除に対する安全網になる）
- **バックアッププラン**: 「いつ・どの頻度で・どれくらいの期間保持するか」をルールとして定義したもの
- **リソース割り当て**: どのEC2インスタンスやEBSボリュームをバックアップ対象にするか、タグ等で指定する

### メリット

- EC2・EBS・RDS・DynamoDB・S3など**複数サービスを横断して1つの画面・1つのルールで管理**できる
- 保持期間切れの自動削除（ライフサイクル管理）を仕組み化できる
- 元のリソースとバックアップ先を分離して保存するため、誤操作や障害からの独立性が高い

## 3. リストア（復元）の基本的な流れ

### EBSスナップショットからの復元

1. 対象のスナップショットを選択し、「ボリュームを作成」
2. 作成した新しいボリュームを、既存または新規のEC2インスタンスにアタッチ（接続）
3. OS内でディスクを認識させ、必要に応じてドライブレターやマウントポイントを設定

### AMIからの復元（インスタンスの再作成）

1. 対象のAMIを選択し、「インスタンスを起動」
2. インスタンスタイプ・ネットワーク・セキュリティグループなど、起動時の設定を指定
3. AMIに含まれるOS・アプリごとそのまま新しいサーバーとして起動する

出典: [とらくら「WindowsServer2022をAMIからリストアしてみた」](https://tracl.cloud/archives/engineerblog/ec2_windowsserver2022_ami)

### AWS Backupからの復元

- AWS Backupのコンソール上で対象のバックアップを選び、「復元」を実行するだけで、対応するリソース（EC2インスタンスやRDSデータベース等）が新規に作成される
- サービスごとに個別の手順を覚える必要がなく、統一されたインターフェースで復元できるのが利点

## 4. Windows Sysprepとは何か

ここからは、**Windowsサーバーの複製・AMI化に不可欠な「Sysprep（システム準備ツール）」**について解説します。

### Sysprepが必要になる理由

Windowsの各PC・サーバーは、内部的に**SID（Security Identifier、セキュリティ識別子）**という一意のIDを持っています。1台のWindowsサーバーをそのまま複製（クローン）して複数台立ち上げると、**すべてのサーバーが同じSIDを持ってしまい**、同一ネットワーク上で通信・認証まわりの不具合が起きる可能性があります。

**Sysprep（System Preparation、システム準備）**は、この「マシン固有の情報（SID等）」をWindowsイメージから取り除く（＝一般化する）ためのMicrosoft公式ツールです。これを実行してから複製することで、それぞれのサーバーが起動時に新しいSIDを自動生成し、安全に複数台展開できるようになります。

出典: [Microsoft Learn「Sysprep（システム準備）の概要」](https://learn.microsoft.com/ja-jp/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview?view=windows-11)、[SEの道標「sysprepの仕組みと使い方」](https://milestone-of-se.nesuke.com/sv-basic/windows-basic/sysprep-general/)

### Sysprepが行う主な処理

- コンピューターのSIDをリセット（初期化）
- コンピューター名・ライセンス認証情報など、マシン固有の設定を消去
- 次回起動時に「初期セットアップ画面」から始まるようにする（監査モード等の運用も可能）

## 5. AWS EC2でのSysprep実行手順

AWSのWindows EC2インスタンスには、あらかじめ**EC2Launch**（Windows Server 2016以降）または**EC2Config**（Windows Server 2008〜2012 R2）というエージェントが入っており、これを通じてSysprepを実行するのがAWS推奨の方法です。

出典: [AWS公式「EC2LaunchでWindows Sysprepを使ってAMIを作成する」](https://docs.aws.amazon.com/ja_jp/AWSEC2/latest/UserGuide/ec2launch-sysprep.html)、[AWS re:Post「Use Sysprep for custom reusable Windows AMIs」](https://repost.aws/knowledge-center/sysprep-create-install-ec2-windows-amis)、[サーバーワークスエンジニアブログ「EC2】Sysprepの手順」](https://blog.serverworks.co.jp/tech/2019/05/07/sysprepfirst/)

### 手順の概要

1. AMI化したい元インスタンスにログインする
2. スタートメニューから該当ツールを起動
   - Windows Server 2016以降 → 「**EC2Launch Settings**」（または「EC2Launch v2」の場合は別のインターフェース）
   - Windows Server 2008〜2012 R2 → 「**EC2ConfigService Settings**」→「Image」タブ
3. **Administrator Password**（管理者パスワード）欄で、Sysprep後に割り当てるパスワードの扱いを選択
   - 「Random」を選ぶと、次回起動時にランダムなパスワードが自動生成される（一般的な推奨設定）
4. 「**Shutdown with Sysprep**」（Sysprepを実行してシャットダウン）を選択し、実行を確認
5. インスタンスが自動的にSysprepを実行し、シャットダウンする
6. AWSマネジメントコンソールで、シャットダウンしたインスタンスから「**イメージを作成**」を実行し、AMIとして保存する

### 注意点

- Sysprepの実行中にインスタンスへ接続したまま操作を続けると、処理が正しく完了しないことがあるため、**Sysprep実行後は自動シャットダウンを待つ**のが基本
- Sysprep完了後のAMIから起動した新しいインスタンスは、初回起動時に新しいSIDの生成やコンピューター名の再設定などの初期化処理が走るため、**起動直後は数分ほど時間がかかる**ことがある
- Amazon Lightsail（AWSの簡易版クラウドサービス）でも同様にSysprepを使ったスナップショット作成が可能（[AWS公式Lightsailガイド](https://docs.aws.amazon.com/ja_jp/lightsail/latest/userguide/prepare-windows-based-instance-and-create-snapshot.html)）

## 6. まとめ：使い分けの目安

| やりたいこと | おすすめの手段 |
|---|---|
| ディスク単位で時点バックアップを取りたい | EBSスナップショット |
| サーバーまるごと複製・別環境に展開したい | AMI（Windowsの場合はSysprep併用が必須） |
| 複数サービスのバックアップを一元管理・自動化したい | AWS Backup |
| Windowsサーバーを複数台、同じ構成で立ち上げたい | Sysprep実行済みのAMIから複数起動 |

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
