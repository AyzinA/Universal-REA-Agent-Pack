# Implementation and validation (only when requested)

## Decide the output mode first

- `analysis`: report only.
- `compatibility`: implement documented observable behavior in target user's project/stack.
- `plugin/hook`: only with an authorized, supported extension surface and verified ABI.
- `reconstruction`: reproduce a specific subsystem, never silently expand to “all source code.”
- `bug`: isolate a minimal causal chain and reproducible input.

Use a verified existing library when licensing, versioning and behavior allow. Never recreate all parsing/asset support from scratch if a maintained parser suffices.

## Minimal contract

1. Write a brief functional contract: inputs, outputs, error behavior, state, side effects, cross-platform constraints.
2. Show source evidence for each nontrivial decision. Distinguish exact behavior from a compatible approximation.
3. Implement the smallest solution with names and interfaces natural for the requested codebase. Do not propagate a target-specific naming scheme into a universal engine.
4. Add deterministic tests (unit/golden/vector) before expanding the surface.
5. Validate only against authorized targets and data. Prefer isolated tests over executing unknown programs.
6. Summarize discrepancies and mark untested paths; do not claim byte-for-byte equivalence from similar-looking output.

## Native ABI/plugin checklist

Verify: exact binary build/hash; CPU/OS ABI; x86 calling convention (`thiscall`/`stdcall`/`cdecl`/etc where applicable); parameter widths and signedness; alignment/packing; ownership and lifetimes; exceptions; thread context; register preservation; hook/trampoline integrity; external plugin SDK version. Use exported/SDK symbols where possible instead of magic offsets. If any critical part is unknown, produce a **non-executable interface sketch** or safe wrapper rather than a working patch claim.

## Tests

- Low risk: pure logic golden vectors, serialization round-trip, sample file parsing, ABI type-size assertions, imports/exports.
- Moderate risk: plugin loads in a test harness; guarded runtime read-only observations.
- Higher risk: hooks/patches/instrumentation only in explicitly approved isolated test environments, with rollback/backup.

Save test commands and results. Never describe tests as passing unless executed and their outcome observed. The user may request a code-only draft: mark it as untested.

## Final output

Concise behavior explanation, evidence IDs, files changed, commands/tests and result, compatible target versions, unknowns and a rollback plan for modifications.
