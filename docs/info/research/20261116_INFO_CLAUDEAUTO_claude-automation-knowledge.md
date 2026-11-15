作成日: 2026-11-16 / STATUS: INFO / TOPIC: CLAUDEAUTO

# Claude / Claude Code 業務自動化ナレッジ（週次 2026-11-16）

## 今週のテーマ

今週は「資料作成の自動化を Skills（スキル：Claude に手順書を覚えさせる仕組み）で行う方法」と、「セキュリティの発見→修正を繰り返し回す運用ループ」を中心に集めました。前週までの記事と重複しない新しい出典を選んでいます。

## 1. ITインフラ運用の資料・レポート自動化

### 1-1. Claude Skills で Excel・PowerPoint・PDF を自動生成する
- 出典: https://zenn.dev/ttks/articles/963d86a67a2083
- Anthropic が公開した Skills 機能と公式 Cookbook（サンプル集）を使い、API から Excel / PowerPoint / PDF を作る流れをまとめた記事です。月次の運用レポートなど「毎回同じ形式」の資料に向きます。手順を一度スキル化すれば、担当者が変わっても同じ品質で出せる点が利点です。
- 注意点: 公開から時間が経つ機能のため、最新の公式ドキュメントで仕様を確認してください。

### 1-2. Claude Cowork で Excel・PowerPoint・文書作成を自動化する実践ガイド
- 出典: https://www.oflight.co.jp/ja/columns/claude-cowork-excel-ppt-document-automation-2026
- Cowork（デスクトップで Claude に作業を任せる機能）で、数式が動く Excel やデザイン済みスライドを指示だけで作る例を紹介しています。コード不要なので、運用チームの非エンジニアにも展開しやすいです。
- 注意点: 生成物の数値は必ず元データと突き合わせてください。業者ブログのため効果は鵜呑みにせず小規模で検証するのが安全です。

## 2. ゼロデイ・セキュリティ運用の自動化

### 2-1. Claude Security が「継続スキャン＋修正追跡」に対応
- 出典: https://claude.com/resources/articles/claude-security-now-scans-continuously-and-tracks-fixes
- リポジトリを接続すると、最初に詳細スキャンを行い、その後はコード変更のリスクに応じて自動で再スキャンします。修正が入ると指摘は自動で「修正済み」になり、再発すれば再オープンされます。API と Webhook（イベント通知）で既存の運用ツールにつなげられます。
- 注意点: Claude Enterprise 向けの公開ベータ（試験提供）です。利用できる契約かどうか事前に確認が必要です。

### 2-2. LLM でソースコードを守る「発見→修正」6ステップ
- 出典: https://claude.com/blog/using-llms-to-secure-source-code
- 脅威モデル→サンドボックス（隔離環境）→発見→検証→トリアージ（優先度付け）→修正、の6段階を整理した Anthropic の記事です。ボトルネックは脆弱性を「見つけること」より「その後の整理と修正」にある、という指摘は運用設計の参考になります。
- 注意点: 隔離環境の準備が前提です。本番環境で直接試さないでください。

### 2-3. Security Recipes: Claude による脆弱性修正レシピ
- 出典: https://security-recipes.ai/claude
- スキル（手順）・フック（危険な編集を事前に止める仕組み）・MCP（Model Context Protocol、外部ツール連携の規格）を組み合わせ、検出結果から PR（Pull Request、変更提案）作成までを自動化する例です。1回の実行で作る PR 数に上限を設ける案など、暴走防止の考え方が実用的です。
- 注意点: 第三者サイトの情報です。機能の提供状況は公式ドキュメントでも確認してください。

## 3. CI/CD・Playwright による自動化

### 3-1. Claude Code + Playwright MCP + GitHub Actions の3層テスト
- 出典: https://dev.to/kenimo49/claude-code-playwright-mcp-github-actions-3-test-layers-that-actually-kill-regressions-34f6
- 「コードを書いた AI に自分でテストも書かせると自己採点になる」という問題に対し、開発時（TDD用サブエージェント）、PR時（Playwright MCP）、CI時（claude-code-action）で役割を分ける構成です。デグレ（既存機能の不具合）防止に有効です。
- 注意点: 個人ブログの事例です。自環境で小さく検証してから採用してください。

### 3-2. Claude Code GitHub Actions 公式ドキュメント
- 出典: https://code.claude.com/docs/en/github-actions
- PR やイシューで `@claude` と書くと、Claude が分析・修正・コミットまで行う公式機能の一次情報です。課題を PR に変える運用の基礎になります。
- 注意点: ワークフロー権限とシークレット（認証情報）の扱いに注意。過去に Microsoft が指摘したプロンプトインジェクション経路もあるため、信頼できる PR のみ対象にしてください。

## 4. セキュリティ補助（開発中の自動レビュー）

### 4-1. security-guidance プラグイン
- 出典: https://code.claude.com/docs/en/security-guidance
- インストールするだけで、編集時のパターン検査（モデル呼び出し無し＝追加費用なし）、ターン終了時のバックグラウンド審査、コミット時の深い審査の3層で自動チェックします。`.github/workflows/` の編集にも警告が出ます。
- 注意点: 審査は1ターン最大30ファイルまで。最終的な人のレビューは省けません。

## 5. GitHub の awesome シリーズ

### 5-1. awesome-claude-skills 系リストの比較
- 出典: https://www.agensi.io/learn/awesome-claude-skills
- 出典: https://github.com/sujayjayjay/awesome-claude-code-skills
- 前者は5つの awesome リストを規模・更新頻度・リンク切れで比較した記事（2026-11-13 時点）、後者は大量掲載ではなく厳選型のリストです。どれから見るか迷う場合の入口になります。
- 注意点: スキルは実行権限を持つコードです。導入前に作者・Star数・ライセンス・コード内容を必ず確認してください（野良スキル対策）。

## 今週のまとめ
- 定型レポートは Skills 化、セキュリティは「継続スキャン＋人による承認」、CI は役割分担、がキーワード。
- どの事例も「自動適用はせず、最終承認は人」という設計でした。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
