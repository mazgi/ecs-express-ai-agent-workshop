# Step 0 — Starting from Scratch

Empty directory. Use the prompts to create a Next.js project with Docker Compose and Playwright E2E tests.

## Prerequisites

- Docker Engine + Docker Compose (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Colima](https://github.com/abiosoft/colima))
- An AI coding agent (e.g. [Claude Code](https://claude.ai/claude-code))

## Get Started

Copy the contents of [prompts.md](prompts.md) in this directory and provide them to your AI agent (such as [Claude Code](https://claude.ai/claude-code), [Cursor](https://www.cursor.com/), [GitHub Copilot](https://github.com/features/copilot), or [ChatGPT](https://chatgpt.com/)). If executed correctly, you will have an environment equivalent to step-1 without manual intervention.

## Expected Output After Completion

After completing the prompts, you should have a working Next.js project equivalent to step-1:

- `docker compose up` starts the Next.js dev server
- **http://localhost:3000** — Default Next.js "Create Next App" landing page
- `docker compose --profile=e2e-tests run --rm web-e2e-tests` — Playwright E2E tests pass

---

[Next: step-1 — Empty Next.js App](../step-1/README.md)
