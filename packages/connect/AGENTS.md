<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# connect (connectrpc package)

## Purpose
The core `connectrpc` package (v1.0.0). Implements the Connect, gRPC, and gRPC-Web protocols for Dart. Provides the public API for building RPC clients, the `Transport` abstraction, interceptors, and the `protoc-gen-connect-dart` protoc plugin for code generation. Published to pub.dev.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Package manifest; version 1.0.0, declares `protoc-gen-connect-dart` executable |
| `mono_pkg.yaml` | Mono-repo CI task configuration |
| `buf.gen.yaml` | Buf code generation config for the main library protos |
| `buf.gen.test.yaml` | Buf config for test fixture proto generation |
| `buf.gen.plugin.yaml` | Buf config for the protoc plugin descriptor |
| `dart_test.yaml` | Test runner configuration |
| `dartdoc_options.yaml` | API documentation options |
| `CHANGELOG.md` | Version history |
| `.pubignore` | Files excluded from pub.dev publish |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `lib/` | Public library entry points and all source (see `lib/AGENTS.md`) |
| `bin/` | `protoc-gen-connect-dart` plugin executable and generator logic (see `bin/AGENTS.md`) |
| `test/` | Unit tests and conformance test wiring (see `test/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- The package name on pub.dev is `connectrpc`; import as `package:connectrpc/connect.dart`.
- Never modify files in `lib/src/grpc/gen/`, `bin/src/gen/`, or `test/gen/` — all are protobuf-generated.
- Regenerate protos with `dart run tools:buf generate` from the workspace root (uses the `buf` tool wrapper in `packages/tools/bin/buf.dart`).
- The `protoc-gen-connect-dart` binary is registered as a Dart executable in `pubspec.yaml`; install it with `dart pub global activate connectrpc`.
- Platform support: android, ios, linux, macos, web, windows (declared in `pubspec.yaml`).

### Testing Requirements
- `dart test` from `packages/connect/` runs all unit tests.
- Conformance tests require `connectconformance` binary; see `.github/CONTRIBUTING.md`.
- `dart analyze` must produce zero diagnostics.
- Test files follow the `*_test.dart` naming convention.

### Common Patterns
- Public API split by platform: `lib/connect.dart` (core), `lib/io.dart` (native), `lib/web.dart` (browser), `lib/protobuf.dart` (codec), `lib/test.dart` (testing utilities).
- `Transport` is an abstract interface; concrete implementations live in `lib/src/*/transport.dart`.
- `Client` extension type wraps a `Transport` and provides `unary`, `server`, `client`, and `bidi` convenience methods used by generated code.
- Interceptors are functions `AnyFn → AnyFn`; applied last-to-first from the interceptors array.

## Dependencies

### Internal
- `packages/conformance` — dev dependency for running conformance tests
- `packages/tools` — dev dependency for buf/license utilities

### External
- `protobuf: >=3.1.0 <5.0.0` — Protobuf runtime
- `http2: ^2.3.0` — HTTP/2 transport for native platforms
- `fixnum: ^1.1.1` — 64-bit integers required by protobuf
- `path: ^1.9.0` — Path manipulation in the plugin

<!-- MANUAL: -->
