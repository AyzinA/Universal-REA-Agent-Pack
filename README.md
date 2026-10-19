# Universal REA Agent Pack — lean, resumable, reuse-first

Generic agent instructions for investigating **games and applications** on supported platforms. Works with Claude Code, Codex and other agents that can read `AGENTS.md` and use the REA MCP server/CLI. This pack does not include or install REA.

## Quick start

1. Install/configure **official** REA: https://github.com/morluto/rea or https://rea.tools/ — e.g. `npx rea-agents setup`, review the changes, then restart your agent. Verify the actual REA release, providers, and capabilities before relying on a tool.
2. Copy this pack into a research workspace. Create `TASK.md` from `templates/TASK.md` and fill in the target and one concrete question.
3. In your coding agent, say: **"Read AGENTS.md, TASK.md and work/STATE.md if available. Perform the requested investigation using REA and reuse existing research. Do not spawn subagents. Save concise evidence and stop once success criteria are met."**
4. Re-run with a new `TASK.md` for another application; store each target in its own `work/` folder to prevent mixing versions.

For a stand-alone one-shot request, copy `MASTER_PROMPT.md` and fill the placeholders. On Claude Code, `CLAUDE.md` points to `AGENTS.md` without duplicating instructions.

## File map and context-loading policy

| At startup | Purpose |
|---|---|
| `AGENTS.md` | Small universal operating policy (always) |
| `TASK.md` | User's question and permission scope (create from template) |
| `work/STATE.md` | Resume state, if it exists |

Open **only relevant** additional guides: `docs/` for procedure, `references/PROJECTS.md` for existing solutions, `templates/` for output. Reading everything at startup defeats the token-efficiency goal.

## What REA can do

REA's exact availability depends on installed release, OS and providers. The official project documents native binaries with Hopper/Ghidra/IDA, JS/Electron apps, websites, .NET/managed code, Android APKs, and additional formats such as WASM and firmware in certain environments. Run capability discovery first; unsupported is not the same as impossible to investigate using another appropriate tool.

Quick checks (after installation):

```bash
rea --help
rea providers --json
rea capabilities --json
```

Sample narrow commands (arguments and formats should be verified with `--help`):

```bash
rea search /path/to/program "feature" --provider ghidra --json
rea function /path/to/program SYMBOL_OR_ADDRESS --provider ghidra --json
rea xrefs /path/to/program 0xADDRESS --provider ghidra --json
```

When an operation produces a huge JSON result, write it to a **local evidence file** and inspect a summary or bounded view. REA supports snapshots for eligible exact analysis queries; see `docs/REA_ROUTING.md`.

## Basic ground rules

- **Do not assume original source can be recovered** from compiled binaries. Recovered code is a decompiler reconstruction.
- **Reuse before redo**; review license, architecture, and exact version before copying/porting code.
- **No automatic brute-force full-app decompilation** unless the task explicitly requests full coverage with a budget.
- **No unsupported runtime actions**; read-only analysis is default.
- **No automatic parallel agents**; single-agent is default.
- **No raw binary or secrets in shared logs/repositories**.

## Example targets

- `C:\\Apps\\MyApp\\app.exe` — trace a settings serialization function.
- `/opt/example/bin/app` — map a plugin interface and its struct layout.
- `/Applications/Example.app` — follow a UI command to its handler.
- `/apps/client/resources/app.asar` — trace an Electron renderer-to-main IPC path.
- `/downloads/example.apk` — understand an offline cache feature.
- `https://example.com` — map a site's public client-side workflow, subject to permitted observation.

## Official references

- REA: https://github.com/morluto/rea
- REA CLI/Evidence: https://github.com/morluto/rea/blob/main/docs/cli.md
- Curated third-party catalog: `references/PROJECTS.md`
