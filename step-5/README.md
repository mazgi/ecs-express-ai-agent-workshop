# Step 5 — Next.js + NestJS with Auth + Items CRUD on ECS Express Mode

Next.js frontend and a NestJS backend with email/password authentication (JWT), user-scoped Items CRUD (PostgreSQL + Prisma), deployed to AWS ECS Express Mode.

## Services

| Service | Technology | Port |
|---------|-----------|------|
| backend | NestJS 11 + PostgreSQL 17 + Prisma + JWT Auth | 4000 |
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

## Backend API

- `POST /auth/signup` — Register with email/password (returns JWT tokens)
- `POST /auth/signin` — Sign in with email/password
- `POST /auth/refresh` — Refresh access token
- `GET /auth/me` — Get current user (requires JWT)
- `DELETE /auth/account` — Delete account (requires JWT)
- `POST /items` — Create item (requires JWT)
- `GET /items` — List user's items (requires JWT)
- `DELETE /items/:id` — Delete item (requires JWT, ownership check)

## Project Structure

```
.
├── compose.yaml
├── backend/               # NestJS API (auth + items)
│   └── prisma/            # Prisma schema (User + Item models)
├── web/
│   ├── app/               # Next.js App Router
│   └── e2e-tests/         # Playwright E2E tests
├── iac/                   # Terraform IaC (AWS)
├── Dockerfiles.d/
├── .github/               # GitHub Actions workflows + custom actions
└── docs/
```

---

[Prev: step-4 — Next.js + NestJS with Items CRUD](../step-4/README.md) | [Next: step-final — Full-Stack App](../step-final/README.md)
