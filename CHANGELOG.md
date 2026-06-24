# Changelog

All notable changes to [aaron-howard/ci-templates](https://github.com/aaron-howard/ci-templates) are documented here.

## [1.0.0] - 2026-06-24

### Added

- Reusable `semgrep.yml`, `ci.yml`, and `e2e.yml` workflows (`workflow_call` only)
- Shared Semgrep baseline rules in `rules/security-baseline.yml` (secrets, fetch timeouts)
- Semgrep workflow checks out `ci-templates/rules` during app repo scans
- README with visibility rules, usage examples, and pinning guidance

### Notes

- App repos keep thin wrappers in `.github/workflows/` pointing at `@v1.0.0`
- Stack-specific Semgrep rules stay in each app under `config/semgrep/rules/`

[1.0.0]: https://github.com/aaron-howard/ci-templates/releases/tag/v1.0.0
