# AWS Bedrock Guardrails APIによる機密情報マスキング — 技術調査ノート

- **記録日:** 2026-08-29
- **位置づけ:** RAG(検索拡張生成)構築における「機密情報のマスキング」という課題に対し、AWS Bedrock Guardrails APIの活用可否を公式ドキュメントベースで調査した記録。

## 背景・目的

生成AI・RAG構築において、取り込むデータに機密情報(PII: 個人を特定しうる情報など)が含まれる場合、それを安全にマスキング・クレンジングしてから活用したいという要件がある。AWS Bedrock Guardrailsの `ApplyGuardrail` APIを使えば、この課題を解消できるのではないか、という仮説のもと、公式ドキュメントを調査した。

## 調査結果

### 1. `ApplyGuardrail` API の概要

[公式ドキュメント](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-use-independent-api.html)によると、`ApplyGuardrail` APIは以下の特徴を持つ。

- **基盤モデル(LLM)を呼び出さずに**、任意のテキストをGuardrailsのポリシーでチェック・マスキングできるスタンドアロンAPI
- リクエスト形式:

```
POST /guardrail/{guardrailIdentifier}/version/{guardrailVersion}/apply
{
  "source": "INPUT" | "OUTPUT",
  "content": [{"text": {"text": "対象テキスト"}}]
}
```

- レスポンスの `action` が `GUARDRAIL_INTERVENED`(介入あり)の場合、`outputs` にマスキング後のテキストが返る(例: `{NAME}`, `{EMAIL}` のようなプレースホルダーに置換)

### 2. マスキング可能なPII種別

[Remove PII from conversations](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-sensitive-filters.html)によると、General(氏名・住所・メールアドレス・電話番号・パスワード等)、Finance(クレジットカード番号・銀行口座番号等)、IT(IPアドレス・AWSアクセスキー等)、US固有(社会保障番号等)の4カテゴリで30種類以上の標準PIIタイプをサポートしている。加えて、カスタム正規表現による独自PII定義も可能。

### 3. データ形式に関する重要な制約

- APIが受け付けるのは**プレーンテキスト(`text`フィールド)のみ**
- **JSON/CSVのような構造化データを直接渡す仕組みはない**。アプリケーション側で構造化データをパースし、テキスト化してからAPIへ渡す必要がある
- レスポンスもテキストで返るため、元の構造(JSONのキーやCSVのカラム対応関係)を維持したい場合は、アプリ側で「どのテキスト片がどのフィールドに対応するか」を管理する設計が必要になる

### 4. RAG(検索拡張生成)での活用を想定した場合の設計上の論点

RAGでは一般的に、原文データを「セマンティックチャンク」(意味のあるまとまり)に分割し、それぞれをベクトル化(embedding)してベクトルストアへ格納する。この文脈でGuardrailsを組み込む場合、以下の点に注意が必要と考えられる。

- **マスキングのタイミング:** embedding化(ベクトル化)する前に、必ずマスキングを完了させておくべきである。先にベクトル化してしまうと、機密情報がベクトル(埋め込み表現)に不可逆的に反映されてしまい、後からの除去が困難になるため
- **セマンティックチャンクとマスキングの両立:** Guardrailsのapply guardrail APIはテキスト単位でしか処理を意識しないため、「意味のあるまとまり(チャンク)を維持したまま、機密情報だけを的確に除去する」という理想の両立は、現状のAPI仕様だけでは難しい部分が残る。チャンク内の一部をマスキングすることで、文脈としての意味が損なわれる可能性があるため
- **格納先の選択肢:** 最終的な格納先はベクトルストアに限らず、全文検索インデックス、RDB、グラフDBなど複数の選択肢があり得る。「ベクトルストア前提」で設計を固めすぎず、目的に応じて柔軟に構成を検討することが望ましい

## 結論

- **技術的には実現可能。** `ApplyGuardrail` APIを使えば、テキストデータに含まれる機密情報を検出・マスキングすることができる
- ただし、**JSON/CSV等の構造化データをそのまま渡せる訳ではなく**、アプリケーション側でのテキスト化・再構築処理が別途必要
- **RAG文脈でのセマンティックチャンクとの両立は、依然として設計上の課題として残る**。今後の検証・設計方針の検討が必要な領域

## 参考リンク

- [Use the ApplyGuardrail API in your application - Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-use-independent-api.html)
- [Remove PII from conversations by using sensitive information filters - Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails-sensitive-filters.html)
- [GuardrailPiiEntityConfig - Amazon Bedrock API Reference](https://docs.aws.amazon.com/bedrock/latest/APIReference/API_GuardrailPiiEntityConfig.html)
