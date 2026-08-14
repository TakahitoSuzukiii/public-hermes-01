# Python: Result / ResultPipeline / Logger パターン(Rustライクなエラーハンドリング)

> ステータス: INFO / カテゴリ: DEV / 作成日 2026-08-15
> ⚠️ マスキング規約準拠。秘密（トークン/鍵）は一切記載しない。ホスト名/ユーザー名/IP 等は placeholder。
> 出典: 自己リポジトリ `public`(python/) を再構成し、最新情報を検証のうえまとめ直したもの。

## 1. これは何か

Python で「例外を投げずに、成功/失敗を明示的な戻り値として扱う」ためのミニマルな設計パターンです。Rust の `Result<T, E>` の考え方を Python に移植したもので、以下の3点セットで構成されます。

- **Result**: 成功(`Ok`)と失敗(`Err`)を型として表現するクラス
- **ResultPipeline**: 複数の処理をチェーンし、途中で失敗したら即座に停止する仕組み
- **Logger / HttpLogger**: 構造化された JSON ログを出力するシンプルなロガー

「最小構成・高可読性・実用性」を重視した、TypeScript 版(後述の別記事)と対になる実装です。

## 2. なぜこのパターンを使うのか(背景の整理)

Python の標準的なエラーハンドリングは `try/except` による例外処理です。これは手軽な反面、以下のような課題があります。

- 関数のシグネチャ(型情報)だけでは「その関数が失敗しうるか」が分からない
- 呼び出し側で catch し忘れると、エラーが握りつぶされるか、逆に上位まで伝播して意図しない場所で落ちる
- 複数の処理をチェーンした際、どこで失敗したのかを追跡しにくい

`Result` 型を使うと、失敗する可能性のある処理は「戻り値の型」として明示され、呼び出し側は `is_ok()` / `is_err()` で明示的に分岐しなければならなくなります。これは静的型チェッカー(mypy 等)と組み合わせることで特に効果を発揮します。

> 補足(最新情報の確認): Rust 本家の `Result<T, E>` は現在も言語の中核機能として現役です(2026年時点)。Python コミュニティでも `returns` ライブラリや `result` パッケージ(PyPI)など、同種の考え方を提供するサードパーティ実装が複数存在し、一定の支持を得ています。本記事のコードは自作の最小実装であり、本番利用では実績のあるライブラリの採用も検討する価値があります。

## 3. コード全体像

```
project/
  result.py           # Result<T, E> 本体
  result_pipeline.py   # チェーン実行用のパイプライン
  logger.py            # 構造化ロガー
  http_logger.py        # HTTPリクエスト/レスポンス専用ロガー
```

### 3.1 Result

```python
from __future__ import annotations
from dataclasses import dataclass
from typing import Generic, TypeVar, Callable, Awaitable, Union

T = TypeVar("T")
E = TypeVar("E")
U = TypeVar("U")


@dataclass
class Result(Generic[T, E]):
    ok: bool
    value: Union[T, None] = None
    error: Union[E, None] = None

    @staticmethod
    def Ok(value: T) -> "Result[T, E]":
        return Result(ok=True, value=value)

    @staticmethod
    def Err(error: E) -> "Result[T, E]":
        return Result(ok=False, error=error)

    def is_ok(self) -> bool:
        return self.ok

    def is_err(self) -> bool:
        return not self.ok

    def unwrap(self) -> T:
        if self.ok:
            return self.value
        raise RuntimeError(f"unwrap() called on Err: {self.error}")

    def unwrap_or(self, default: T) -> T:
        return self.value if self.ok else default

    def map(self, fn: Callable[[T], U]) -> "Result[U, E]":
        if self.ok:
            try:
                return Result.Ok(fn(self.value))
            except Exception as e:
                return Result.Err(e)
        return Result.Err(self.error)

    async def map_async(self, fn: Callable[[T], Awaitable[U]]) -> "Result[U, E]":
        if self.ok:
            try:
                return Result.Ok(await fn(self.value))
            except Exception as e:
                return Result.Err(e)
        return Result.Err(self.error)

    def and_then(self, fn: Callable[[T], "Result[U, E]"]) -> "Result[U, E]":
        if self.ok:
            try:
                return fn(self.value)
            except Exception as e:
                return Result.Err(e)
        return Result.Err(self.error)

    async def and_then_async(self, fn: Callable[[T], Awaitable["Result[U, E]"]]) -> "Result[U, E]":
        if self.ok:
            try:
                return await fn(self.value)
            except Exception as e:
                return Result.Err(e)
        return Result.Err(self.error)
```

ポイント:
- `map` は成功値を別の値に変換する(失敗時は何もしない)
- `and_then` は「次も `Result` を返す関数」をチェーンする(モナドの `bind` に相当)
- `_async` サフィックス付きのメソッドで `async/await` にネイティブ対応

### 3.2 ResultPipeline

```python
from typing import Callable, Awaitable, Any
from .result import Result


class ResultPipeline:
    def __init__(self, initial: Result):
        self.result = initial

    @staticmethod
    def start(value: Any) -> "ResultPipeline":
        return ResultPipeline(Result.Ok(value))

    def pipe(self, fn: Callable[[Any], Result]) -> "ResultPipeline":
        if self.result.is_ok():
            self.result = fn(self.result.value)
        return self

    async def pipe_async(self, fn: Callable[[Any], Awaitable[Result]]) -> "ResultPipeline":
        if self.result.is_ok():
            self.result = await fn(self.result.value)
        return self

    def unwrap(self):
        return self.result.unwrap()

    def get(self) -> Result:
        return self.result
```

複数の処理を `.pipe()` / `.pipe_async()` で連結し、途中で `Err` が発生したらそれ以降の処理をスキップします。

### 3.3 使用例(async パイプライン)

```python
from result import Result
from result_pipeline import ResultPipeline

async def step1(x: int) -> Result[int, str]:
    return Result.Ok(x + 1)

async def step2(x: int) -> Result[int, str]:
    if x > 5:
        return Result.Err("too big")
    return Result.Ok(x * 2)

async def main():
    pipeline = (
        await ResultPipeline.start(2)
        .pipe_async(step1)
        .pipe_async(step2)
    )
    result = pipeline.get()
    print(result)
```

### 3.4 Logger / HttpLogger

```python
import json
from datetime import datetime
from typing import Any, Dict

class Logger:
    def __init__(self, service: str = "app"):
        self.service = service

    def _log(self, level: str, message: str, payload: Dict[str, Any] | None = None):
        log_entry = {
            "timestamp": datetime.utcnow().isoformat(),
            "service": self.service,
            "level": level,
            "message": message,
        }
        if payload:
            log_entry["payload"] = payload
        print(json.dumps(log_entry, ensure_ascii=False))

    def info(self, message: str, payload=None):
        self._log("INFO", message, payload)

    def warn(self, message: str, payload=None):
        self._log("WARN", message, payload)

    def error(self, message: str, payload=None):
        self._log("ERROR", message, payload)
```

`HttpLogger` は `Logger` を継承し、HTTP のリクエスト/レスポンスに特化した `request()` / `response()` メソッドを追加した薄いラッパーです。

> 補足: `datetime.utcnow()` は Python 3.12 以降非推奨(deprecation warning)となっており、`datetime.now(datetime.UTC)` への置き換えが推奨されています。元記事のサンプルコードをそのまま使う場合は、この点だけ最新の書き方に直すとよいでしょう。

## 4. 設計思想まとめ

- **最小構成**: 複雑な抽象化を避け、読みやすさを最優先
- **Rust ライク**: `Result` による明示的な成功/失敗の表現
- **TypeScript 版との思想統一**: 同じ設計思想を言語をまたいで適用(別記事参照)
- **async/await に自然対応**
- **拡張しやすい**: `Logger` を CloudWatch / ファイル / HTTP などに簡単に拡張可能

## 5. 関連記事

- TypeScript版の同パターン、および Zscaler IP自動更新スクリプトへの実践的な適用例は別記事「TypeScript: Result / Logger パターンと CDK 自動更新スクリプト」を参照。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
