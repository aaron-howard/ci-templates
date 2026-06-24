# Shared Semgrep baseline rules

Loaded by the `ci-templates` Semgrep workflow (second checkout) on every app repo scan.

| File | Rules |
|------|-------|
| `security-baseline.yml` | Hardcoded secrets, fetch timeouts in server code |

App repos add stack-specific rules under `config/semgrep/rules/` (e.g. SvelteKit architecture).
