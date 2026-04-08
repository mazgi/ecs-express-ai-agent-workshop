# Step 1 — 空の Next.js アプリ

出発点：Playwright E2E テスト付きの空の Next.js App Router プロジェクトです。

## アーキテクチャ

```mermaid
graph LR
    subgraph Docker Compose
        Web["Web<br/>Next.js :3000"]
        E2E["E2E Tests<br/>Playwright"]
    end

    Browser["ブラウザ"] --> Web
    E2E -.->|テスト| Web
```

## 前提条件

- Docker Engine + Docker Compose（例: [Docker Desktop](https://www.docker.com/products/docker-desktop/)、[Podman](https://podman.io/)、[Colima](https://github.com/abiosoft/colima)）

## クイックスタート

```sh
docker compose up
```

http://localhost:3000 を開くと、デフォルトの Next.js ページが表示されます。

## E2E テストの実行

```sh
docker compose --profile=e2e-tests run --rm web-e2e-tests
```

## プロジェクト構成

```
.
├── compose.yaml
├── Dockerfiles.d/
│   ├── web/               # Next.js 開発用 Dockerfile
│   └── web-e2e-tests/     # Playwright 用 Dockerfile
└── web/
    ├── app/               # Next.js App Router
    └── e2e-tests/         # Playwright E2E テスト
```

## AI エージェントによる実装

次のステップ（step-2）に進むために、AI エージェント（[Claude Code](https://claude.ai/claude-code)、[Cursor](https://www.cursor.com/)、[GitHub Copilot](https://github.com/features/copilot)、[ChatGPT](https://chatgpt.com/) など）にコードを生成させることができます。

このディレクトリの [prompts.md](prompts.md) の内容をコピーして AI エージェントに渡してください。正しく実行されれば、手動の作業なしで step-2 と同等の環境が構築されます。

---

[前へ: step-0 — ゼロからスタート](../step-0/README.ja.md) | [次へ: step-2 — ECS Express Mode 上の Next.js](../step-2/README.ja.md)
