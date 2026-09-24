作成日: 2026-09-19 / STATUS: INFO / TOPIC: AIAGENT

# Jevの具体的な使い方:指示・出力の判断・活用方法

- **記録日:** 2026-09-19
- **位置づけ:** 「新AIモデル基盤System One Models & Jev」記事の続編。TypeSafe AI公式ドキュメント(docs.typesafe.ai)に基づき、Jevへの具体的な指示方法、出力(確信度付き回答)の判断基準、コードでの活用方法を実例つきで整理する。

## 1. どう指示するか:「state(状況)」+「questions(質問)」の2要素

Jevへのリクエストは、Claudeのような自由な会話プロンプトではなく、**「① 判断対象のデータ(state)」+「② それについて知りたい質問(questions)」**という、非常にシンプルな2要素の組み合わせ。

### 具体例:カスタマーサポートのチケット分類

```json
POST https://api.typesafe.ai/v1/systemone

{
  "state": "Hi, I've been trying to connect my Stripe account for 3 days and the integration keeps failing. I'm losing sales. Please help ASAP.",
  "model": "jev-latest",
  "questions": {
    "department": {
      "type": "choice",
      "instructions": "Which team should handle this",
      "criteria": {
        "billing": "Payment or subscription issues",
        "technical": "Bugs or integration problems",
        "sales": "Pricing or account questions"
      }
    },
    "frustration": {
      "type": "score",
      "instructions": "How frustrated the customer appears",
      "criteria": ["Calm, just stating facts", "Frustrated but civil", "Very angry, strong language"]
    },
    "is_urgent": {
      "type": "noul",
      "instructions": "The message conveys urgency or time-sensitivity"
    }
  }
}
```

### 3種類の質問タイプ(プリミティブ)を使い分ける

| 質問タイプ | 使う場面 | 具体例 |
|---|---|---|
| **Choice(選択)** | 順序のない選択肢から1つ選ばせたい | 「どの部署が対応すべきか」「文書の種類は?」 |
| **Score(段階評価)** | スペクトラム上の位置を測りたい | 「顧客の不満度」「バグの深刻度」「スキルレベル」 |
| **Noul(はい/いいえ)** | 確率そのものが意味を持つyes/no判定 | 「個人情報が含まれているか」「返金を要求しているか」 |

### 設計原則(公式ドキュメントの推奨)

Jevには**「1つの質問につき、人間が一瞬で下せる程度の単純な判断」だけを聞く**のがコツ。「このメッセージへの最適な対応を分析して決定して」のような複雑な複合判断は**Jevに直接聞かず**、「市場規模は?」「技術的実現性は?」「差別化要因は?」のように**小さな質問に分解し、その答えをコード側で組み合わせて最終判断を出す**、という設計思想になっている。

## 2. どう出力を判断するか:「答え」と「確信度」をセットで見る

### 返ってくる出力(レスポンス例)

```json
{
  "model": "jev-1.13.0",
  "answers": {
    "department": {
      "type": "choice",
      "choice": "technical",
      "confidence": 0.78,
      "probabilities": { "technical": 0.85, "sales": 0.0, "billing": 0.15 }
    },
    "frustration": {
      "type": "score",
      "score": 1.0,
      "confidence": 1.0,
      "legend": { "0": "Calm...", "1": "Frustrated but civil", "2": "Very angry..." }
    },
    "is_urgent": { "type": "noul", "noul": 1.0 }
  },
  "usage": { "input_tokens": 392, "output_tokens": 65 }
}
```

各回答タイプごとに、判断材料となる情報が付いてくる。

- **Choice**:`choice`(選ばれた選択肢)+`probabilities`(全選択肢への確率分布)+`confidence`(その分布がどれだけ1点に集中しているかを表す0〜1の数値)
- **Score**:`score`(段階の位置、2段階の間の値も取りうる)+`confidence`
- **Noul**:`noul`という0〜1の確率値そのものが答え。1に近いほど強いYes、0に近いほど強いNo、0.5に近いほど「わからない」

### confidence(確信度)を使った「判断の3段階ルール」(公式推奨パターン)

これがJev活用の核心部分。公式ドキュメントは**confidenceの値によって、システムの振る舞いを3段階に分けること**を推奨している。

| confidenceの範囲 | 推奨される振る舞い |
|---|---|
| **高い(例:0.8以上)** | **自動で処理を進める**。モデルの判断が明確なので、人間を介さず即座にアクションを実行してよい |
| **中程度** | **慎重に進める**。妥当な答えだが確実ではないため、ユーザーに確認を求める、レビューにフラグを立てる、追加情報を集めてから行動する等 |
| **低い** | **行動しない**。人間に回す、追加の説明を求める、別のシステムにフォールバックする。「モデルが判断材料不足を正直に伝えている」状態と捉える |

公式ドキュメントは**「知的なシステム(人間でも機械でも)が正直に"わからない"と言えなければ、そのシステムは信頼できない」**と述べており、confidenceは単なる付加情報ではなく、**「moderate/low confidenceのケースを人間の判断に委ねる」という安全装置そのもの**として設計されている。

## 3. どう出力を使うか:コードの中で「if文」「閾値」として直接使う

Choiceの答えは、そのままコードの分岐(if/switch)に対応させる。

```python
from typesafe_sdk import Choice, Noul, Score, TypeSafeClient

client = TypeSafeClient()  # 環境変数 TYPESAFE_API_KEY を自動で読む

response = client.system_one(
    state=ticket_text,
    questions={
        "department": Choice(
            instructions="Which team should handle this",
            criteria={
                "billing": "Payment or subscription issues",
                "technical": "Bugs or integration problems",
                "sales": "Pricing or account questions",
            },
        ),
        "frustration": Score(
            instructions="How frustrated the customer appears",
            criteria=["Calm, just stating facts", "Frustrated but civil", "Very angry, strong language"],
        ),
        "is_urgent": Noul(instructions="The message conveys urgency or time-sensitivity"),
    },
)

print(response.answers["department"].choice)     # "technical" → そのままルーティング先に使う
print(response.answers["frustration"].score)      # 1.0 → 閾値判定に使う
print(response.answers["is_urgent"].noul)          # 1.0 → if is_urgent > 0.8: の条件式に使う
```

実務での使い方は以下の流れになる。

1. **`department.choice`(文字列)を、そのままルーティング先の関数呼び出しやキュー振り分けに直接使う**(`if choice == "technical": route_to_tech_team()`)
2. **`frustration.score`(数値)を、閾値と比較してエスカレーション判定に使う**(`if score >= 1.5: escalate_to_manager()`)
3. **`is_urgent.noul`(0〜1の確率)を、しきい値でif分岐に使う**(`if noul > 0.7: send_priority_alert()`)
4. **`confidence`が低いケースだけ、人間のレビューキューに送る**という安全弁を全体にかぶせる

## まとめ:Jevは「AIへの質問」ではなく「型付きの関数呼び出し」として使う

Jevは**「非構造化データを入れると、型付きの確率的判断が返ってくる関数」**として設計されている。Claude等のLLMのように「自由に会話して答えを引き出す」のではなく、**「あらかじめ定義した選択肢・段階・yes/no質問のリストに対して、確信度付きの答えを高速に返してもらい、その答えをコードのif文・閾値判定にそのまま組み込む」**という、ソフトウェア的な使い方が前提になっている。

## 情報源の注記

調査中に`jev-ai-guide.com`・`jevai.org`・`jevapi.dev`のような非公式ドメインが多数見つかったが、内容の信頼性が未確認のため本記事では使用せず、**公式ドメイン(typesafe.ai / docs.typesafe.ai)のみを情報源**としている。

## 参考リンク

- TypeSafe AI公式ドキュメント「Quick start」: <https://docs.typesafe.ai/introduction/quickstart>
- TypeSafe AI公式ドキュメント「Primitives (Questions)」: <https://docs.typesafe.ai/primitives>
- TypeSafe AI公式ドキュメント「Confidence」: <https://docs.typesafe.ai/confidence>
- 元記事(TypeSafe AI、2026-09-15): <https://typesafe.ai/blog/introducing-system-one-models-and-jev>

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
