# Publish to Cloudflare Workers Action

Reusable GitHub Action to install deps, build, and deploy Cloudflare Workers using Wrangler.

## Inputs

- `node-version` (default: `20`)
- `wrangler-version` (default: `latest`)
- `working-directory` (default: `.`)
- `install-command` (default: `npm ci`)
- `build-command` (default: `npm run build --if-present`)
- `deploy-command` (default: `deploy`)
- `cloudflare-api-token` (**required**)
- `cloudflare-account-id` (**required**)
- `checkout` (default: `true`)

## Usage

```yaml
name: Publish to Cloudflare Workers

on:
  push:
    branches: [ main ]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy Workers
        uses: your-org/cf-workers-publish-action@v1
        with:
          cloudflare-api-token: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          cloudflare-account-id: ${{ secrets.CF_ACCOUNT_ID }}
```

## Custom deploy args

Example: deploy with env or specific config.

```yaml
- uses: your-org/cf-workers-publish-action@v1
  with:
    cloudflare-api-token: ${{ secrets.CLOUDFLARE_API_TOKEN }}
    cloudflare-account-id: ${{ secrets.CF_ACCOUNT_ID }}
    deploy-command: "deploy --env production"
```

## Notes

- This action uses `npx wrangler@<version>`.
- Make sure your repository contains a valid `wrangler.toml`.
