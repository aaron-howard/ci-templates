# ci-templates

Reusable GitHub Actions workflows for projects under [aaron-howard](https://github.com/aaron-howard).

This repository contains **workflow definitions only** — it is not an application. Workflows run against the **calling repository** when invoked with `workflow_call`.

## Repository visibility

| Caller repo | `ci-templates` must be |
|-------------|------------------------|
| **Public** (e.g. `profile-page`) | **Public** |
| Private | Private or public, with Actions access enabled |

Public repos **cannot** call reusable workflows in a private repo — GitHub returns *workflow was not found*.

If you keep this repo **private**, enable reusable workflow access:

**Settings → Actions → General → Access** → *Accessible from repositories owned by the user `aaron-howard`*.

Only **private** caller repos can use a private `ci-templates` repo.

## Workflows

| File | Purpose |
|------|---------|
| `semgrep.yml` | SAST scan (Semgrep + SARIF upload) |
| `ci.yml` | Lint, typecheck, test coverage, build |
| `e2e.yml` | Playwright E2E (`npm run test:e2e`) |

## Usage in an app repo

Example `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  semgrep:
    uses: aaron-howard/ci-templates/.github/workflows/semgrep.yml@main
    permissions:
      contents: read
      security-events: write
      actions: read

  ci:
    uses: aaron-howard/ci-templates/.github/workflows/ci.yml@main
    permissions:
      contents: read
```

Optional E2E (post-merge or manual):

```yaml
jobs:
  e2e:
    uses: aaron-howard/ci-templates/.github/workflows/e2e.yml@main
    permissions:
      contents: read
```

## Semgrep custom rules

Keep app-specific rules in each project at `config/semgrep/rules/`. The shared workflow scans that path when present.

## Pinning versions

`@main` tracks the latest templates. For stability, pin to a commit SHA or tag:

```yaml
uses: aaron-howard/ci-templates/.github/workflows/semgrep.yml@abc1234
```
