作成日: 2026-11-26 / STATUS: INFO / TOPIC: CLAUDESKILLS / 対象期間: 2026-11-19〜2026-11-26

# Claude Skills(Agent Skills)週次ウォッチ 2026-11-26

## 📌 今週のハイライト
- **Skills over MCP が公開ベータ**: MCP(Model Context Protocol=AIと外部システムをつなぐ共通規格)サーバが、ツールと一緒に「スキル」も配れるようになった。
- **Claude の管理画面が「Plugins」に統合**: Skills / Connectors / Plugins の3タブが1つの Plugins ページに。Team プランは 11/30 から順次。
- **Claude Code 2.1.330**: スキルの `model` 設定が、Claudeが起動するサブエージェントには効かなくなった(第三者の検証記事による)。
- 公式リポジトリ(anthropics/skills、agentskills)自体のコミット・リリースは今週ゼロ。

## 🧩 公式の動き
**リポジトリ(取得時点の値)**
- anthropics/skills: コミット・リリースとも今週なし。最終更新(pushed)は 2026-11-16。Star 200,490 / Fork 23,448 / ライセンスは明記なし / Organization。
- agentskills/agentskills(規格の仕様書): 今週の更新なし。最終更新 2026-11-04。Star 27,629 / Apache-2.0 / Organization。

**Claude 側の機能更新(Web検索で確認)**
- **Skills over MCP(公開ベータ)**: MCPサーバがツールと並べてスキル(手順書・ベストプラクティス)を配布できる。必要な時だけ読み込まれるためコンテキスト消費が小さく、サーバ更新と同時にスキルも更新される。Claude と Claude Code で、Pro/Max/Ultra は既定オン、Team は管理者が有効化すると利用可、Enterprise は近日。事例として Shopify・HubSpot・Atlassian が紹介されている。あわせて Tasks(長時間処理を背景実行)と Elicitation(処理中にユーザーへ追加入力を求める)が一般提供(GA)になった。
- **Plugins ページ統合**: 「Customize」が「Plugins」に改名され、スキルはプラグインの一種として「+」または「/」から使う形に。公開プラグインには Verified / Community のラベルが付く。Free〜Ultra は適用済み、Team は 11/30 から段階展開、Enterprise は数週間以内。**注意**: 組織で Skills を無効にしていると、11/30 以降は Claude Desktop でもプラグインが使えなくなる(使い続けるなら 11/30 前に Skills を有効化)。
- **Claude Code 2.1.330(11/20)**: 第三者の検証記事によると、Claudeが自動で起動したスキルの `model` 指定は、サブエージェント等に反映されなくなった(`context: fork` のスキルは従来どおり。スラッシュコマンドで手動実行した場合は反映)。コスト最適化のために `model` を指定していた場合は挙動確認を。※検証者個人の実測であり公式の説明ではない。

## 🌱 注目のスキル集・新着リポジトリ
(取得した候補約20件から、宣伝色が強いもの・用途がスキルと直接関係しないものを除き8件。Star数は取得時点)
- **addyosmani/agent-skills** — コーディングエージェント向けの実務的エンジニアリングスキル集。Star 120,421 / MIT / 作成 2026-02-15 / 最終更新 2026-11-24 / User。https://github.com/addyosmani/agent-skills
- **Graphify-Labs/graphify** — コードやドキュメント、SQLスキーマ等を検索可能な知識グラフにする `/graphify` スキル。Star 153,358 / Apache-2.0 / 作成 2026-04-03 / 最終更新 2026-11-25 / Organization。https://github.com/Graphify-Labs/graphify
- **nextlevelbuilder/ui-ux-pro-max-skill** — UI/UX設計の知見を与えるスキル。Star 154,182 / MIT / 作成 2025-11-30 / 最終更新 2026-11-25 / Organization。https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- **pbakaus/impeccable** — デザイン用語でエージェントを操作・レビューするスキル。Star 116,858 / Apache-2.0 / 作成 2025-11-16 / 最終更新 2026-11-25 / User。https://github.com/pbakaus/impeccable
- **Leonxlnx/taste-skill** — 参考画像とブラウザ確認でデザインの質を上げるスキル。Star 121,539 / MIT / 作成 2026-02-19 / 最終更新 2026-11-25 / User。https://github.com/Leonxlnx/taste-skill
- **mvanhorn/last30days-skill** — Reddit・YouTube・Web等を横断し直近30日の話題を調べるスキル。Star 75,056 / MIT / 作成 2026-01-23 / 最終更新 2026-11-25 / User。https://github.com/mvanhorn/last30days-skill
- **blader/humanizer** — 文章からAI生成っぽさを取り除くスキル。Star 73,572 / MIT / 作成 2026-01-18 / 最終更新 2026-11-19 / User。https://github.com/blader/humanizer
- **heygen-com/hyperframes** — Claude Code等で動画を編集・生成するOSSツール。Star 90,125 / Apache-2.0 / 作成 2026-03-10 / 最終更新 2026-11-25 / Organization。https://github.com/heygen-com/hyperframes

⚠ 第三者製です。導入前に信頼性チェック(コード目視・作者・ライセンス)を。個人(User)運営のものは特に scripts/ の中身を確認してください。

## 🛡 安全に使うために
- スキルは「指示書+実行スクリプト」。野良スキルは **任意コード実行・不審な外部通信・認証情報(トークン等)の窃取** の入口になり得ます。Skills over MCP でサーバ経由でもスキルが届くようになったため、「接続先MCPサーバを信頼できるか」も確認対象になります。
- 導入前チェック: ①Star/Fork(極端に少ない・急増していないか) ②作者(Organization/実績/アカウント作成日) ③最終更新日(放置されていないか) ④ライセンス(明記あり) ⑤`scripts/` と SKILL.md の目視(難読化、curl等の外部送信、環境変数・秘密鍵の参照がないか)。
- Claude の Plugins ページの Verified / Community ラベルは目安の一つ。Community 扱いは自己確認が前提です。

## 🔧 活用の示唆(Hermes/Claude Code)
(筆者の見立て)
- Claude Code を使う場合、2.1.330 でスキルの `model` 指定の挙動が変わった可能性があるため、コスト調整用に使っているスキルがあれば手元で確認すると安全です。
- Skills over MCP は、MCPサーバ+スキルを一体で管理できる設計。Hermes側で MCP 連携を使う際も、ツールとスキルをセットで更新できる方向性は参考になります。
- 外部スキルの導入は、既存の信頼性チェック手順(Star・作者・ライセンス・scripts目視)を引き続き適用するのが妥当です。

## ℹ この記事の見方
- 取得方法: GitHub 公式API(リポジトリのメタ情報・コミット・リリース・検索)。Claude側の更新は公式ヘルプ/ブログと報道をWeb検索で確認。
- Star数等は取得時点(2026-11-26朝)の値。
- 取得できなかった情報源: なし(8/8 成功)。

## 出典
- https://github.com/anthropics/skills
- https://github.com/agentskills/agentskills
- https://claude.com/resources/articles/skills-over-mcp-tasks-and-more
- https://support.claude.com/en/articles/17740565-manage-plugins-skills-and-connectors-from-one-plugins-page
- https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- https://thenextweb.com/news/anthropic-claude-skills-over-mcp-tasks-elicitation
- https://gloss.run/post/when-claude-runs-your-skill-its-model-line-now-does-nothing
- https://api.github.com/ (リポジトリ・検索API)

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
