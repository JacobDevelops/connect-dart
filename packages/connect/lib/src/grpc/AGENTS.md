<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src/grpc

## Purpose
Implementation of the gRPC protocol over HTTP/2. Handles request header construction, response parsing, trailer extraction, gRPC status code mapping, and the native HTTP/2 transport. Used for native-platform gRPC calls (Android, iOS, Linux, macOS, Windows).

## Key Files

| File | Description |
|------|-------------|
| `protocol.dart` | `GrpcProtocol` class; top-level protocol object |
| `transport.dart` | `GrpcTransport` — implements `Transport` using gRPC over HTTP/2 |
| `headers.dart` | gRPC-specific HTTP header names (`grpc-status`, `grpc-message`, `grpc-encoding`, etc.) |
| `request_header.dart` | Builds gRPC request headers including content-type, encoding, and timeout |
| `response.dart` | Parses gRPC HTTP/2 responses; extracts messages and trailing metadata |
| `trailer.dart` | Reads gRPC trailers from HTTP/2 trailer frames |
| `trailer_error.dart` | Converts `grpc-status` / `grpc-message` trailer values into `ConnectException` |
| `status.dart` | Maps gRPC `Status` proto to `ConnectException` and `Code` |
| `http_status.dart` | Maps HTTP status codes to gRPC `Code` values for error cases |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `gen/` | Generated protobuf types for the gRPC Status proto (do not edit) |
| `proto/` | Source `status.proto` used for the generated status types |

## For AI Agents

### Working In This Directory
- Implements the [gRPC over HTTP/2 protocol](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md).
- gRPC uses HTTP/2 trailers (actual HTTP/2 HEADERS frames after DATA frames) — distinct from Connect's in-body trailers.
- `Content-Type` is `application/grpc+proto` (or `+json`).
- gRPC status codes map to `Code` enum but via `status.dart` / `trailer_error.dart` — separate from Connect's HTTP status mapping.
- Files in `gen/` are auto-generated from `proto/status.proto` — never edit manually.
- This transport is for native platforms only; web uses `grpc_web/transport.dart` instead.

### Common Patterns
- gRPC timeout is sent as `grpc-timeout` header in a compact format (`100m` = 100 milliseconds).
- Error detection requires reading `grpc-status` from trailers; a `200 OK` HTTP response can still be a gRPC error.

## Dependencies

### Internal
- `src/protocol/` — envelope framing, compression, serialization
- `src/http2/` — HTTP/2 connection management
- `src/code.dart`, `src/exception.dart`, `src/headers.dart`

<!-- MANUAL: -->
