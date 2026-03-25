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
| データベース | PostgreSQL 17 |
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

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

| サービス | URL |
|----------|-----|
| フロントエンド | http://localhost:3000 |
| バックエンド | http://localhost:8000 |
| API ドキュメント | http://localhost:8000/docs |
| PostgreSQL | localhost:5432 (ローカルのみ) |

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

## データベースマイグレーション

```bash
cd aun_back

# マイグレーションファイルを自動生成
uv run alembic revision --autogenerate -m "説明"

# マイグレーションを実行
uv run alembic upgrade head

# 1つ前に戻す
uv run alembic downgrade -1
```
