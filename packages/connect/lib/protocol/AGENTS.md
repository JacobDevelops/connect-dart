<!-- Parent: ../AGENTS.md -->
<!-- Generated: 2026-04-21 | Updated: 2026-04-21 -->

# protocol (public re-exports)

## Purpose
Public re-export barrel files that expose the three concrete transport factories — Connect, gRPC, and gRPC-Web — as part of the `connectrpc` public API. Consumers import these to select which wire protocol to use.

## Key Files

| File | Description |
|------|-------------|
| `connect.dart` | Re-exports the Connect protocol transport factory from `src/connect/transport.dart` |
| `grpc.dart` | Re-exports the gRPC protocol transport factory from `src/grpc/transport.dart` |
| `grpc_web.dart` | Re-exports the gRPC-Web protocol transport factory from `src/grpc_web/transport.dart` |

## For AI Agents

### Working In This Directory
- These files are thin re-exports — implementation lives in `lib/src/{protocol}/transport.dart`.
- Consumers typically import via `package:connectrpc/protocol/grpc_web.dart` (for example) to get the `GrpcWebTransport` factory.
- Do not add implementation code here; keep these as pure re-export files.

<!-- MANUAL: -->
