# ECS Express AI Agent ワークショップ

Next.js、NestJS、Prisma アプリケーションを AI エージェント（[Claude Code](https://claude.ai/claude-code) など）を使って AWS ECS 上で開発するハンズオンワークショップです。

単なるチュートリアルにとどまらず、最終的に構築するアプリケーションは、堅牢なユーザー認証の実装や OAuth2 Identity Provider（IdP）とのシームレスな連携が可能な、本番環境にも対応できる基盤となります。

各 `step-*` ディレクトリはプロジェクトの自己完結型スナップショットです。各ステップの `prompts.md` に従って AI エージェントにコードの記述、インフラのプロビジョニング、プロジェクトの進化を指示し、モダンな AI 駆動の開発ワークフローを体験しましょう。

## 前提条件

- Docker Engine + Docker Compose（例: [Docker Desktop](https://www.docker.com/products/docker-desktop/)、[Podman](https://podman.io/)、[Colima](https://github.com/abiosoft/colima)）
- AI コーディングエージェント（例: [Claude Code](https://claude.ai/claude-code)）

## 使い方

1. ステップディレクトリを選択（`step-0/` または `step-1/` から開始）
2. AI エージェントで開く
3. `prompts.md` のプロンプトに従って次のステップに向けてビルド
4. 結果を次のステップディレクトリと比較

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

## インフラ設計：永続レイヤーとエフェメラルレイヤー

本ワークショップでは、Terraform コードを **永続（デフォルト）** と **エフェメラル** の 2 つのレイヤーに分割しています。

このアーキテクチャの主な目的は、学習中のクラウドコストを最小限に抑えつつ、何度でも構築・破棄できるクリーンで再現可能な実験環境を維持することです。

### 永続レイヤー

**主なリソース：** VPC（ネットワークインフラ）、ECR（コンテナレジストリ）、IAM ロール、セキュリティグループなど。

**特徴：** 一度作成するとほとんど変更されず、維持コストはほぼ発生しません。ワークショップ期間中を通じて保持する「基盤」として機能します。

### エフェメラルレイヤー

**主なリソース：** ECS（Fargate コンテナ実行環境）、ALB（ロードバランサー）、RDS（`db.t4g.micro` PostgreSQL）。

**特徴：** 実行中に時間単位で継続的に課金されるリソースをこのレイヤーに集約しています。作業中にのみ `terraform apply` を行い、作業終了時にこのレイヤーを `terraform destroy` することで、アイドルコストを大幅に削減できます。

### なぜデータベース（RDS）も使い捨てなのか？

本番環境では通常、データを保護するためにデータベースは永続レイヤーに配置されます。しかし、本ワークショップでは意図的にデータベースをエフェメラルレイヤーに含めています。

- **徹底的なコスト管理：** 非常にコスト効率の良い `db.t4g.micro` インスタンスを使用していますが、24 時間 365 日稼働させると課金が発生します。コンピュートリソースと一緒にグループ化することで、消し忘れを防ぎ、予期しない請求を回避できます。
- **クリーンな状態からの再開：** AI エージェントの開発では、プロンプトやロジックの調整に伴い、スキーマ変更やテストデータの再作成が頻繁に必要になります。環境全体を破棄・再作成することで、残留データやスキーマの不整合によるバグを回避し、常に IaC（Infrastructure as Code）で定義されたクリーンな状態から開発を再開できます。

> **注意：** エフェメラルレイヤーを破棄すると、DB 内のすべてのデータが完全に削除されます。これは「使い捨て環境」のコンセプトを採用した、本ワークショップの意図的な設計です。

## ライセンス

[MIT](LICENSE)
