# ECS Express AI Agent ワークショップ

Next.js、NestJS、Prisma アプリを AI エージェント（Claude Code）を使って AWS ECS Express Mode 上で開発するハンズオンワークショップです。

各 `step-*` ディレクトリはプロジェクトの自己完結型スナップショットです。各ステップの `prompts.md` に従って AI エージェントにプロジェクトを次のステップへ進化させましょう。

## ステップ

### [step-0](step-0/README.ja.md) — ゼロからスタート

空のディレクトリです。プロンプトに従ってすべてをゼロから作成します。

**次へ:** [step-0/prompts.md](step-0/prompts.md) に従って、Docker Compose と Playwright E2E テストを含む Next.js プロジェクトを作成します。

### [step-1](step-1/README.ja.md) — 空の Next.js アプリ

出発点：空の Next.js App Router プロジェクトに、ローカル開発用の Docker Compose と Playwright E2E テストが含まれています。バックエンドやインフラはありません。

**含まれるもの:**
- Next.js 16 App Router（TypeScript）
- Docker Compose（`web` + `web-e2e-tests` サービス）
- Playwright スモークテスト

**次へ:** [step-1/prompts.md](step-1/prompts.md) に従って、AWS インフラ（Terraform）、CI/CD（GitHub Actions）、本番用 Docker ビルドを追加します。

### [step-2](step-2/README.ja.md) — ECS Express Mode 上の Next.js

Next.js アプリに、AWS ECS Express Mode へデプロイするための Terraform IaC と GitHub Actions による CI/CD が含まれています。フロントエンドのみで、バックエンドやデータベースはありません。

**step-1 からの追加内容:**
- Terraform IaC（永続: VPC、ECR、IAM；エフェメラル: ECS Express Gateway）
- GitHub Actions ワークフロー（E2E テスト、イメージビルド/プッシュ、IaC plan/apply）
- Web 用本番 Dockerfile
- OIDC セットアップとクラウドデプロイドキュメント

**次へ:** [step-2/prompts.md](step-2/prompts.md) に従って、ヘルスチェックと Git SHA 表示を備えた最小限の NestJS バックエンドを追加します。

### [step-3](step-3/README.ja.md) — ECS Express Mode 上の Next.js + NestJS（ヘルスチェック）

Next.js フロントエンドと最小限の NestJS バックエンド（GIT_SHA 付きヘルスチェックと Swagger）を、AWS ECS Express Mode にデプロイします。

**step-2 からの追加内容:**
- NestJS 11 バックエンド（`GET /health` エンドポイント、Git SHA を返す）
- Swagger UI（`/api`、非本番環境）
- バックエンド用 Dockerfile、ECR リポジトリ、セキュリティグループ、ECS Express Gateway サービス
- Web アプリがバックエンドの Git SHA を取得・表示
- Docker Compose にバックエンドサービスを追加

**次へ:** [step-3/prompts.md](step-3/prompts.md) に従って、PostgreSQL、Prisma ORM、Items CRUD を追加します。

### [step-4](step-4/README.ja.md) — ECS Express Mode 上の Next.js + NestJS（Items CRUD）

Next.js フロントエンドと、ヘルスチェックおよび Items CRUD（PostgreSQL + Prisma）を備えた NestJS バックエンドを、AWS ECS Express Mode にデプロイします。

**step-3 からの追加内容:**
- PostgreSQL 17 データベース
- Prisma ORM（Item モデル）
- Items CRUD API（`POST /items`、`GET /items`、`DELETE /items/:id`）— 認証なし
- Web アプリにアイテム一覧、作成フォーム、削除ボタン
- Items E2E テスト
- Terraform に RDS PostgreSQL、プライベートサブネット、NAT ゲートウェイ
- DATABASE_URL 用 Secrets Manager

**次へ:** [step-4/prompts.md](step-4/prompts.md) に従って、メール/パスワード認証（JWT）とユーザースコープのアイテムを追加します。

### [step-5](step-5/README.ja.md) — ECS Express Mode 上の Next.js + NestJS（認証 + Items CRUD）

Next.js フロントエンドと、メール/パスワード認証（JWT）およびユーザースコープの Items CRUD（PostgreSQL + Prisma）を備えた NestJS バックエンドを、AWS ECS Express Mode にデプロイします。

**step-4 からの追加内容:**
- メール/パスワードによるサインアップ・サインイン（JWT トークン）
- Prisma の User モデル（ユーザースコープのアイテム）
- Items エンドポイントに JWT 認証ガード（所有権チェック）
- サインイン・サインアップページ（AuthContext 付き）
- ダッシュボード（ユーザープロフィール）と認証済みアイテムページ
- ナビゲーションヘッダー（ダッシュボード、アイテム、サインアウト）
- Terraform に JWT シークレットと DATABASE_URL 用 Secrets Manager

**次へ:** [step-5/prompts.md](step-5/prompts.md) に従って、OAuth2、メール認証、TOTP MFA、国際化を追加します。

### [step-final](step-final/README.ja.md) — フルスタックアプリ

すべての機能を備えた完成版アプリケーション — OAuth2 認証、メール認証、TOTP MFA、国際化など。

**step-5 からの追加内容:**
- OAuth2 認証（Apple、Discord、GitHub、Google、X/Twitter）
- メール認証とパスワードリセットフロー
- TOTP MFA（二要素認証）とリカバリーコード
- SMTP メール連携（ローカル開発用 Mailpit）
- 国際化（英語 + 日本語）
- OAuth プロバイダーのアカウントリンク/リンク解除
- 設定ページ（メール、MFA、連携アカウント、テーマ）
- バックエンドと Web の完全な E2E テストスイート

## 前提条件

- Docker Engine + Docker Compose（例: [Docker Desktop](https://www.docker.com/products/docker-desktop/)、[Podman](https://podman.io/)、[Colima](https://github.com/abiosoft/colima)）
- AI コーディングエージェント（例: [Claude Code](https://claude.ai/claude-code)）

## 使い方

1. ステップディレクトリを選択（`step-0/` または `step-1/` から開始）
2. AI エージェントで開く
3. `prompts.md` のプロンプトに従って次のステップに向けてビルド
4. 結果を次のステップディレクトリと比較

## ライセンス

[MIT](LICENSE)
