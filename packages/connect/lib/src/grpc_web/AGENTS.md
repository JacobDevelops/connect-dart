<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src/grpc_web

## Purpose
Implementation of the gRPC-Web protocol. A browser-compatible variant of gRPC that works over standard HTTP/1.1 or HTTP/2 without requiring HTTP/2 trailers. Encodes trailers inside the response body using a special frame type. Used for web-platform gRPC calls.

## Key Files

| File | Description |
|------|-------------|
| `protocol.dart` | `GrpcWebProtocol` class; top-level protocol object |
| `transport.dart` | `GrpcWebTransport` — implements `Transport` using gRPC-Web over Fetch API |
| `request_header.dart` | Builds gRPC-Web request headers (`Content-Type: application/grpc-web+proto`) |
| `response.dart` | Parses gRPC-Web responses; demultiplexes data frames and trailer frames from the body stream |
| `trailer.dart` | Decodes the gRPC-Web trailer frame (flag byte `0x80`) embedded in the response body |

## For AI Agents

### Working In This Directory
- Implements the [gRPC-Web protocol spec](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md).
- gRPC-Web encodes trailers as a body frame with flag `0x80` (vs `0x00` for data) — not as HTTP trailers.
- Uses the Fetch API (via `src/fetch_bindings.dart`) rather than `dart:io` HTTP — web-only.
- `Content-Type` is `application/grpc-web+proto` (or `+json`).
- This transport works in browsers where native gRPC (HTTP/2 with trailers) is not available.
- Do not import `dart:io` here; this code runs in browser context only.

### Common Patterns
- Response body is a readable stream parsed frame-by-frame: data frames yield messages, trailer frames close the RPC and carry gRPC status.
- Status error detection follows the same `grpc-status` trailer logic as `src/grpc/`.

## Dependencies

### Internal
- `src/protocol/` — envelope framing, serialization
- `src/grpc/headers.dart`, `src/grpc/trailer_error.dart` — reuse gRPC header names and error conversion
- `src/fetch_bindings.dart` — Fetch API JS interop
- `src/code.dart`, `src/exception.dart`, `src/headers.dart`

<!-- MANUAL: -->
