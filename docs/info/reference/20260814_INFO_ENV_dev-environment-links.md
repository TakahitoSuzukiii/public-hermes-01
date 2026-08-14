# 開発環境リンク集(Git/GitHub・Linux・macOS・Windows・シェル・SSH・VSCode)

> 出典: 個人メモ用リポジトリ `docs`(private)の `pages/40_environment/` 配下を再構成したもの。実ホスト名・実ユーザ名などの環境固有情報は placeholder に置換しています。

## 目次
- [Git / GitHub](#git--github)
- [Linux](#linux)
- [macOS](#macos)
- [OS全般](#os全般)
- [シェル(PowerShell含む)](#シェルpowershell含む)
- [SSH](#ssh)
- [VSCode](#vscode)
- [Windows](#windows)

## Git / GitHub

- [Git and Git Flow Cheat Sheet](https://github.com/arslanbilal/git-cheat-sheet#git-and-git-flow-cheat-sheet-)
- [よく使うGitコマンド19選(初心者向け)](https://www.sejuku.net/blog/5816#index_id5)
- [初めてのGit設定・コマンド操作まとめ](https://dev.classmethod.jp/articles/howtogit_forbeginner/)

### stash(作業を一時退避する)
```bash
git stash save -u コメント
git stash list
git stash apply stash@{0}
git stash drop stash@{0}
git diff stash@{0}
git diff stash@{0} hoge.txt
git stash clear
```

### fetch(リモートの変更を取得する)
> みんなの更新内容を、自分の開発環境に取り入れる機能。
- [git fetchを正しく理解しよう](https://www.sejuku.net/blog/71164)

```bash
git fetch
git fetch origin   # 特定のリポジトリのみ取得
git fetch --all    # 全て取得
git fetch -t       # タグの同期
git fetch -p       # 削除ブランチの同期
```

### merge(ブランチを取り込む)
> 現在のブランチ(HEADの指している場所)へ、他のブランチの更新を取り込む処理。
- [git mergeでブランチをマージしよう](https://www.sejuku.net/blog/71003)

```bash
git merge 取り込みたいブランチ
git merge --no-ff 取り込みたいブランチ名  # 強制的にマージコミットを作成
```

### pull(fetch + merge)
> 内部で「fetchコマンド」と「mergeコマンド」を順次行ってくれるコマンド。
- [pullでリモートリポジトリの履歴に更新する方法](https://www.sejuku.net/blog/70851)

```bash
git pull [リポジトリ名] [ブランチ名]
git pull origin master
```

### reset
```bash
git reset --hard HEAD^   # git pullの取り消し
```

### rebase(コミット履歴の整理)
> 指定したコミットを、ブランチを変えて作り直したり、ひとまとめにしたりして、ログを綺麗にするコマンド。
> merge と rebase の違い: 既存のコミットへ影響を与えるか・与えないか。
- [図解でわかるgit rebaseの2つの使い方](https://www.sejuku.net/blog/71919)

```bash
git rebase [つなぐ元にするブランチ名]
git rebase -i [ひとまとめにする地点の一つ前のコミットID]  # 複数コミットをまとめる
```

### 認証(Personal Access Token)
- [Personal Access Tokenを使用してGitHubへアクセスする](https://qiita.com/YuukiYoshida/items/2e6b250d44bf1e0f5a0b)
- [GitHubへの認証について(公式)](https://docs.github.com/en/enterprise-server@3.6/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)
- [個人のアクセストークンの管理(公式)](https://docs.github.com/en/enterprise-server@3.6/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
- [アクセストークン認証の解説](https://zenn.dev/technicarium/articles/5bf0647056fb87#%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E3%83%88%E3%83%BC%E3%82%AF%E3%83%B3%E8%AA%8D%E8%A8%BC)
- [OAuthアプリのスコープ(公式)](https://docs.github.com/ja/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes)

> ⚠️ アクセストークンは絶対にドキュメントやコードにハードコードしない。環境変数やsecret managerで管理する。

### ブランチ・通知
- [Upstream branchとは](https://qiita.com/djkazunoko/items/373363648d2e0b620bf8)
- [GitHub通知を使いこなす](https://zenn.dev/siketyan/articles/you-are-not-using-github-correctly)

### pull時の挙動・トラブルシュート
- [Git 2.27でのgit pull時のwarningについて](https://qiita.com/tearoom6/items/0237080aaf2ad46b1963)
- [git pullするとhintがたくさん出てくる](https://qiita.com/Bjp8kHYYPFq8MrI/items/77f7dfb9c078a3074b7b)
- [git pullとgit pull --rebaseの違い](https://qiita.com/Hashimoto-Noriaki/items/6e183f738289cf288b23)
- [git pullの取り消し方法をケース別に紹介](https://ensei1375.com/git-pull-reset/)

### Gitflow(ブランチ運用モデル)
- [Gitflowワークフロー(Atlassian)](https://www.atlassian.com/ja/git/tutorials/comparing-workflows/gitflow-workflow)
- [Git-flowをざっと整理してみた](https://dev.classmethod.jp/articles/introduce-git-flow)

### GitHub Organization
- [GitHub Organizationおすすめ初期設定](https://tech.cm-group.co.jp/posts/github-organization)

### GitHub Actions(CI/CD)
- [GitHub Actions公式紹介](https://github.co.jp/features/actions)
- [GitHub Actionsを使ったマイクロサービスのCI/CDモジュール管理](https://lab.mo-t.com/blog/gha-microservice-cicd)
- [【入門】GitHub Actionsとは？](https://www.kagoya.jp/howto/it-glossary/develop/githubactions/)
- [GitHubの新機能「GitHub Actions」で試すCI/CD](https://knowledge.sakura.ad.jp/23478/)
- [GitHub Actionsって何？入門・逆引きリファレンス](https://qiita.com/yu-ichiro/items/b50ceb0008edc3c0312e)

---

## Linux

- [Awesome Linux](https://github.com/inputsh/awesome-linux#readme)
- [Awesome Linux Software](https://github.com/luong-komorebi/Awesome-Linux-Software#awesome-linux-software)
- [Awesome Linux Containers](https://github.com/Friz-zy/awesome-linux-containers#awesome-linux-containers)

### シンボリックリンク
- [シンボリックリンクの作成と削除](https://qiita.com/colorrabbit/items/2e99304bd92201261c60)

```bash
ln -s /hoge/fuga/watashi ./watashi   # シンボリックリンクを作成
unlink ./watashi                     # シンボリックリンクを削除
```

### 書籍
- [Linuxシステムの仁組み](https://www.amazon.co.jp/-/en/Brian-Ward-ebook/dp/B09TDYLWM8/)

---

## macOS

- [Awesome Mac](https://github.com/jaywcjlove/awesome-mac#awesome-mac)

---

## OS全般

- [Awesome OS](https://github.com/jubalh/awesome-os#awesome-operating-system-stuff)
- [Awesome WSL(Windows Subsystem for Linux)](https://github.com/sirredbeard/Awesome-WSL#awesome-wsl---windows-subsystem-for-linux)

### 書籍
- [コンピュータアーキテクチャ](https://www.amazon.co.jp/-/en/%E6%9C%A8%E6%9D%91-%E5%84%AA%E4%B9%8B-ebook/dp/B0B4RRZ795/)
- [自作OS](https://www.amazon.co.jp/%E6%80%92%E7%94%B0%E6%99%9F%E4%B9%9F-ebook/dp/B0C52SFYDC/)
- [プログラマーのためのCPU入門](https://www.lambdanote.com/products/cpu)

---

## シェル(PowerShell含む)

- [Awesome Shell](https://github.com/alebcay/awesome-shell#awesome-shell-)
- [Top 50+ Linux Commands You MUST Know](https://www.digitalocean.com/community/tutorials/linux-commands)

### Windows PowerShellでps1を実行する
- [PowerShellでps1を実行する方法(コマンドプロンプト経由含む)](https://extan.jp/?p=10865)

```powershell
New-Item start.ps1
# PowerShellを管理者モードで起動してから
Set-ExecutionPolicy RemoteSigned
.\start.ps1
```

---

## SSH

- [Awesome SSH](https://github.com/moul/awesome-ssh#awesome-ssh-)
- [awesome-tunneling](https://github.com/anderspitman/awesome-tunneling#readme)

### .ssh/config の設定例
- [.ssh configの解説](https://penpen-dev.com/blog/userknownhostsfile-stricthostkeychecking)
- [便利なssh configとコマンド](https://zenn.dev/ymmmtym/articles/useful-ssh-config-and-command)

> 以下は設定例です。ホスト名・鍵ファイル名は環境に応じて置き換えてください(実値はここに書かない)。

```
# ~/.ssh/config の例
Host *staging*
  StrictHostKeyChecking no
  # UserKnownHostsFile=~/.ssh/known_hosts_staging

Host *prod*
  StrictHostKeyChecking no
  # UserKnownHostsFile=~/.ssh/known_hosts_prod

Host *
  StrictHostKeyChecking no
  UserKnownHostsFile=/dev/null
  ServerAliveInterval 120
  ServerAliveCountMax 5
  AddKeysToAgent yes
  UseKeychain yes
  IdentitiesOnly yes
  TCPKeepAlive yes

# GitHub用
Host github
  HostName github.com
  User git
  Port 22
  IdentityFile ~/.ssh/<your-key-file>

# 開発環境の例(ホスト名・ユーザ名・鍵ファイル名はplaceholder)
Host <env-name>
  HostName <server-hostname>
  User <your-user>
  Port 443
  IdentityFile ~/.ssh/<your-key-file>.pem
```

> ⚠️ 秘密鍵ファイル自体・実際のホスト名・IPアドレスは絶対にドキュメントに書かない。

---

## VSCode

- [VSCodeの定番機能を一挙解説](https://qiita.com/midiambear/items/bc0e137ed77153cb421c)

### ワークスペース設定
- [VS Codeのワークスペースをちゃんと使いたい](https://qiita.com/amac-53/items/86b1466e93524844c2a8)

> `main.code-workspace` の設定例(パスは環境依存のためplaceholder化)

```jsonc
{
  "folders": [
    { "name": "デスクトップ", "path": "C:/Users/<your-user>/OneDrive/デスクトップ" },
    { "name": "ダウンロード", "path": "C:/Users/<your-user>/Downloads" },
    { "name": "Dドライブ", "path": "D:/" }
  ],
  "settings": {
    "git.ignoreLimitWarning": true,
    "todo-tree.general.tags": ["NOTE", "WARNING", "TODO", "FIXME", "BUG", "MTG"],
    "todo-tree.highlights.customHighlight": {
      "NOTE": { "icon": "note", "foreground": "#C0C0C0", "iconColour": "#C0C0C0" },
      "WARNING": { "icon": "alert", "foreground": "red", "iconColour": "red" },
      "TODO": { "icon": "check-circle-fill", "foreground": "orange", "iconColour": "orange" },
      "FIXME": { "icon": "flame", "foreground": "yellow", "iconColour": "yellow" },
      "BUG": { "icon": "bug", "foreground": "#40BA8D", "iconColour": "#40BA8D" },
      "MTG": { "icon": "feed-discussion", "foreground": "#65BBE9", "iconColour": "#65BBE9" }
    }
  }
}
```

### 保存時の自動整形
- [保存時自動整形の設定方法](https://qiita.com/mitashun/items/e2f118a9ca7b96b97840)

```
shift + alt + F   # 手動フォーマット
```

`settings.json` に `"editor.formatOnSave": true` を設定すると保存時に自動整形される。

### ユーザースニペット設定例
```jsonc
{
  "editor.tabCompletion": "onlySnippets",
  "[markdown]": {
    "editor.quickSuggestions": true
  }
}
```

### Todo Tree拡張機能
- [公式(Marketplace)](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.todo-tree)
- [Octicons(アイコン一覧)](https://primer.style/foundations/icons/)

### Git関連拡張機能
- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

---

## Windows

- [Awesome Windows](https://github.com/Awesome-Windows/Awesome#readme)

### ショートカットキー
- [Windows 10 ショートカットキー一覧](https://pc-karuma.net/windows-10-keyboard-shortcuts-list/#google_vignette)
- [【完全版】ショートカットキー早見表](https://techmania.jp/blog/windows-shortcutkey/)

### バックスラッシュの入力
日本語キーボードでバックスラッシュ `\` を入力する際の確認用メモ。

### PowerShellでのファイル新規作成
```powershell
New-Item bbb.txt
New-Item -Path "./file.txt" -ItemType "file"
```

### Office365関連
- [PowerShell(lazywinadmin)](https://github.com/lazywinadmin/PowerShell)
- [OneDrive Client for Linux](https://github.com/abraunegg/onedrive?tab=readme-ov-file#onedrive-client-for-linux)
- [Power Automate 公式](https://make.powerautomate.com/)
