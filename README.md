# AUN Infrastructure

バックエンド・フロントエンド・データベースを統合管理するインフラリポジトリです。

## 構成

```
aun_infrastructure/
├── docker-compose.yml           # 共通設定 (base)
├── docker-compose.override.yml  # ローカル開発用 (自動適用, gitignore)
├── docker-compose.prod.yml      # 本番用
├── .env.example                 # 環境変数テンプレート
├── aun_back/                    # サブモジュール (FastAPI + SQLModel)
└── aun_front/                   # サブモジュール (Next.js)
```

## 技術スタック

| レイヤー | 技術 |
|----------|------|
| フロントエンド | Next.js 16 / React 19 / TypeScript |
| バックエンド | FastAPI / SQLModel / Alembic |
| データベース | PostgreSQL 18 |
| コンテナ | Docker Compose |

## セットアップ

### 1. リポジトリのクローン

```bash
git clone --recurse-submodules https://github.com/Konit611/AUN_Infrastructure.git
cd AUN_Infrastructure
```

既にクローン済みの場合、サブモジュールを取得するには：

```bash
git submodule update --init --recursive
```

### 2. 環境変数の設定

```bash
cp .env.example .env
# .env を編集してDB_PASSWORDなどを設定
```

### 3. Docker Composeで起動

#### ローカル開発

```bash
docker compose up
```

`docker-compose.override.yml` が自動で適用されます（DB外部ポート開放、DEBUGモードなど）。

#### 本番デプロイ

- **フロントエンド**: Vercel (Next.js native)
- **バックエンド**: Render (Docker)
- **データベース**: Supabase Postgres
- **画像ストレージ**: Supabase Storage (S3 互換)

| サービス | URL |
|----------|-----|
| フロントエンド | https://aun-sake.com |
| バックエンド | https://api.aun-sake.com |
| API ドキュメント | https://api.aun-sake.com/docs |

## サブモジュールの操作

### サブモジュールを最新に更新

```bash
git submodule update --remote
```

### サブモジュール内での作業後

```bash
cd aun_back
# 変更をコミット＆プッシュ
git add . && git commit -m "変更内容" && git push

# infrastructureに戻って参照を更新
cd ..
git add aun_back
git commit -m "Update aun_back submodule ref"
```

## 本番デプロイ手順

> Vercel + Render + Supabase 構成への移行中。詳細手順は別途整備予定。

## データベースマイグレーション

### ローカル開発 DB（Docker）

```bash
cd aun_back

# マイグレーションファイルを自動生成
uv run alembic revision --autogenerate -m "説明"

# マイグレーションを実行
uv run alembic upgrade head

# 1つ前に戻す
uv run alembic downgrade -1
```

### 本番 DB（Supabase）にローカルから直接実行

`config.py` が実行ディレクトリの `.env` を読むため、ルートの `.env` を `aun_back/` に一時コピーして実行する。

```bash
# ルートの .env を本番用に設定してから実行
cp .env aun_back/.env && cd aun_back && uv run alembic upgrade head; rm -f .env; cd ..
```

> **Note**: EC2 でコンテナを再起動すると `entrypoint.sh` が自動で `alembic upgrade head` を実行するため、通常は EC2 デプロイ時に自動適用される。ローカルから直接実行するのは緊急時や検証時のみ。
