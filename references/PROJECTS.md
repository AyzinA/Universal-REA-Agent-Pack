# Curated public reverse-engineering projects — select by target

Use as an index to avoid rebuilding solved components, **not as a checklist to read in full**. Prefer official upstream and verify commit, license, target version, supported OS and exact behavior before reuse.

| Project (upstream URL) | Useful for | Reuse guidance |
|---|---|---|
| [REA](https://github.com/morluto/rea) | MCP/CLI investigations across native/managed/JS/app layers | Primary workflow and Evidence; use documented caches/views |
| [Ghidra](https://github.com/NationalSecurityAgency/ghidra) | Multi-ISA native disassembly, decompilation, scripting | Choose if REA-native provider configured |
| [LIEF](https://github.com/lief-project/LIEF) | PE/ELF/Mach-O metadata, parse/patch interfaces | Triage and ABI/container details |
| [angr](https://github.com/angr/angr) | Native program path/control-flow/symbolic analysis | Only when static search insufficient |
| [capa](https://github.com/mandiant/capa) | Executable capability identification | Triage unknown binaries; evidence is heuristic |
| [FLOSS](https://github.com/mandiant/flare-floss) | Extract obfuscated/decoded strings | Escalation for hidden string evidence |
| [Frida](https://github.com/frida/frida) | Runtime observation/dynamic instrumentation | Authorized, sandboxed runtime only |
| [ILSpy](https://github.com/icsharpcode/ILSpy) | .NET assembly decompilation | Prefer managed metadata/IL before native code |
| [JADX](https://github.com/skylot/jadx) | Android APK/DEX and Java methods | Use when app actually contains DEX/Java |
| [WABT](https://github.com/WebAssembly/wabt) | WebAssembly imports/exports, WAT and utilities | Inspect WASM artifact interfaces |
| [BinExport](https://github.com/google/binexport) | Export graphs for binary/version comparisons | Use for target diffing if configured |
| [Electron ASAR](https://github.com/electron/asar) | Electron ASAR packaging | Parse package container; prefer REA JS views |

## Finding existing target-specific code

- Search **exact product + binary version** with `sdk`, `symbols`, `pdb`, `decompile`, `source`, `modding`, `plugin`, `reimplementation`, `parser`, `format`.
- Prioritize official repositories, actively maintained original projects, documented reverse-engineering research and stable SDKs; record license and commit.
- An API-compatible implementation is not necessarily byte-identical; verify the specific boundary relevant to the task.
- For games, useful reference *examples* include [OpenGothic](https://github.com/Try/OpenGothic) (open reimplementation) and [ZenKit](https://github.com/GothicKit/ZenKit) (asset/format parsing), but do **not** load these for unrelated apps.

## Source attribution note

URLs are pointers, not proof of exact compatibility. Avoid assuming an identified symbol, structure or GitHub snippet applies to a given installed build without checking. Research dates and versions can change.
