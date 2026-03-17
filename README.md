# hassos-apps Workflows

Reusable GitHub Actions workflows for all hassos-apps addons.

## Usage

### CI (in your addon repo `.github/workflows/ci.yaml`)

```yaml
jobs:
  ci:
    uses: hassos-apps/workflows/.github/workflows/app-ci.yaml@main
    with:
      addon: your-addon-slug
```

### Deploy (in your addon repo `.github/workflows/deploy.yaml`)

```yaml
jobs:
  deploy:
    uses: hassos-apps/workflows/.github/workflows/app-deploy.yaml@main
    with:
      addon: your-addon-slug
    secrets:
      DISPATCH_TOKEN: ${{ secrets.DISPATCH_TOKEN }}
```

## Workflows

| Workflow | Trigger | Description |
|---|---|---|
| `app-ci.yaml` | `workflow_call` | Lint + build test multi-arch |
| `app-deploy.yaml` | `workflow_call` | Build, push to ghcr.io, notify repository |
