<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# example

## Purpose
Sample applications demonstrating Connect-Dart usage. Contains a full Flutter app and a Dart web app, both implementing a chat client against the Eliza demo service.

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `eliza/` | Flutter app targeting Android, iOS, Linux, macOS, Windows, and Web (see `eliza/AGENTS.md`) |
| `web/` | Minimal Dart web app compiled to JS, demonstrating browser-only gRPC-Web usage (see `web/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- Example packages are **not** part of the workspace; they manage their own `pub get`.
- Generated files under `gen/` (`.pb.dart`, `.connect.client.dart`, `.connect.spec.dart`) must not be hand-edited — regenerate with `buf generate` from the example directory.
- Example apps depend on the published `connectrpc` package, not the local path version.

### Testing Requirements
- `flutter test` from `eliza/` for the Flutter example.
- Web example is verified by compiling with `dart compile js` or `webdev build`.

<!-- MANUAL: -->
