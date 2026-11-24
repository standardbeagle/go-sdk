# AGENTS.md

## Project Overview

此庫乃 Model Context Protocol (MCP) 官方 Go SDK。其制尚 idiomatic、future-proof、extensible。

### Key Packages

- `mcp`: 核心包；定構建、使用 MCP clients 與 servers 之主 APIs；多數邏輯居此。
- `jsonrpc`: 供 JSON-RPC 2.0 transport layer；自製 transports 則用之。
- `auth`: 支 OAuth 之 primitives。
- `oauthex`: OAuth protocol 之 extensions，如 Protected Resource Metadata。
- `internal`: 內部實作，不示用戶。
- `examples`: clients 與 servers 範例；用作 usage patterns 參照。

## Development Setup

用 standard Go toolchain。

- **Build**: `go build ./...`
- **Test**: `go test ./...`

## Testing

- **Unit Tests**: 行 `go test ./...`，盡跑 unit tests。
- **Conformance Tests**: 以下 scripts 以 SDK 對 official MCP conformance tests。
  - `./scripts/server-conformance.sh` 為 server tests。
  - `./scripts/client-conformance.sh` 為 client tests。
  - scripts 預設自 npm 下載 latest conformance suite。
  - 欲見 options，傳 `--help` flag 於 script。

## Development Guidelines

### Code Style

- 循 standard Go conventions (Effective Go)。
- 以 `gofmt` 格式化 code。
- 凡新 Go files，必加 copyright headers：
  ```go
  // Copyright 2025 The Go MCP SDK Authors. All rights reserved.
  // Use of this source code is governed by the license
  // that can be found in the LICENSE file.
  ```
- 非真必要勿加 comments：
  - 尚 self-documenting code。
  - comments 重 "why"，勿重 "what"。

### Documentation

- **README.md**: 勿直改 `README.md`。其由 `internal/readme/README.src.md` 生成。
  - 改 `internal/readme/README.src.md`。
  - 行 `go generate ./internal/readme` 再生成。
  - 兩 files 皆 commit。
- **docs/**: 勿直改 `docs/` directory。其由 `internal/docs` 中 files 生成。
  - 改 `internal/docs/*.src.md`。
  - 行 `go generate ./internal/docs` 再生成。
  - 兩 directories 之 files 皆 commit。