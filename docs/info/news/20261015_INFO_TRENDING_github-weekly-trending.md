作成日: 2026-10-15 / STATUS: INFO / TOPIC: TRENDING

# GitHub 週次トレンド（2026-10-15）

前回（2026-10-08）との比較です。対象はスター1万以上の開発者向けリポジトリ（調査対象プール450件）。「Risers」は前週比でスターが増えた順、「Newcomers」は今回プールに新しく入ったリポジトリです（新規作成ではなく、基準を超えて集計対象になったという意味です）。データは GitHub 公式 REST Search API から取得しています。

## 今週の傾向
- **AIエージェント周辺ツール（skills／harness／図解／動画生成）が引き続き主役。** ponytail、ECC、orca、archify など Claude Code 系の強化部品が上位に並びます。
- **「ローカル完結」「リバースエンジニアリング」系の伸びが目立つ。** VoiceStudio（ローカル音声AI）、ghidra（逆アセンブラ）、Newcomersの rea（エージェントで解析）が揃って登場しました。
- 優先トピックでは **claude・typescript・python** が多数。**rust** は cc-switch と photocraft、**go／docker／nix** は nixery が注目枠に入っています。

## 前週比の伸び（Risers）上位15件
- **[debpalash/VoiceStudio](https://github.com/debpalash/VoiceStudio)** — 概要: 完全ローカルで動く ElevenLabs 代替（音声クローン、吹替、文字起こし、オーディオブック作成）。注目理由: 今週最大の伸び（+13,276）。スター68,364／Python。
- **[mattpocock/skills](https://github.com/mattpocock/skills)** — 概要: 著者の `.agents` ディレクトリを公開した、実務者向けエージェント用スキル集。注目理由: +11,563、総スター最大級。スター292,426／Shell。
- **[cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design)** — 概要: Claude Code や Cursor 等向けの図解デザイン。44種類の図を HTML＋SVG で生成。注目理由: +9,877。スター55,768／HTML／claude。
- **[eternity4719/HowToLiveBetter](https://github.com/eternity4719/HowToLiveBetter)** — 概要: 健康・お金・法律・育児などの生活情報を、論文や公的資料の出典付きでまとめた中国語の指南書。注目理由: +9,555（2週連続の急伸）。スター63,792／HTML。
- **[bilawalsidhu/gods-eye-view](https://github.com/bilawalsidhu/gods-eye-view)** — 概要: ブラウザ上の「スパイ衛星シミュレータ」。実データを3D地球儀に表示。注目理由: +7,728。特徴: フライト追跡など地理空間情報を可視化。スター56,797／JavaScript。
- **[NationalSecurityAgency/ghidra](https://github.com/NationalSecurityAgency/ghidra)** — 概要: 米NSA製のソフトウェア・リバースエンジニアリング基盤。注目理由: +6,712。スター88,380／Java。
- **[DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)** — 概要: AIエージェントを「怠け者のシニア開発者」のように考えさせ、不要なコードを書かせない工夫集。+5,877。スター164,186／JavaScript／claude。
- **[stablyai/orca](https://github.com/stablyai/orca)** — 概要: 複数のコーディングエージェントを並列運用する開発環境（デスクトップ／モバイル）。+5,429。スター93,193／TypeScript。
- **[heygen-com/hyperframes](https://github.com/heygen-com/hyperframes)** — 概要: HTMLを書けば動画をレンダリングできる、エージェント向けの仕組み。+5,278。スター64,302／TypeScript。
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** — 概要: エージェントの性能最適化システム（スキル・メモリ・セキュリティ等）。+4,706。スター280,052／JavaScript／claude。
- **[deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness)** — 概要: 「すべてがプラグイン」のエージェント実行基盤。+4,536。スター250,322／TypeScript。
- **[tt-a1i/archify](https://github.com/tt-a1i/archify)** — 概要: アイデアやコードから対話型の図を作るエージェント用スキル。+4,225。スター83,962／JavaScript。
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — 概要: 文書やテーマからネイティブ形式のPowerPointを生成するAI。+4,103。スター62,396／Python。
- **[mksglu/context-mode](https://github.com/mksglu/context-mode)** — 概要: コーディングエージェントのコンテキスト消費を抑える仕組み（ツール出力をサンドボックス化、セッション記憶、MCP＋フック）。+3,974。スター29,668／TypeScript／claude・openclaw。
- **[rohitg00/ai-engineering-from-scratch](https://github.com/rohitg00/ai-engineering-from-scratch)** — 概要: AIエンジニアリングを基礎から学ぶ教材。+3,836。スター69,614／Python。

## 今回のNewcomers（プール新規入り、スター1万以上・上位から）
- **[morluto/rea](https://github.com/morluto/rea)** — エージェントでアプリの挙動からネイティブバイナリまで解析するリバースエンジニアリング支援。263,758／TypeScript。（deepseek-harness のプラグイン系トピック付き）
- **[x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)** — Cursor、Devin など各種AIツールのシステムプロンプト集。144,041。
- **[krahets/hello-algo](https://github.com/krahets/hello-algo)** — アニメ図解付きのデータ構造とアルゴリズム入門（日本語版あり、多言語コード実装）。130,737／Java。
- **[Anduin2017/HowToCook](https://github.com/Anduin2017/HowToCook)** — プログラマー向け家庭料理ガイド。102,807。
- **[microsoft/ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners)** — AIエージェント開発を学ぶ全18レッスン。77,216／Jupyter Notebook。
- **[ansible/ansible](https://github.com/ansible/ansible)** — エージェント不要（SSH利用）のIT自動化基盤。70,975／Python。
- **[storytold/photocraft](https://github.com/storytold/photocraft)** — 純Rustでゼロから書かれたOSSの写真編集ソフト。62,745／Rust（2026-09-30作成の新しいリポジトリ）。
- **[pathwaycom/serviette](https://github.com/pathwaycom/serviette)** — RAG・AIパイプライン・企業内検索の実行可能テンプレート集（Docker対応）。58,795／Python。
- **[DavidHDev/react-bits](https://github.com/DavidHDev/react-bits)** — アニメーション付きReact／Next.jsコンポーネント集。49,266／JavaScript。
- **[boykopovar/AnyPS5](https://github.com/boykopovar/AnyPS5)** — PS5の実行ファイルをLinux／Windowsへ移植するツール。38,127／C++。
- **[tashfeenahmed/freellmapi](https://github.com/tashfeenahmed/freellmapi)** — 複数の無料LLMを1つのOpenAI互換エンドポイントにまとめるゲートウェイ（個人実験用）。35,642／TypeScript。
- **[vercel-labs/skills](https://github.com/vercel-labs/skills)** — `npx skills` で使うオープンなエージェントスキル管理ツール。35,068／TypeScript。
- **[webadderallorg/Recordly](https://github.com/webadderallorg/Recordly)** — 編集スキル不要でデモ動画を作れる録画ツール。33,865／TypeScript。

## 優先トピックの注目枠
- **claude**: ponytail、ECC、archify、diagram-design、orca、context-mode、rea、system-prompts など多数。
- **rust**: cc-switch（144,692。Claude Code・Codex・OpenClaw・Hermes Agent 等を一括管理するデスクトップアプリ。hermes-agent／openclaw トピック付き）、photocraft（62,745）。
- **typescript**: deepseek-harness、orca、hyperframes、context-mode、freellmapi、vercel-labs/skills、Recordly。
- **python**: VoiceStudio、ppt-master、ai-engineering-from-scratch、ansible、serviette、MiroFish（79,419）。
- **go**: nixery（**2,022、1万未満の注目枠**。Nixでイメージを透過的にビルドするコンテナレジストリ／go・docker・nix）。
- **nextjs**: react-bits、bknd（**3,772、1万未満の注目枠**。Firebase／Supabase代替の軽量バックエンド。Next.js等で動作）。
- **angular／typescript**: ghostfolio（**9,449、あと一歩で1万**。Angular＋NestJS製の資産管理OSS）。
- **hermes-agent**: 今週も cc-switch がタグ付け（前週141,482→144,692）。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
