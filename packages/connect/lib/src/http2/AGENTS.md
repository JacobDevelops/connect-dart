<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src/http2

## Purpose
HTTP/2 connection management for native-platform transports. Wraps the `http2` Dart package to provide a managed connection pool with TLS support, used by the gRPC transport on Android, iOS, Linux, macOS, and Windows.

## Key Files

| File | Description |
|------|-------------|
| `http2.dart` | Public-facing HTTP/2 utilities; entry point for the http2 sub-system |
| `connection.dart` | `Http2Connection` — manages a single HTTP/2 client connection including TLS handshake and stream lifecycle |
| `errors.dart` | Maps HTTP/2 protocol errors (RST_STREAM, GOAWAY) to `ConnectException` |

## For AI Agents

### Working In This Directory
- This code is native-only (`dart:io` required); never imported on web platform.
- `connection.dart` handles TLS negotiation (ALPN `h2`) and multiplexed stream management.
- HTTP/2 streams map 1:1 to RPC calls; connection is reused across calls.
- RST_STREAM and GOAWAY frames are translated to appropriate `Code` values via `errors.dart`.
- The `http2` pub package (v2.3+) is the underlying dependency.

### Common Patterns
- Connection is established lazily on first call and kept alive for subsequent calls.
- TLS is required for most gRPC endpoints; insecure connections need explicit opt-in.

## Dependencies

### Internal
- `src/code.dart`, `src/exception.dart`

### External
- `http2: ^2.3.0` — HTTP/2 client implementation

<!-- MANUAL: -->
