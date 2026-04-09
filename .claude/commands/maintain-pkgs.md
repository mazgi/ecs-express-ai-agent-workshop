Maintain and update packages in the current step directory.

For each service that has a `package.json` (e.g., `backend`, `web/app`, `web/e2e-tests`):

1. Run `npm-check-updates --upgrade` to update package.json to latest versions
2. Run `sort-package-json` to sort package.json keys
3. Run `pnpm install` to install updated packages
4. Run `pnpm audit --fix` to fix known vulnerabilities
5. Run `pnpm install` again to ensure lockfile is consistent

IMPORTANT: All commands must be run via Docker Compose since Node.js is not installed on the host. Use the appropriate service from compose.yaml (e.g., `docker compose exec backend sh -c "..."` or `docker compose run --rm`).

If compose services are not running, start them first with `docker compose up -d`.

IMPORTANT: Use `-e CI=true` and `--no-frozen-lockfile` flags when running `pnpm install` via `docker compose run` to avoid TTY prompts and frozen-lockfile errors.

After updating each step, run E2E tests to verify the project still works:
1. Start services: `docker compose up -d` (wait for healthy)
2. Run E2E tests: `docker compose --profile=e2e-tests run --rm web-e2e-tests`
3. Stop services: `docker compose --profile=e2e-tests down`

Process each step sequentially (update packages, then run E2E tests) before moving to the next step.

Report a summary of what was updated (major version bumps, security fixes, etc.) and E2E test results for each step.
