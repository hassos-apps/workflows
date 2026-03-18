# HassOS Apps — Shared Workflows

> Reusable GitHub Actions workflows for all [HassOS Apps](https://github.com/hassos-apps).

## Usage

### CI (in your app repo `.github/workflows/ci.yaml`)

```yaml
jobs:
  ci:
    uses: hassos-apps/workflows/.github/workflows/app-ci.yaml@main
    with:
      addon: your-app-slug
```

### Deploy (in your app repo `.github/workflows/deploy.yaml`)

```yaml
jobs:
  deploy:
    uses: hassos-apps/workflows/.github/workflows/app-deploy.yaml@main
    with:
      addon: your-app-slug
    secrets:
      DISPATCH_TOKEN: ${{ secrets.DISPATCH_TOKEN }}
```

> **Note:** The `addon` parameter name is kept for backward compatibility with the workflow interface.

## Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `app-ci.yaml` | `workflow_call` | Lint (yamllint, hadolint, shellcheck) + Docker build test multi-arch |
| `app-deploy.yaml` | `workflow_call` | Build, push to ghcr.io, create multi-arch manifest, notify repository |

## Pipeline Flow

```
app push/release
  → app-ci.yaml (lint + build)
  → app-deploy.yaml (build + push to ghcr.io)
    → multi-arch manifest
      → repository_dispatch → app store auto-update
```

---

> Part of **[HassOS Apps](https://github.com/hassos-apps)** — a curated ecosystem of purpose-built Home Assistant apps, crafted with structure, clarity and long-term reliability.
