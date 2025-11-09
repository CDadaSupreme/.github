# .github

Organization-level GitHub configuration and reusable workflows for the Kanovi platform.

## Reusable Workflows

### `preprod-reusable.yml`

A reusable workflow for hardened pre-production testing across all repositories.

**Usage:**

```yaml
name: Preprod Check
on:
  pull_request: { branches: [ main ] }
  workflow_dispatch: {}

jobs:
  preprod:
    uses: CDadaSupreme/.github/.github/workflows/preprod-reusable.yml@main
    with:
      repo_kind: 'api'  # or 'web', 'worker'
      strict_health: false
      node_version: '20'
    secrets: inherit
```

**Parameters:**

- `repo_kind` (required): Type of repository - `api`, `web`, or `worker`
- `strict_health` (optional): Enable strict health check enforcement (default: `false`)
- `node_version` (optional): Node.js version to use (default: `'20'`)

**Secrets:**

All secrets are optional and will be used if provided:
- `PREPROD_DATABASE_URL`
- `PREPROD_REDIS_URL`
- `PREPROD_JWT_SECRET`
- `PREPROD_SESSION_SECRET`
- `PREPROD_NEXT_PUBLIC_API_URL`

**Features:**

- Dynamic runner selection (Ubuntu for web, Windows for api/worker)
- Automatic `.env.preprod` generation
- PowerShell-based test execution
- Log artifact upload on all runs
- Cross-platform compatibility
