<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# tools

## Purpose
Internal development utilities for the connect-dart monorepo. Provides two executables: a `buf` wrapper that runs the Buf CLI for protobuf code generation, and a `license_header` tool that injects/validates Apache 2.0 license headers in source files. Not published to pub.dev.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Package manifest; version 0.1.0, `publish_to: none`, declares `buf` and `license_header` executables |
| `mono_pkg.yaml` | CI task configuration |
| `bin/buf.dart` | Wrapper that invokes the `buf` CLI for protobuf generation tasks |
| `bin/license_header.dart` | Scans and injects Apache 2.0 license headers into Dart source files |

## For AI Agents

### Working In This Directory
- Both executables are dev-only; they are consumed as dev dependencies by `connect` and `conformance`.
- Run via `dart run tools:buf` or `dart run tools:license_header` from the workspace root.
- The `buf` wrapper delegates to the external `buf` CLI binary (must be installed separately).
- `license_header` is run in CI to enforce copyright headers — run it before committing new `.dart` files.

### Testing Requirements
- No formal test suite; correctness is validated by CI lint and format checks.

### Common Patterns
- Executables use only the `path` package (no heavy dependencies).
- Follow the same Apache 2.0 header pattern as all other Dart files in the repo.

## Dependencies

### External
- `path: ^1.9.1` — Path manipulation utilities

<!-- MANUAL: -->
