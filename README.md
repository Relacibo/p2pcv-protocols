# P2PCV Shared Protocols

Unified Bebop protocol definitions for p2p-chessvariants (frontend) and p2pcv-server (backend).

## Structure

- `schemas/` — Source `.bop` files for Bebop protocol definitions
  - `c2s.bop` — Client-to-server messages (sent during authentication, game invites)
  - `s2c.bop` — Server-to-client messages (game events, friend notifications)
  - `lobby.bop` — Peer-to-peer messages (lobby join/start/leave)

## Usage

Both frontend and server reference this repo as a submodule. During build:

### Frontend (TypeScript)
```bash
# Regenerate types
yarn bebop

# Generated file: src/api/bebop/generated.ts
```

Requires: `bebopc` CLI
```bash
cargo install bebop-tools
```

### Server (Rust)
```bash
# Automatically regenerated during build
cargo build -p p2pcv-bebop

# Generated file: libs/pvpcv_bebop/src/generated/mod.rs
```

Uses: `build.rs` downloads and runs `bebopc` automatically

## Adding New Messages

1. Edit `.bop` schema file
2. Push to this repo
3. Update submodule in both repos: `git submodule update --remote`
4. Regenerate types:
   - Frontend: `yarn bebop`
   - Server: `cargo build -p p2pcv-bebop`
5. Commit generated files in both repos

## Protocol Versioning

The API has a single version (no versioning per-message yet). Maintain backward compatibility 
or bump the version carefully across both repos simultaneously.

