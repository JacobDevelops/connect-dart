<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# packages

## Purpose
Dart workspace packages for the connect-dart monorepo. Contains three packages: the core Connect protocol library (`connectrpc`), the conformance test suite, and development utilities.

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `connect/` | Core `connectrpc` package — protocol implementations, transport, code generator (see `connect/AGENTS.md`) |
| `conformance/` | Conformance test runner validating Connect/gRPC/gRPC-Web spec compliance (see `conformance/AGENTS.md`) |
| `tools/` | Development tools: buf wrapper and license header injector (see `tools/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- Each subdirectory is an independent Dart package with its own `pubspec.yaml`.
- All packages share the workspace resolution declared in the root `pubspec.yaml`.
- `conformance` and `tools` set `publish_to: none`; only `connectrpc` is published to pub.dev.
- Inter-package dependencies use `path:` references within the workspace.

### Common Patterns
- Each package has a `mono_pkg.yaml` that declares CI tasks run by `mono_repo`.
- Buf configuration (`buf.gen.yaml`, `buf.gen.test.yaml`) lives in `packages/connect/` and controls protobuf code generation.

<!-- MANUAL: -->
