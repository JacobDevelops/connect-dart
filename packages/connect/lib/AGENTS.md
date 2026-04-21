<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# lib

## Purpose
Public-facing library entry points for the `connectrpc` package. Each `.dart` file is a separate library barrel that exposes a specific slice of the API. Consumer code imports only the barrel that matches their platform and needs.

## Key Files

| File | Description |
|------|-------------|
| `connect.dart` | Core public API: `Transport`, `Client`, `Interceptor`, `Headers`, `ConnectException`, `Code`, `Spec`, `AbortSignal` — platform-agnostic |
| `io.dart` | Native-platform transport entry point (Android, iOS, Linux, macOS, Windows) — imports HTTP/2 and dart:io |
| `web.dart` | Browser-platform transport entry point — imports Fetch API bindings, no dart:io |
| `http2.dart` | Low-level HTTP/2 connection utilities, re-exported for advanced use |
| `protobuf.dart` | Protobuf codec integration — `ProtoCodec`, `JsonCodec` |
| `test.dart` | Testing utilities: `FakeTransport` for unit-testing clients without a real server |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `src/` | All implementation code; not intended for direct import (see `src/AGENTS.md`) |
| `protocol/` | Protocol-specific public re-exports (Connect, gRPC, gRPC-Web) |

## For AI Agents

### Working In This Directory
- **Never** import from `lib/src/` directly in consumer code — always go through the barrel files.
- `io.dart` and `web.dart` are mutually exclusive per compilation target; never import both in the same compilation unit.
- Adding a new public symbol requires exporting it from the appropriate barrel file.
- The split between `connect.dart` (platform-agnostic) and `io.dart`/`web.dart` (platform-specific) is intentional — keep it clean.

### Common Patterns
- Barrel files use `export 'src/foo.dart'` with no `show`/`hide` — the entire public surface of each src file is considered intentional.
- New platform-specific code goes in `src/io.dart` or `src/web.dart`, then exported from the matching barrel.

<!-- MANUAL: -->
