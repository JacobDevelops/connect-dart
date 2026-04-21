<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src

## Purpose
All implementation code for the `connectrpc` package. Contains the shared core types, platform-specific transport wiring, and per-protocol subdirectories. Nothing here is intended for direct import by consumers — use the barrel files in `lib/` instead.

## Key Files

| File | Description |
|------|-------------|
| `abort.dart` | `AbortSignal` and `AbortController` for cancelling in-flight RPCs |
| `client.dart` | `Client` extension type wrapping `Transport`; provides `unary`, `server`, `client`, `bidi` convenience methods used by generated code |
| `code.dart` | `Code` enum — all Connect/gRPC status codes (ok, canceled, unknown, …) |
| `codec.dart` | `Codec` abstract interface for message encoding/decoding; `CodecName` constants |
| `compression.dart` | `Compression` abstraction for content-encoding; registry and negotiation logic |
| `exception.dart` | `ConnectException` — typed RPC errors with `Code`, message, and metadata |
| `fake.dart` | `FakeTransport` for unit testing clients; configurable request/response handlers |
| `fetch_bindings.dart` | Dart JS-interop bindings for the browser Fetch API |
| `gzip.dart` | Gzip `Compression` implementation using `dart:io` `GZipCodec` |
| `headers.dart` | `Headers` — case-insensitive HTTP header map with append semantics |
| `http.dart` | Shared HTTP utilities; `UnaryResponse`/`StreamResponse` lower-level types |
| `interceptor.dart` | `Interceptor` typedef, `AnyFn`, and `Request`/`Response` sealed class hierarchy |
| `io.dart` | Native-platform transport factory (uses HTTP/2 connection from `http2/`) |
| `protobuf.dart` | `ProtoCodec` and `JsonCodec` implementations using the `protobuf` package |
| `sentinel.dart` | Internal sentinel values (e.g. end-of-stream markers) |
| `spec.dart` | `Spec<I,O>` — service method descriptor used by generated clients and transports |
| `transport.dart` | `Transport` abstract interface + `CallOptions`; core abstraction between client and protocol |
| `version.dart` | Package version constant (kept in sync with `pubspec.yaml`) |
| `web.dart` | Browser-platform transport factory (uses Fetch API bindings) |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `connect/` | Connect protocol implementation (see `connect/AGENTS.md`) |
| `grpc/` | gRPC protocol implementation (see `grpc/AGENTS.md`) |
| `grpc_web/` | gRPC-Web protocol implementation (see `grpc_web/AGENTS.md`) |
| `http2/` | HTTP/2 connection management for native transport (see `http2/AGENTS.md`) |
| `protocol/` | Shared protocol abstractions: envelope framing, serialization, compression, sink (see `protocol/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- All files here are internal — public API is exposed through `lib/*.dart` barrel files only.
- `io.dart` imports `dart:io` and must not be imported in web builds; `web.dart` imports JS-interop and must not be imported in native builds.
- `fetch_bindings.dart` contains `@JS()` annotations for the Fetch API — only valid in web compilation.
- `transport.dart` defines the single most important abstraction: `Transport`. All protocol implementations satisfy this interface.
- `spec.dart` defines `Spec<I,O>` — the generated code depends on this type; changes are breaking.

### Common Patterns
- Platform split: `io.dart` vs `web.dart` both expose a transport factory; the correct one is selected by the barrel (`lib/io.dart` / `lib/web.dart`).
- Error handling: all RPC errors are `ConnectException`; use `Code` values, not raw integers.
- Interceptors wrap `AnyFn` (a function from `Request` → `Future<Response>`); they are composable and applied last-to-first.

## Dependencies

### Internal
- `connect/`, `grpc/`, `grpc_web/` — protocol implementations used by `io.dart` and `web.dart`
- `protocol/` — shared envelope, serialization, compression utilities

### External
- `protobuf` — used in `protobuf.dart`
- `http2` — used in `io.dart` via `http2/`
- `fixnum` — used in protobuf codec

<!-- MANUAL: -->
