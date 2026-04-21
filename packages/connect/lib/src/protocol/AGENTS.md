<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# src/protocol

## Purpose
Shared protocol-level utilities used by all three protocol implementations (Connect, gRPC, gRPC-Web). Provides the foundational building blocks: binary envelope framing, message serialization, compression negotiation, streaming sinks, and the base transport helper.

## Key Files

| File | Description |
|------|-------------|
| `protocol.dart` | `Protocol` abstract interface; implemented by `ConnectProtocol`, `GrpcProtocol`, `GrpcWebProtocol` |
| `envelope.dart` | Binary envelope encoding/decoding: 5-byte header (1-byte flags + 4-byte big-endian length) wrapping each message |
| `serialization.dart` | `Serialization` — ties together a `Codec` and a `Compression` to serialize/deserialize messages for the wire |
| `compression.dart` | `Compression` registry and negotiation; selects encoding based on request/response headers |
| `transport.dart` | Base transport helpers shared across protocol implementations |
| `sink.dart` | `MessageSink` — a `StreamSink` abstraction for writing outbound messages into an HTTP request body |

## For AI Agents

### Working In This Directory
- `envelope.dart` is critical — all three protocols use the same 5-byte framing. Changes here affect every protocol.
- The flag byte in the envelope header is protocol-specific: `0x01` = compressed, `0x02` = end-stream (Connect only), `0x80` = trailer frame (gRPC-Web only).
- `serialization.dart` composes `Codec` + `Compression` — adding a new codec (e.g. JSON) or compression algorithm (e.g. Brotli) requires implementing the respective abstract class in `src/codec.dart` / `src/compression.dart`.
- Do not add protocol-specific logic here; keep it generic and reusable.

### Common Patterns
- `splitEnvelope` (in `envelope.dart`) splits a byte buffer into (flags, payload) pairs — it was improved in PR #31.
- Compression negotiation reads the `Accept-Encoding` and `Content-Encoding` headers.

## Dependencies

### Internal
- `src/codec.dart` — `Codec` interface
- `src/compression.dart` — `Compression` interface
- `src/headers.dart`, `src/exception.dart`

<!-- MANUAL: -->
