# Cloudflare Pages deployment

This project is a static site, so the deploy target is the repository root (`.`).

## GitHub setup

Add these repository secrets:

- `CLOUDFLARE_API_TOKEN`: Cloudflare API token with Pages deploy permission.
- `CLOUDFLARE_ACCOUNT_ID`: your Cloudflare account ID.

Add these repository variables:

- `CLOUDFLARE_PAGES_PROJECT_NAME`: the exact Cloudflare Pages project name.
- `CLOUDFLARE_DEPLOY_ON_PUSH`: set to `true` to deploy automatically on every push to `main`.

## Recommended rollout

1. Keep `CLOUDFLARE_DEPLOY_ON_PUSH` unset or set to `false` at first.
2. Run the `Deploy to Cloudflare Pages` workflow manually from GitHub Actions to verify credentials and project name.
3. If your Cloudflare Pages project is still using Cloudflare's own Git integration, disable its automatic production deploys before setting `CLOUDFLARE_DEPLOY_ON_PUSH=true`. This avoids double deployments from both Cloudflare and GitHub Actions.

## What this workflow does

- Manual deploy: always available through `workflow_dispatch`.
- Automatic deploy: runs on push to `main` only when `CLOUDFLARE_DEPLOY_ON_PUSH=true`.
- Uploads the repository root directly with `wrangler pages deploy .`.
