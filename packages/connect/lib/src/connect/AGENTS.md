<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src/connect

## Purpose
Implementation of the Connect protocol. Handles request/response framing, header construction, error encoding, trailer parsing, and the HTTP transport for Connect-specific wire format. Supports both POST (streaming and unary) and GET (idempotent unary) requests.

## Key Files

| File | Description |
|------|-------------|
| `protocol.dart` | `ConnectProtocol` class; top-level protocol object used by the transport |
| `transport.dart` | `ConnectTransport` — implements `Transport` using the Connect protocol |
| `header.dart` | Connect-specific HTTP header names and construction logic |
| `response.dart` | Response parsing: extracts message and trailers from Connect HTTP responses |
| `trailer.dart` | Parses Connect trailers (sent as JSON in the response body end-stream) |
| `end_stream.dart` | Parses the Connect end-stream message that carries trailers and errors |
| `error_json.dart` | Serializes/deserializes `ConnectException` to/from the Connect JSON error format |
| `http_status.dart` | Maps HTTP status codes to Connect `Code` values and vice versa |
| `get.dart` | Implements the Connect GET request path for idempotent unary calls |
| `stable_codec.dart` | Codec wrapper that ensures stable (deterministic) encoding for GET request URL params |
| `version.dart` | Connect-Connect-Protocol version header value constant |

## For AI Agents

### Working In This Directory
- This directory implements the [Connect protocol spec](https://connectrpc.com/docs/protocol).
- The Connect protocol uses `Content-Type: application/connect+proto` (or `+json`) and trailers encoded in the response body.
- GET requests (via `get.dart`) are only valid for idempotent methods and encode the request message as a URL query parameter.
- `error_json.dart` handles the Connect error format — a JSON object with `code`, `message`, and `details` fields.
- HTTP status ↔ Code mapping in `http_status.dart` differs from gRPC's mapping; keep them separate.
- Changes here may require updating the conformance test suite if protocol behavior changes.

### Common Patterns
- Transport reads `Spec.idempotency` to decide between GET and POST.
- End-stream messages use the flag byte `0x02` in the 5-byte envelope header to distinguish them from data messages.

## Dependencies

### Internal
- `src/protocol/` — envelope framing, compression, serialization
- `src/code.dart`, `src/exception.dart`, `src/headers.dart`, `src/transport.dart`

<!-- MANUAL: -->
