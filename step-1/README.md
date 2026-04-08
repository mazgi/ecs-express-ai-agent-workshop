# Step 1 — Empty Next.js App

Starting point: an empty Next.js App Router project with Playwright E2E tests.

## Architecture at Start

The following diagram shows what you **already have** when you begin this step — not the final goal. See [Expected Output After Completion](#expected-output-after-completion) for what you will build.

```mermaid
graph LR
    subgraph Docker Compose
        Web["Web<br/>Next.js :3000"]
        E2E["E2E Tests<br/>Playwright"]
    end

    Browser["Browser"] --> Web
    E2E -.->|tests| Web
```

## Prerequisites

- Docker Engine + Docker Compose (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Colima](https://github.com/abiosoft/colima))

## Quick Start

```sh
docker compose up
```

Open http://localhost:3000 to see the default Next.js page.

## Run E2E Tests

```sh
docker compose --profile=e2e-tests run --rm web-e2e-tests
```

## Project Structure

```
.
├── compose.yaml
├── Dockerfiles.d/
│   ├── web/               # Dockerfile for Next.js dev
│   └── web-e2e-tests/     # Dockerfile for Playwright
└── web/
    ├── app/               # Next.js App Router
    └── e2e-tests/         # Playwright E2E tests
```

## Implementation via AI Agent

To prepare for the next step (step-2), you can have an AI agent (such as [Claude Code](https://claude.ai/claude-code), [Cursor](https://www.cursor.com/), [GitHub Copilot](https://github.com/features/copilot), or [ChatGPT](https://chatgpt.com/)) generate the code for you.

Copy the contents of [prompts.md](prompts.md) in this directory and provide them to your AI agent. If executed correctly, you will have an environment equivalent to step-2 without manual intervention.

## Expected Output After Completion

After completing the prompts, you should have a project equivalent to step-2 with:

- Terraform IaC under `iac/` (persistent + ephemeral layers)
- GitHub Actions workflows under `.github/`
- A production Dockerfile for web (`Dockerfiles.d/web-build/`)
- Cloud deployment documentation under `docs/`
- Local development still works: `docker compose up` → http://localhost:3000

---

[Prev: step-0 — Starting from Scratch](../step-0/README.md) | [Next: step-2 — Next.js on ECS Express Mode](../step-2/README.md)
