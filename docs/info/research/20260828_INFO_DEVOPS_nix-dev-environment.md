作成日: 2026-08-28 / STATUS: INFO / TOPIC: DEVOPS

# Nix — 開発環境構築自動化ツールの調査

> 開発環境構築の自動化ツールとしてのNix(Nixパッケージマネージャー / NixOS / Nix Flakes)について調査したノート。

## 0. 結論(先出し)

**Nixは「宣言型」で開発環境・パッケージ・OS設定を管理できるツール群の総称。** 1つの設定ファイルに「何が必要か」を書くだけで、誰の環境でも寸分違わず同じ開発環境を再現できる。DockerやIaC(Infrastructure as Code)とは競合ではなく**補完関係**にあり、「Dockerは環境を丸ごと箱に入れる」「Nixは必要な道具だけを正確に揃える」というイメージの違いがある。

出典: [UNICORNEE AI「Nixとは？宣言型パッケージ管理で開発環境の『壊れた』をなくす方法」](https://unicornee.ai/articles/nix-package-manager/)

## 1. Nixとは何か

Nixは狭義には「**純粋関数型パッケージマネージャ**」。brewやapt等の一般的なパッケージマネージャーと同様、パッケージのインストール・バージョン管理・ビルド機能を持つが、決定的に違うのは**「外部から隔離された環境で、依存関係を明示的にしてパッケージをビルドする」**という性質。

出典: [日本経済新聞「純粋関数型パッケージマネージャ Nix のメリットと活用事例」](https://hack.nikkei.com/blog/advent20241207/)

「Nix」という言葉が指す範囲は広く、以下の要素を含む:

| 要素 | 内容 |
|---|---|
| **Nixパッケージマネージャー** | ソフトウェア・開発環境を再現可能にする本体機能 |
| **Nixpkgs** | Nix用の巨大なパッケージリポジトリ(コミュニティ管理) |
| **NixOS** | Nixの仕組みをOS全体に適用したLinuxディストリビューション |
| **nix-darwin** | macOSにNixOSと同様の宣言的システム管理を持ち込むプロジェクト |
| **Nix Flakes** | 依存関係とバージョンを固定し、再現性をさらに高める新しい仕組み(実験的機能として提供されつつも広く使われている) |

出典: [Zenn「Nixで始める再現可能な開発環境：DockerやIaCとの違い」](https://zenn.dev/stmn_inc/articles/nix-package-manager)

## 2. なぜ「壊れない」開発環境を作れるのか

### 2-1. 純粋関数型という設計

Nixにおけるパッケージのビルドは「関数」として扱われ、**同じ入力(依存関係・バージョン)からは必ず同じ出力(ビルド結果)が得られる**ことが保証される。これにより「私の環境では動くのに、あなたの環境では動かない」という典型的な問題を構造的に防げる。

### 2-2. 依存関係の完全な明示

システムに元々入っているライブラリやツールに暗黙的に依存することがなく、**必要なものは全てNixの設定ファイルに明記**される。これにより、新しいメンバーが参加してもコマンド一つで全く同じ開発環境を再現できる。

### 2-3. `nix run` による一時実行

パッケージをシステムに恒久的にインストールせず、**一時的に実行して痕跡を残さない**ことができる。

```bash
# Pythonの特定バージョンをインストールせずに試す
nix run nixpkgs#python311 -- --version

# cowsayを一度だけ使いたい
nix run nixpkgs#cowsay -- "Hello from Nix!"
```

実行が終われば環境は汚れない。「ちょっと試したいだけ」のケースに強い。

出典: [UNICORNEE AI「Nixとは？」](https://unicornee.ai/articles/nix-package-manager/)

## 3. Nix Flakesの基本的な使い方

Flakesは、プロジェクトごとの依存関係・バージョンをより厳密に固定する仕組み。プロジェクトルートに`flake.nix`というファイルを置いて管理する。

### 3-1. 基本コマンド

```bash
# デフォルトテンプレートでflakeを新規作成
nix flake init

# flake.nixで定義した開発シェルに入る(devShellが定義されている場合)
nix develop
```

`nix flake init`は、既存のディレクトリに`flake.nix`を生成する。テンプレートを指定することも可能で、プロジェクトの言語(Rust/Node.js等)に応じた依存関係を含む雛形を生成するツール(`fh init`等)も存在する。

出典: [Nix Reference Manual「nix flake init」](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-flake-init.html)、[Zero to Nix「Turn your project into a flake」](https://zero-to-nix.com/start/init-flake/)

### 3-2. devShell(開発シェル)の考え方

Flakesにおける`devShell`は、旧来の`nix-shell`に相当する仕組みで、**プロジェクトに必要なツール・ライブラリ一式が揃った状態のシェル環境**を、コマンド一つ(`nix develop`)で立ち上げられる。これまでDockerfileを書いてDevContainerを立ち上げていた部分が、Flakesの作成に置き換わるようなイメージで捉えられる。

出典: [Zenn「Nixで作る個人開発環境」](https://zenn.dev/hctaw_srp/articles/3cd4e62e6fedc3)、[Yuan Wang's Blog「Getting started with Nix Flakes and devshell」](https://yuanwang.ca/posts/getting-started-with-flakes.html)

## 4. Docker・IaCとの違い

| 観点 | Nix | Docker |
|---|---|---|
| **抽象化の粒度** | 必要なパッケージ・ツールを個別に正確に指定 | アプリケーションの実行環境を丸ごとコンテナ化 |
| **たとえ** | 「必要な道具だけを正確にリストアップして揃える」 | 「部屋ごと段ボール箱に入れる」 |
| **OS/システム設定への適用範囲** | NixOS/nix-darwinでシステム全体の設定管理も可能 | コンテナ内に限定 |
| **関係性** | 競合ではなく**補完関係**。NixでDockerイメージをビルドする使い方も人気 | 同上 |

Nixは開発環境のパッケージ管理に特化しており、Dockerはアプリケーションの実行環境を隔離することに特化している。両者は役割が異なるため、**「Nixで環境を作り、Dockerでデプロイする」**といった組み合わせ方も一般的。

出典: [UNICORNEE AI「Nixとは？」](https://unicornee.ai/articles/nix-package-manager/)、[Zenn「Nixで始める再現可能な開発環境」](https://zenn.dev/stmn_inc/articles/nix-package-manager)

## 5. NixOSとDockerの比較(システムレベル)

NixOSは「システム全体がImmutable(不変)であること」を前提に設計されている。この精度の高さは、Dockerの「ベースイメージや依存バージョンの微妙な差異が原因の、診断しづらい不具合」が起きにくいという利点につながる。また、NixOSには**ロールバック機能(設定変更前の状態へ簡単に戻せる)**や**きめ細かいバージョン管理**といった、Dockerにはない特徴もある。

出典: [Medium「Why NixOS and Devbox Are Gaining an Edge Over Docker」](https://medium.com/@yedidyarashi/why-nixos-and-devbox-are-gaining-an-edge-over-docker-609edb4e374c)

## 6. メリット・デメリット

### メリット
- **再現性**: 環境構築の「動く動かない問題」を構造的に防げる
- **柔軟性**: 開発環境に限らず、システムやユーザー設定なども統一的に管理できる
- **ロールバック**: 変更前の状態に簡単に戻せる(NixOS)
- **クリーンな試用**: `nix run`で環境を汚さずツールを試せる

### デメリット
- **学習コストが高い**: Nix独自の概念(純粋関数型・宣言型記法等)を理解する必要がある
- **エコシステムの規模**: Nixpkgsは巨大だが、主要言語のパッケージマネージャーと比べるとエコシステムの規模はまだ小さい
- **Flakesは実験的機能**: 広く使われているものの、Nix公式のドキュメント上は依然「experimental」の扱い

出典: [Zenn「Nixで始める再現可能な開発環境」](https://zenn.dev/stmn_inc/articles/nix-package-manager)

## 7. まとめ

Nixは「開発環境が壊れる・再現できない」という長年の課題に対する、宣言型・純粋関数型アプローチによる解決策。Docker/IaCと競合するものではなく、**役割の異なるツールとして組み合わせて使う**のが実践的な位置づけ。学習コストの高さがハードルではあるが、チーム開発で環境差異によるトラブルを減らしたい場合や、macOS(nix-darwin)・Linux(NixOS)を問わず統一的にシステム設定を管理したい場合に検討価値が高いツール。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。