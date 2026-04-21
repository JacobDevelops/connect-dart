<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# eliza (Flutter example)

## Purpose
Full Flutter application demonstrating Connect-Dart usage with the Eliza demo service. Implements a chat UI that communicates via unary, server-streaming, and bidirectional-streaming RPCs. Supports all 6 Flutter platforms: Android, iOS, Linux, macOS, Windows, and Web.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Flutter package manifest; depends on published `connectrpc` package |
| `buf.gen.yaml` | Buf generation config for the eliza proto |
| `buf.yaml` | Buf module configuration |
| `analysis_options.yaml` | Dart analyzer settings |
| `proto/eliza.proto` | Source proto definition for the Eliza service |
| `lib/main.dart` | Flutter app entry point and UI |
| `lib/http.dart` | Platform-agnostic HTTP client abstraction |
| `lib/http_io.dart` | Native platform HTTP implementation (uses `connectrpc/io.dart`) |
| `lib/http_web.dart` | Web platform HTTP implementation (uses `connectrpc/web.dart`) |
| `test/widget_test.dart` | Flutter widget tests |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `lib/gen/` | Protobuf-generated client and message types (do not edit) |
| `android/` | Android native configuration |
| `ios/` | iOS native configuration |
| `linux/` | Linux native configuration |
| `macos/` | macOS native configuration |
| `windows/` | Windows native configuration |
| `web/` | Web assets (HTML, icons) |

## Generated Files (lib/gen/)

| File | Description |
|------|-------------|
| `eliza.connect.client.dart` | Generated Connect client extension type |
| `eliza.connect.spec.dart` | Generated service spec (method descriptors) |
| `eliza.pb.dart` | Generated protobuf message classes |
| `eliza.pbenum.dart` | Generated protobuf enums |
| `eliza.pbjson.dart` | Generated JSON serialization |
| `eliza.pbserver.dart` | Generated server stubs (unused client-side) |

## For AI Agents

### Working In This Directory
- This package is **not** part of the workspace — run `flutter pub get` separately.
- All files in `lib/gen/` are generated from `proto/eliza.proto` via `buf generate`; never edit manually.
- Platform-specific HTTP transport is selected at compile time via conditional imports (`http_io.dart` vs `http_web.dart`).
- Depends on the **published** `connectrpc` package, not the local path version.

### Testing Requirements
- `flutter test` runs widget tests.
- Manual testing required for each target platform (Android, iOS, Linux, macOS, Windows, Web).

### Common Patterns
- `lib/http.dart` defines the interface; platform files implement it — this is the standard Flutter pattern for platform-conditional imports.
- All RPC calls go through the generated `ElizaServiceClient` extension type.

## Dependencies

### External
- `connectrpc` — Connect-Dart library (published version)
- `flutter` SDK

<!-- MANUAL: -->
