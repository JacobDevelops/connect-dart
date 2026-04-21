<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# test

## Purpose
Unit and integration test suite for the `connectrpc` package. Covers abort signals, exceptions, envelope encoding/decoding, fake transport, HTTP headers, HTTP/2 transport, and protocol-level behavior. Also contains conformance test wiring and protoc plugin golden tests.

## Key Files

| File | Description |
|------|-------------|
| `abort_test.dart` | Tests for `AbortSignal` and cancellation behavior |
| `exception_test.dart` | Tests for `ConnectException` serialization and error code mapping |
| `envelope_test.dart` | Tests for binary envelope framing (5-byte header + payload) |
| `fake_test.dart` | Tests for the `FakeTransport` testing utility |
| `headers_test.dart` | Tests for `Headers` manipulation and case-insensitivity |
| `http2_test.dart` | Integration tests for the HTTP/2 native transport |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `conformance/` | Conformance test configuration and runners (io + web) |
| `plugin/` | Protoc plugin golden file tests |
| `protocol/` | Protocol transport integration tests |
| `gen/` | Generated protobuf fixtures used by tests (do not edit) |

## For AI Agents

### Working In This Directory
- Run all tests: `dart test` from `packages/connect/`.
- Run a single file: `dart test test/envelope_test.dart`.
- Tests under `conformance/` require the external `connectconformance` binary; they are skipped locally without it.
- Golden files in `plugin/golden/` must match generated output exactly — run `dart test --update-goldens` to regenerate after intentional plugin changes.
- Files in `gen/` are protobuf-generated — never edit manually.
- `dart_test.yaml` in the package root controls test configuration (platforms, timeouts).

### Common Patterns
- Unit tests use the `test` package with `group`/`test`/`expect` — no mocking framework.
- `FakeTransport` (from `lib/test.dart`) is the standard way to test client code without a live server.
- Envelope tests verify the 5-byte framing: 1-byte flags + 4-byte big-endian length.

<!-- MANUAL: -->
