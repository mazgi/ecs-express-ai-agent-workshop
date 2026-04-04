# Step 4 — Next.js + NestJS with Items CRUD on ECS Express Mode

Next.js frontend and a NestJS backend with health check (Git SHA) and Items CRUD (PostgreSQL + Prisma), deployed to AWS ECS Express Mode.

## Services

| Service | Technology | Port |
|---------|-----------|------|
| backend | NestJS 11 + PostgreSQL 17 + Prisma | 4000 |
| web | Next.js 16 | 3000 |

## Prerequisites

- Docker Engine + Docker Compose (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Colima](https://github.com/abiosoft/colima))

## Quick Start

```sh
cp .example.secrets.env .secrets.env
docker compose up
```

| URL | Description |
|-----|-------------|
| http://localhost:4000/health | Backend health check |
| http://localhost:4000/api | Swagger UI |
| http://localhost:3000 | Web |

## Run E2E Tests

```sh
docker compose --profile=e2e-tests run --rm web-e2e-tests
```

## Project Structure

```
.
├── compose.yaml
├── backend/               # NestJS API (health check + items CRUD)
│   └── prisma/            # Prisma schema (Item model)
├── web/
│   ├── app/               # Next.js App Router
│   └── e2e-tests/         # Playwright E2E tests
├── iac/                   # Terraform IaC (AWS)
├── Dockerfiles.d/
├── .github/               # GitHub Actions workflows + custom actions
└── docs/
```
