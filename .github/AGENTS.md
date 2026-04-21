<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# .github

## Purpose
GitHub-specific configuration: CI/CD workflows, issue templates, contribution guidelines, release procedures, and dependency automation.

## Key Files

| File | Description |
|------|-------------|
| `CONTRIBUTING.md` | Step-by-step guide for building, testing, and submitting contributions |
| `CODE_OF_CONDUCT.md` | Community standards and enforcement |
| `RELEASING.md` | Release procedure and checklist |
| `dependabot.yml` | Automated dependency update configuration |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `workflows/` | GitHub Actions CI pipelines (see `workflows/AGENTS.md`) |
| `ISSUE_TEMPLATE/` | Structured bug report and feature request templates |

## For AI Agents

### Working In This Directory
- `CONTRIBUTING.md` contains the authoritative guide for local dev setup — read it before proposing build or test changes.
- Workflow YAML files must be validated against the GitHub Actions schema before committing.
- Do not modify `dependabot.yml` without understanding the current update cadence.

<!-- MANUAL: -->
