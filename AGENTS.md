<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# connect-dart

## Purpose
Connect-Dart is a Dart implementation of the Connect, gRPC, and gRPC-Web RPC protocols using Protocol Buffers. It provides a slim, type-safe client library plus a `protoc-gen-connect-dart` code generator plugin that produces idiomatic Dart clients from `.proto` files. The library targets all 6 Dart/Flutter platforms: Android, iOS, Linux, macOS, Windows, and Web.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Workspace root; declares Dart SDK ≥3.6.0, registers the three workspace packages |
| `mono_repo.yaml` | Mono-repo metadata and CI task configuration |
| `analysis_options.yaml` | Dart analyzer/linter rules for all packages |
| `LICENSE` | Apache 2.0 license |
| `README.md` | Project overview, quick start links, and ecosystem references |
| `MAINTAINERS.md` | Current maintainers and contact info |
| `SECURITY.md` | Vulnerability reporting policy |
| `tool/ci.sh` | Manual CI helper script |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `packages/` | Monorepo workspace packages (see `packages/AGENTS.md`) |
| `example/` | Example Flutter and web applications (see `example/AGENTS.md`) |
| `.github/` | CI workflows, issue templates, contribution guides (see `.github/AGENTS.md`) |
| `tool/` | Root-level shell scripts for CI |

## For AI Agents

### Working In This Directory
- This is a **Dart monorepo** managed as a Dart workspace (`pubspec.yaml` workspace field).
- Use `dart pub get` from the repo root to resolve all workspace packages at once.
- Never edit files in `packages/connect/lib/src/grpc/gen/`, `packages/connect/bin/src/gen/`, or any `gen/` directory — these are protobuf-generated and must be regenerated via `buf`.
- The protoc plugin binary is `protoc-gen-connect-dart` (published via `packages/connect`).
- Version control uses **Jujutsu (jj)**, not git — use `jj` commands, never `git` directly.
- Conventional commits are required; branch prefixes: `feat/`, `fix/`, `chore/`, `refactor/`.

### Testing Requirements
- Run tests from the workspace root: `dart test packages/connect`
- Conformance tests require the external `connectconformance` binary (see `.github/CONTRIBUTING.md`).
- `dart analyze` must pass with zero errors before committing.
- `dart format --output=none --set-exit-if-changed .` must pass.

### Common Patterns
- Public API is exported via barrel files (`lib/connect.dart`, `lib/io.dart`, `lib/web.dart`, `lib/protobuf.dart`, `lib/web.dart`, `lib/test.dart`).
- Platform-specific code uses separate `io.dart` / `web.dart` entry points; never import both.
- All `.pb.dart`, `.connect.client.dart`, `.connect.spec.dart` files are generated — edit the upstream `.proto` instead.

## Dependencies

### External
- `protobuf: >=3.1.0 <5.0.0` — Dart Protocol Buffers runtime
- `http2: ^2.3.0` — HTTP/2 transport (native platforms)
- `fixnum: ^1.1.1` — 64-bit integer support for protobuf
- `path: ^1.9.0` — File path utilities
- `lints: ^4.0.0` — Dart recommended lint rules

<!-- MANUAL: -->
