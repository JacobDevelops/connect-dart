<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# bin

## Purpose
The `protoc-gen-connect-dart` protoc plugin executable. Reads a `CodeGeneratorRequest` from stdin (as provided by `protoc` or `buf`) and writes a `CodeGeneratorResponse` to stdout, generating `.connect.client.dart` and `.connect.spec.dart` files for each proto service definition.

## Key Files

| File | Description |
|------|-------------|
| `protoc-gen-connect-dart.dart` | Entry point: reads stdin, delegates to `src/run.dart`, writes to stdout |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `src/` | Plugin implementation (see `src/AGENTS.md`) |
| `src/gen/` | Generated protobuf descriptor types for the plugin protocol (do not edit) |

## For AI Agents

### Working In This Directory
- The binary is invoked by `buf` or `protoc` as a plugin; it communicates exclusively via stdin/stdout using protobuf-encoded `CodeGeneratorRequest`/`CodeGeneratorResponse` messages.
- Do not add `print()` or any logging to stdout — it corrupts the protoc protocol. Use stderr for debug output.
- Install globally with `dart pub global activate connectrpc` to make `protoc-gen-connect-dart` available on PATH.
- Plugin tests are in `packages/connect/test/plugin/` using golden file comparison.

### Testing Requirements
- Run plugin tests: `dart test test/plugin/plugin_test.dart`
- Golden files in `test/plugin/golden/` define expected output — update them with `dart test --update-goldens` only when output changes are intentional.

### Common Patterns
- Plugin reads the entire stdin buffer before processing (protobuf framing).
- Generated client files use Dart extension types (`extension type FooClient(Transport _transport)`).
- Generated spec files expose static `Spec` constants for each RPC method.

<!-- MANUAL: -->
