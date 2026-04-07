# template-containerized-oauth2-project

An example project for developing a Next.js, NestJS, and Prisma app on ECS Express Mode using the AI agent.

## Services

| Service | Technology | Port |
|---------|-----------|------|
| backend | NestJS 11 + PostgreSQL 17 | 4000 |
| web | Next.js 16 | 3000 |

## Prerequisites

- Docker Engine + Docker Compose (e.g. [Docker Desktop](https://www.docker.com/products/docker-desktop/), [Podman](https://podman.io/), [Colima](https://github.com/abiosoft/colima))

## Quick Start

```sh
cp .example.secrets.env .secrets.env   # then fill in secrets — see docs/local-development.md
docker compose up
```

| URL | Description |
|-----|-------------|
| http://localhost:4000 | backend API |
| http://localhost:4000/api | Swagger UI |
| http://localhost:3000 | Web |

See [Local Development](docs/local-development.md) for detailed setup instructions (OAuth provider configuration, E2E tests, etc.).

## Use This Template

After creating a repository from this template, follow these steps. Only step 1 is required — the rest are optional depending on your needs.

1. **Local development** — Copy `.example.secrets.env` → `.secrets.env`, fill in secrets, and run `docker compose up`. See [Local Development](docs/local-development.md).
2. **E2E tests on CI** — Add GitHub Actions secrets for JWT and OAuth2 providers. See [CI — Setup for E2E tests](docs/ci.md#for-e2e-tests-only).
3. **Cloud deployment via CI** — Set up OIDC authentication, configure GitHub Actions variables, and run IaC workflows. See [CI — Setup for cloud deployment](docs/ci.md#for-cloud-deployment-e2e-tests--production-builds--iac).
4. **Manual cloud deployment** — Deploy directly with Terraform. See [Cloud Deployment](docs/cloud-deployment.md).

## Cloud Deployment (Terraform)

See [docs/cloud-deployment-aws.md](docs/cloud-deployment-aws.md) for full details. See also [docs/secrets.md](docs/secrets.md) for Secrets Manager setup.

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

## Project Structure

```
.
├── compose.yaml
├── .example.secrets.env
├── backend/               # NestJS API
├── web/
│   ├── app/               # Next.js SPA
│   └── e2e-tests/         # Playwright E2E tests
├── iac/                   # Terraform IaC (AWS)
├── Dockerfiles.d/
├── .github/               # GitHub Actions workflows + custom actions
└── docs/
```

## Documentation

- [Local Development](docs/local-development.md) — environment setup, running the stack, E2E tests
- Cloud Deployment — [overview](docs/cloud-deployment.md) / [AWS](docs/cloud-deployment-aws.md)
- [CI / GitHub Actions](docs/ci.md) — workflows, required secrets and variables
- [Secrets Management](docs/secrets.md) — AWS Secrets Manager
- [OIDC Setup](docs/oidc-setup.md) — one-time cloud provider authentication setup
- [Git SHA Display](docs/git-sha-display.md) — per-platform build SHA injection
- [Environment Variables](.example.secrets.env) — backend config and secrets
- [GitHub Actions Variables](.example.env) — CI/CD and cloud deployment variables

---

[Prev: step-5 — Next.js + NestJS with Auth + Items CRUD](../step-5/README.md)
