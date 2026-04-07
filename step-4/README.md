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

## Cloud Deployment (Terraform)

See [docs/cloud-deployment-aws.md](docs/cloud-deployment-aws.md) for full details. Quick summary:

```sh
# 1. Configure variables
cp iac/aws/terraform.tfvars.example iac/aws/terraform.tfvars
cp iac/aws/ephemeral/terraform.tfvars.example iac/aws/ephemeral/terraform.tfvars

# 2. Deploy persistent infrastructure (VPC, ECR, IAM, Secrets Manager)
source .env
docker compose --profile=iac run --rm iac terraform -chdir=aws init \
  -backend-config="bucket=$AWS_TF_STATE_BUCKET" \
  -backend-config="region=$AWS_TF_STATE_REGION"
docker compose --profile=iac run --rm iac terraform -chdir=aws apply -var-file=terraform.tfvars

# 3. Build and push Docker images to ECR, then deploy ephemeral infrastructure (ECS Express Gateway, RDS)
docker compose --profile=iac run --rm iac terraform -chdir=aws/ephemeral init \
  -backend-config="bucket=$AWS_TF_STATE_BUCKET" \
  -backend-config="region=$AWS_TF_STATE_REGION"
docker compose --profile=iac run --rm iac terraform -chdir=aws/ephemeral apply -var-file=terraform.tfvars
```

## Implementation via AI Agent

To prepare for the next step (step-5), you can have an AI agent (such as [Claude Code](https://claude.ai/claude-code), [Cursor](https://www.cursor.com/), [GitHub Copilot](https://github.com/features/copilot), or [ChatGPT](https://chatgpt.com/)) generate the code for you.

Copy the contents of [prompts.md](prompts.md) in this directory and provide them to your AI agent. If executed correctly, you will have an environment equivalent to step-5 without manual intervention.

---

[Prev: step-3 — Next.js + NestJS (health check)](../step-3/README.md) | [Next: step-5 — Next.js + NestJS with Auth + Items CRUD](../step-5/README.md)
