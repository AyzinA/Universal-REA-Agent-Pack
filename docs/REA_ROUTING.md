# REA-first tool routing (version-aware)

**Official:** https://github.com/morluto/rea and https://github.com/morluto/rea/blob/main/docs/cli.md

REA evolves quickly. Discover actual MCP tools, params, advertised capability and host support in the **installed version**. This guide describes operation *types*, not a guarantee that every provider/host implements them.

## Startup capability gate

```bash
rea --help
rea providers --json
rea capabilities --json
rea doctor  # when available and useful
```

If using MCP, inspect the available tool list once and cache a small routing note. Never fabricate signatures. Choose a single supported native provider (Hopper, Ghidra or IDA where configured), rather than loading all providers for the same target.

## Route by artifact

| Observed format | Start with | Escalate to |
|---|---|---|
| PE, ELF, Mach-O, native DLL/SO/DYLIB | metadata, symbols, imports, narrow strings | provider function/xrefs/instructions or controlled runtime |
| .NET assembly / PE-CLI | metadata, type/member/IL inspection | ILSpy/managed debugging only when necessary |
| Java JAR, Android APK/DEX | manifest, package/classes/methods | JADX/bytecode, native `.so` only for JNI boundary |
| Electron/ASAR/JS/TS | app map, source maps, module/route/IPC | focused module and native addon analysis |
| Web app | permitted page/script/network observation | bounded client-side calls, source maps, WASM |
| WASM | imports/exports/sections | WAT & call structure |
| Firmware or unknown | magic/container/partition manifest | applicable unpacker and relevant processor target |

## Efficient native examples

```bash
rea search /path/to/binary "specific-string" --provider ghidra --json
rea function /path/to/binary 0xADDRESS --provider ghidra --json
rea xrefs /path/to/binary 0xADDRESS --provider ghidra --json
rea instructions /path/to/binary 0xADDRESS --provider ghidra --json
```

Use `rea --help`/subcommand `--help`: command syntax differs across releases. MCP sessions can reuse an open target; prefer this to repeatedly reopening a provider. Use snapshots when supported and exact inputs repeat.

## Snapshots (native REA feature; don't reinvent)

```bash
rea analyze /path/to/binary --provider ghidra --snapshot /safe/local/path/analysis.json
```

A snapshot replays only eligible, matching queries (same target bytes, settings, operation, parameters and provider). It **is not** a complete saved decompiler database. REA MCP supports `snapshot_path` on `open_binary` and save on `close_binary` in documented versions; verify actual schemas. Do not overwrite another version's snapshot.

## Avoid multi-MB JS/Electron responses

The official CLI/Evidence guide recommends saving full result once and inspecting a small view:

```bash
rea analyze-javascript-application /path/to/app --json > app-evidence.json
jq -c '{source:{kind:"inline",evidence:.},view:{kind:"summary"}}' app-evidence.json > app-view.json
rea inspect-analysis-view app-view.json
```

Filter further by selected module/page as documented. Redirect and store raw result locally, **do not paste the raw JSON into model context**. For security-sensitive targets, keep Evidence private.

## CLI output filtering

Recent REA versions document bounded `--token-limit` and `--token-offset`. Check locally. If not supported, use a local JSON projection (`jq` or small script) and view only required keys. Never silently truncate the sole support for a conclusion; preserve full raw local evidence and address it by ID/path.

## Provider failures

Use structured errors to distinguish target unsupported, provider missing, invalid operation, timeout, and genuine absence of a symbol. A timed-out client query may leave analysis running; inspect session state rather than launching duplicate runs. Use `rea doctor --provider <id> --json` where documented. Explicitly state unsupported operations and use a specialized tool only when justified.
