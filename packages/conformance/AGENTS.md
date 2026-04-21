<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# conformance

## Purpose
Conformance test suite for connect-dart. Validates that the Connect, gRPC, and gRPC-Web protocol implementations correctly interoperate with the reference conformance server. Runs as both native I/O and browser-based web tests via the `connectconformance` harness. Not published to pub.dev.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Package manifest; version 0.3.0, `publish_to: none`, declares `pipe` executable |
| `mono_pkg.yaml` | CI task configuration |
| `lib/conformance.dart` | Public entry point for the conformance test library |
| `lib/runner.dart` | Public entry for the test runner |
| `lib/test.dart` | Public test utilities |
| `bin/pipe.dart` | Executable that acts as a communication pipe between the conformance harness and the test runner |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `lib/src/` | Internal implementation: args parsing, invocation, protocol selection, test runners |
| `lib/src/gen/` | Protobuf-generated conformance proto types (do not edit) |
| `test/` | Tests for the conformance runner itself |

## Key Source Files

| File | Description |
|------|-------------|
| `lib/src/args.dart` | CLI argument parsing for the conformance runner |
| `lib/src/invoke.dart` | Invokes RPC calls against test targets |
| `lib/src/protocol.dart` | Protocol selection logic (Connect / gRPC / gRPC-Web) |
| `lib/src/runner.dart` | Core test execution engine |
| `lib/src/test.dart` | Test case definitions |
| `lib/src/test_hybrid.dart` | Tests that run on both I/O and web |
| `lib/src/test_io.dart` | Native I/O-specific conformance tests |
| `lib/src/test_web.dart` | Browser/web-specific conformance tests |

## For AI Agents

### Working In This Directory
- Files under `lib/src/gen/` are generated from the connectrpc conformance proto schema — never edit manually.
- The `pipe` executable is invoked by the external `connectconformance` binary to communicate test cases.
- Conformance tests require the external `connectconformance` binary (from the [connectrpc/conformance](https://github.com/connectrpc/conformance) repo) to be on `PATH`.
- Configuration for which tests run is in `packages/connect/test/conformance/conformance.io.yaml` and `conformance.web.yaml`.

### Testing Requirements
- `dart test test/runner_test.dart` runs unit tests for the runner itself.
- Full conformance suite: triggered via CI (`dart.yml`) using the `connectconformance` binary.

### Common Patterns
- Tests are split by platform: `test_io.dart` for native, `test_web.dart` for browser, `test_hybrid.dart` for both.
- Each test case sends a `ClientCompatRequest` proto and validates the response against expected outcomes.

## Dependencies

### Internal
- `connectrpc` (path: `../connect`) — the library under test

### External
- `protobuf: >=3.1.0 <5.0.0` — Protobuf runtime for conformance message types
- `archive: ^3.6.1` — Used for test data handling
- `shelf: ^1.4.2` + `shelf_web_socket: ^2.0.0` — Local HTTP server for web tests
- `web_socket_channel: ^3.0.1` — WebSocket support
- `args: ^2.5.0` — CLI argument parsing
- `test: ^1.25.8` — Test framework
- `stream_channel: ^2.1.2` — Stream channel utilities

<!-- MANUAL: -->
