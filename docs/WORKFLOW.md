# Focused investigation workflow

## Phase 0 — choose an objective

Restate objective in one sentence. Define what would **falsify** each plausible interpretation and what deliverable ends the task. An example: “Locate and explain the function that serializes custom settings, with names/offsets and one behavior test,” not “reverse engineer this app.”

## Phase 1 — cheap target identity

Collect: absolute path, file magic/format, architecture, app version/build, hash (file SHA-256 where feasible), modules, packaging/runtime, available symbols/PDB/DWARF/source map, engine/provider version. For a directory, identify relevant entry points and component files; do not hash or enumerate gigantic asset trees for no reason. Branch by detected format, not the name or extension.

Check if this exact target + objective already has a report. If yes, **verify compatibility**, skip covered steps, and answer from saved evidence if sufficient.

## Phase 2 — reuse-first gate

1. Existing local source/debug symbols/metadata.
2. Previously saved REA evidence/snapshots, local research notes or code.
3. Official SDK/docs, public reference implementations, upstream and forks.
4. Public GitHub search limited to relevant project/component/feature, version and architecture.

Record: candidate, URL/path, license, how it matches this binary, what remains unproven. A similar implementation is a *lead*, not direct proof of how the target works.

## Phase 3 — minimal evidence plan

Write at most 3 hypotheses. Example:

- H1: settings dispatch invokes native function F.
- H2: serialization lives in managed type T.
- H3: UI calls JS IPC message M to a native add-on.

Pick **one** cheapest discriminating action per hypothesis. Avoid calling several decompilers for the same function without a reason.

## Phase 4 — targeted search (progressively more expensive)

1. Existing indices, symbols, imports/exports, type names, manifest/routes, error strings.
2. Exact text/name search with 2–5 narrow variants.
3. Direct references or selected call graph depth 1–2.
4. One relevant method/module/function and its immediate dependencies.
5. Assembly/CIL/bytecode/source map or observed behavior to settle a concrete ambiguity.
6. Wider search only if the evidence points to a new area.

For mobile/web targets, follow high-level method/module/IPC paths before machine code. For stripped native binaries, use strings/imports/call sites instead of relying on a `zC`-style class naming scheme.

## Phase 5 — decision and verification

Tag each conclusion `confirmed`, `supported`, `hypothesis`, or `unknown`. Distinguish: app's actual code, decompiled representation, behavior observed at runtime, API documentation, unrelated public implementation. If evidence conflicts, report the conflict and the missing observation.

## Phase 6 — deliver and stop

Stop when all task acceptance criteria are met and material assumptions are verified. Stop earlier if the required provider, permission, data, or tool is missing and a lower-cost alternative cannot resolve it. Do not switch into whole-app reconstruction or plugin writing unless requested.

## Priority order when budget is exhausted

Deliver in this order: confirmed findings → evidence locations → unresolved assumptions → smallest reproducible test → exact next query for resumption. Partial but correct evidence beats speculative completeness.
