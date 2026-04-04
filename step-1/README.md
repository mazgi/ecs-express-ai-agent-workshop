# Step 1 — Empty Next.js App

Starting point: an empty Next.js App Router project with Playwright E2E tests.

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
