<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# web (Dart web example)

## Purpose
Minimal Dart web application demonstrating Connect-Dart usage in a browser environment. Uses the gRPC-Web transport to communicate with the Eliza demo service. Compiled to JavaScript via `dart compile js` or `webdev`.

## Key Files

| File | Description |
|------|-------------|
| `pubspec.yaml` | Package manifest; depends on published `connectrpc` package |
| `buf.gen.yaml` | Buf generation config for the eliza proto |
| `analysis_options.yaml` | Dart analyzer settings |
| `README.md` | Setup and run instructions |
| `web/index.html` | Entry HTML that loads the compiled Dart app |
| `web/main.dart` | Dart entry point; wires up the Connect client and UI |
| `web/styles.css` | Application styles |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `web/gen/connectrpc/eliza/v1/` | Protobuf-generated client and message types (do not edit) |
| `web/icons/` | Web app icons |

## For AI Agents

### Working In This Directory
- Browser-only; uses `connectrpc/web.dart` transport — do not import `connectrpc/io.dart`.
- Generated files under `web/gen/` come from buf; never edit manually.
- This package is **not** part of the workspace; run `dart pub get` separately.

### Testing Requirements
- Build with `dart compile js web/main.dart -o web/main.dart.js` and open `web/index.html` in a browser.
- No automated test suite; verification is manual.

## Dependencies

### External
- `connectrpc` — Connect-Dart library (published version, web entry point)

<!-- MANUAL: -->
