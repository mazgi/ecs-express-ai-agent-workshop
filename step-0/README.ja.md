# Step 0 — ゼロからスタート

空のディレクトリです。プロンプトを使って、Docker Compose と Playwright E2E テストを含む Next.js プロジェクトを作成します。

## 前提条件

- Docker Engine + Docker Compose（例: [Docker Desktop](https://www.docker.com/products/docker-desktop/)、[Podman](https://podman.io/)、[Colima](https://github.com/abiosoft/colima)）
- AI コーディングエージェント（例: [Claude Code](https://claude.ai/claude-code)）

## はじめに

このディレクトリの [prompts.md](prompts.md) の内容をコピーして AI エージェント（[Claude Code](https://claude.ai/claude-code)、[Cursor](https://www.cursor.com/)、[GitHub Copilot](https://github.com/features/copilot)、[ChatGPT](https://chatgpt.com/) など）に渡してください。正しく実行されれば、手動の作業なしで step-1 と同等の環境が構築されます。

## 完了後の期待される出力

プロンプトを完了すると、step-1 と同等のプロジェクトが構築されます：

- `docker compose up` で Next.js 開発サーバーが起動
- **http://localhost:3000** — デフォルトの Next.js「Create Next App」ランディングページ
- `docker compose --profile=e2e-tests run --rm web-e2e-tests` — Playwright E2E テストがパス

---

[次へ: step-1 — 空の Next.js アプリ](../step-1/README.ja.md)
