# .env による環境変数・シークレット管理設計テンプレ（TypeScript / Python）

> **対象**: `.env` ファイルを使った環境変数管理を、コードに秘密情報を書かずに安全に設計したい開発者向け。
> **作成日**: 2026-08-15（JST） / **ステータス**: INFO（情報提供・設計テンプレート）
> **一次情報**: [python-dotenv公式（PyPI）](https://pypi.org/project/python-dotenv/)、[The Twelve-Factor App — III. Config](https://12factor.net/config)
> **元記事**: public2リポジトリ `env/env.md` を再構成（内容はweb_searchで裏取りし加筆修正）

---

## 用語ミニ解説（初心者向け）

- **環境変数（environment variable）**: OS・実行環境が持つキー・バリュー形式の設定値。プログラムはコードを変更せずに動作を切り替えられる。
- **.env ファイル**: 環境変数をローカル開発用にまとめて記述するテキストファイル。`dotenv` 系ライブラリで読み込む。
- **シークレット管理サービス**: AWS Secrets Manager や Parameter Store のように、パスワード・APIキー等を暗号化して一元管理するクラウドサービス。本番運用では `.env` ファイルより優先すべき手段。

---

## 0. 前提ルール（共通・最重要）

- **コードに秘密情報を直接書かない**
- **`.env` はGit管理しない**（`.gitignore` に必ず追加）
- **本番のシークレットはクラウド側（Secrets Manager / Parameter Store 等）に寄せる**
- **コンテナイメージに秘密情報を焼き込まない**（ビルド時に `.env` をコピーしない）

> ⚠️ **セキュリティ注記（2026年時点の実態調査より）**: `.env` ファイルの誤コミットによる秘密情報漏洩は依然として多発しているインシデントパターン。GitGuardianの調査でも、有効なシークレットが漏洩したリポジトリの一定割合が `.env` 由来と報告されている。チーム開発では `.env` 運用だけに頼らず、シークレットスキャン（pre-commitフック等）の併用が推奨される。

---

## 1. TypeScript プロジェクト向け .env 設計テンプレ

### 想定構成

- ランタイム: Node.js（TypeScriptビルド済み）
- ライブラリ: `dotenv`（.envファイル読み込み）, `zod`（型安全なバリデーション）
- 実行環境: Docker / Docker Compose / クラウド

### ディレクトリ構成例

```text
project/
  src/
    index.ts
    env.ts
  dist/
  .env.local
  .env.example
  package.json
  tsconfig.json
  docker-compose.yml
  Dockerfile
```

### `.env.example`（サンプル・共有用。値はダミー）

```env
NODE_ENV=development
PORT=3000
DISCORD_TOKEN=<your-discord-token>
DATABASE_URL=postgres://<user>:<password>@localhost:5432/app
LOG_LEVEL=debug
```

- 目的: 「何が必要な環境変数か」をチームで共有する
- ポイント: 値はダミー（`<...>` プレースホルダ）にする。本物は絶対に書かない

### `src/env.ts`（型安全な環境変数ラッパ）

```ts
import { z } from "zod";
import dotenv from "dotenv";

dotenv.config(); // .env.local or .env をロード

const EnvSchema = z.object({
  NODE_ENV: z.enum(["development", "test", "production"]).default("development"),
  PORT: z.string().default("3000"),
  DISCORD_TOKEN: z.string(),
  DATABASE_URL: z.string().url(),
  LOG_LEVEL: z.string().default("info"),
});

export const env = EnvSchema.parse(process.env);
```

`zod` でスキーマ検証することで、必須の環境変数が未設定のまま起動する事故を防げる（起動時に例外を投げる）。

---

## 2. Python プロジェクト向け .env 設計テンプレ

### 想定構成

- ランタイム: Python 3.x
- ライブラリ: `python-dotenv`, `pydantic-settings`
- 実行環境: Docker / Docker Compose / クラウド

### `.env.example`

```env
ENV=development
PORT=8000
DISCORD_TOKEN=<your-discord-token>
DATABASE_URL=postgres://<user>:<password>@localhost:5432/app
LOG_LEVEL=debug
```

### `settings.py`（Pydanticで型安全に）

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    env: str = "development"
    port: int = 8000
    discord_token: str
    database_url: str
    log_level: str = "info"

    class Config:
        env_file = ".env.local"  # ローカル開発用
        env_file_encoding = "utf-8"

settings = Settings()
```

> 本番環境では `.env.local` を使わず、環境変数で直接上書きする（Pydanticは環境変数を優先して読む）。

`python-dotenv` の公式ドキュメントでは、複数の`.env`ファイルを階層的にマージする使い方も提供されている:

```python
from dotenv import dotenv_values

config = {
    **dotenv_values(".env.shared"),  # チーム共有の非機密設定
    **dotenv_values(".env.secret"),  # 個人のシークレット（Git管理外）
    **os.environ,                     # 実行環境の環境変数で最終上書き
}
```

---

## 3. Docker Compose と組み合わせた実践例

TypeScriptアプリ・Pythonアプリ・PostgreSQLの3サービス構成で、`.env.local` を「Composeの変数展開」と「各サービスの環境変数」の両方に使う例。

### `.env.local`

```env
COMPOSE_PROJECT_NAME=sample_app
TS_PORT=3000
PY_PORT=8000
POSTGRES_USER=app
POSTGRES_PASSWORD=<password>
POSTGRES_DB=app
POSTGRES_PORT=5432
DISCORD_TOKEN=<your-discord-token>
DATABASE_URL=postgres://app:<password>@db:5432/app
LOG_LEVEL=debug
```

### `docker-compose.yml`

```yaml
services:
  db:
    image: postgres:15-alpine
    container_name: ${COMPOSE_PROJECT_NAME}-db
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "${POSTGRES_PORT}:5432"
    volumes:
      - db-data:/var/lib/postgresql/data

  app-ts:
    build:
      context: ./ts-app
    env_file:
      - .env.local
    ports:
      - "${TS_PORT}:3000"
    depends_on:
      - db

  app-py:
    build:
      context: ./py-app
    env_file:
      - .env.local
    ports:
      - "${PY_PORT}:8000"
    depends_on:
      - db

volumes:
  db-data:
```

### ポイント整理

- `${変数名}` はCompose自身が `.env.local` から読んで展開する（ポート番号やプロジェクト名など）
- `env_file: .env.local` は各コンテナ内のアプリから `process.env` / `os.environ` として参照される
- 本番運用への切り替え時は、`.env` ファイルへの依存を減らし、Secrets Manager / Parameter Store 等のクラウドサービスに寄せる

---

## まとめ（運用の指針）

- **ローカル開発**: `.env.local` に実値を書いてOK（ただしGit管理しない）。TypeScript/Pythonともに型安全なバリデーション（zod/pydantic）をかませて起動時に不備を検知する。
- **本番**: `.env` ファイルは極力使わず、環境変数＋クラウドのシークレット管理サービスに寄せる。コンテナイメージに秘密情報を焼き込まない。
- **チーム運用**: `.env.example` で必要な変数一覧を共有しつつ、pre-commitフック等でシークレットの誤コミットを機械的に検知する仕組みを併用するとより安全。

## Author and Ownership / 著作権と所属について

This project was created as a personal initiative and is not connected to any organization or group.
It is published as an individual creative work.

本プロジェクトは個人の活動として作成したものであり、特定の組織や団体の業務とは関係ありません。
個人の創作物として公開しています。
