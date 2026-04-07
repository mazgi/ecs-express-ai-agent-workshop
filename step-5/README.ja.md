# Step 5 — ECS Express Mode 上の Next.js + NestJS（認証 + Items CRUD）

Next.js フロントエンドと、メール/パスワード認証（JWT）およびユーザースコープの Items CRUD（PostgreSQL + Prisma）を備えた NestJS バックエンドを、AWS ECS Express Mode にデプロイします。

## サービス

| サービス | 技術 | ポート |
|---------|------|--------|
| backend | NestJS 11 + PostgreSQL 17 + Prisma + JWT Auth | 4000 |
| web | Next.js 16 | 3000 |

## 前提条件

- Docker Engine + Docker Compose（例: [Docker Desktop](https://www.docker.com/products/docker-desktop/)、[Podman](https://podman.io/)、[Colima](https://github.com/abiosoft/colima)）

## クイックスタート

```sh
cp .example.secrets.env .secrets.env
docker compose up
```

| URL | 説明 |
|-----|------|
| http://localhost:4000/health | バックエンドヘルスチェック |
| http://localhost:4000/api | Swagger UI |
| http://localhost:3000 | Web |

## バックエンド API

- `POST /auth/signup` — メール/パスワードで登録（JWT トークンを返す）
- `POST /auth/signin` — メール/パスワードでサインイン
- `POST /auth/refresh` — アクセストークンのリフレッシュ
- `GET /auth/me` — 現在のユーザーを取得（JWT 必須）
- `DELETE /auth/account` — アカウント削除（JWT 必須）
- `POST /items` — アイテム作成（JWT 必須）
- `GET /items` — ユーザーのアイテム一覧（JWT 必須）
- `DELETE /items/:id` — アイテム削除（JWT 必須、所有権チェック）

## プロジェクト構成

```
.
├── compose.yaml
├── backend/               # NestJS API（認証 + アイテム）
│   └── prisma/            # Prisma スキーマ（User + Item モデル）
├── web/
│   ├── app/               # Next.js App Router
│   └── e2e-tests/         # Playwright E2E テスト
├── iac/                   # Terraform IaC（AWS）
├── Dockerfiles.d/
├── .github/               # GitHub Actions ワークフロー + カスタムアクション
└── docs/
```
