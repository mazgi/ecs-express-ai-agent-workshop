# ECS Express AI Agent Workshop

A hands-on workshop for developing a Next.js, NestJS, and Prisma app on AWS ECS Express Mode using the AI agent (Claude Code).

Each `step-*` directory is a self-contained project snapshot. Use the `prompts.md` in each step to guide the AI agent to evolve the project to the next step.

## Steps

### [step-0](step-0/) — Starting from Scratch

Empty directory. Follow the prompts to create everything from scratch.

**Next:** Follow [step-0/prompts.md](step-0/prompts.md) to create a Next.js project with Docker Compose and Playwright E2E tests.

### [step-1](step-1/) — Empty Next.js App

Starting point: an empty Next.js App Router project with Docker Compose for local development and Playwright E2E tests. No backend, no infrastructure.

**What you have:**
- Next.js 16 App Router (TypeScript)
- Docker Compose (`web` + `web-e2e-tests` services)
- Playwright smoke test

**Next:** Follow [step-1/prompts.md](step-1/prompts.md) to add AWS infrastructure (Terraform), CI/CD (GitHub Actions), and production Docker builds.

### [step-2](step-2/) — Next.js on ECS Express Mode

The Next.js app with Terraform IaC for deploying to AWS ECS Express Mode, plus CI/CD via GitHub Actions. Frontend only — no backend or database.

**What's added from step-1:**
- Terraform IaC (persistent: VPC, ECR, IAM; ephemeral: ECS Express Gateway)
- GitHub Actions workflows (E2E tests, image build/push, IaC plan/apply)
- Production Dockerfile for web
- OIDC setup and cloud deployment documentation

**Next:** Follow [step-2/prompts.md](step-2/prompts.md) to add a minimal NestJS backend with health check and Git SHA display.

### [step-3](step-3/) — Next.js + NestJS (health check) on ECS Express Mode

Next.js frontend and a minimal NestJS backend (health check with GIT_SHA and Swagger), both deployed to AWS ECS Express Mode.

**What's added from step-2:**
- NestJS 11 backend with `GET /health` endpoint (returns Git SHA)
- Swagger UI at `/api` (non-production)
- Backend Dockerfile, ECR repository, security group, and ECS Express Gateway service
- Web app fetches and displays backend Git SHA
- Backend service in Docker Compose

**Next:** Follow [step-3/prompts.md](step-3/prompts.md) to add PostgreSQL, Prisma ORM, and Items CRUD.

### [step-4](step-4/) — Next.js + NestJS with Items CRUD on ECS Express Mode

Next.js frontend and a NestJS backend with health check and Items CRUD (PostgreSQL + Prisma), deployed to AWS ECS Express Mode.

**What's added from step-3:**
- PostgreSQL 17 database
- Prisma ORM with Item model
- Items CRUD API (`POST /items`, `GET /items`, `DELETE /items/:id`) — no authentication
- Web app with items list, create form, and delete buttons
- Items E2E test
- RDS PostgreSQL, private subnets, and NAT gateway in Terraform
- Secrets Manager for DATABASE_URL

**Next:** Follow [step-4/prompts.md](step-4/prompts.md) to add email/password authentication (JWT) with user-scoped items.

### [step-5](step-5/) — Next.js + NestJS with Auth + Items CRUD on ECS Express Mode

Next.js frontend and a NestJS backend with email/password authentication (JWT) and user-scoped Items CRUD (PostgreSQL + Prisma), deployed to AWS ECS Express Mode.

**What's added from step-4:**
- Email/password sign-up and sign-in with JWT tokens
- User model in Prisma (user-scoped items)
- JWT auth guard on items endpoints (ownership check)
- Sign-in and sign-up pages with AuthContext
- Dashboard (user profile) and authenticated items page
- Navigation header (Dashboard, Items, Sign out)
- Secrets Manager for JWT secrets and DATABASE_URL in Terraform

**Next:** Follow [step-5/prompts.md](step-5/prompts.md) to add OAuth2, email verification, TOTP MFA, and internationalization.

### [step-final](step-final/) — Full-Stack App

The complete application with all features — OAuth2 authentication, email verification, TOTP MFA, internationalization, and more.

**What's added from step-5:**
- OAuth2 authentication (Apple, Discord, GitHub, Google, X/Twitter)
- Email verification and password reset flows
- TOTP MFA (two-factor authentication) with recovery codes
- SMTP email integration (Mailpit for local dev)
- Internationalization (English + Japanese)
- Account linking/unlinking for OAuth providers
- Settings page (email, MFA, linked accounts, theme)
- Full E2E test suites for backend and web

## Prerequisites

- Docker Engine + Docker Compose (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Colima](https://github.com/abiosoft/colima))
- An AI coding agent (e.g. [Claude Code](https://claude.ai/claude-code))

## How to Use

1. Pick a step directory (start with `step-0/` or `step-1/`)
2. Open it in your AI agent
3. Follow the prompts in `prompts.md` to build toward the next step
4. Compare your result with the next step directory

## License

[MIT](LICENSE)
