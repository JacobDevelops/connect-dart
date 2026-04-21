<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# workflows

## Purpose
GitHub Actions CI/CD pipeline definitions for connect-dart. Controls automated testing, analysis, formatting, and project management on every push and pull request.

## Key Files

| File | Description |
|------|-------------|
| `dart.yml` | Primary CI pipeline: installs Dart SDK, runs `dart analyze`, `dart format`, `dart test`, and conformance tests across all packages |
| `add-to-project.yaml` | Automatically adds new issues and PRs to the GitHub project board |
| `pr-title.yaml` | Validates that PR titles follow conventional commit format |

## For AI Agents

### Working In This Directory
- `dart.yml` is the authoritative definition of what "passing CI" means — match its commands exactly when testing locally.
- Workflow files use the `ubuntu-latest` runner; macOS/Windows jobs may be added for platform-specific testing.
- The conformance test job in `dart.yml` downloads the `connectconformance` binary — check this job when debugging conformance failures.
- Validate YAML syntax against the GitHub Actions schema before committing workflow changes.
- Secrets (API keys, tokens) are never stored in workflow files; they reference GitHub repository secrets.

### Common Patterns
- Dart version is pinned via the `dart-lang/setup-dart` action — update the version there, not in multiple places.
- Caching of the Dart pub cache is handled by the setup action.

<!-- MANUAL: -->
