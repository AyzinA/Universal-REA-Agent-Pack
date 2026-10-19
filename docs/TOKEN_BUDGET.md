# Token and tool-call budget (defaults; adjust to task)

The goal is **lower overall cost**, not an arbitrary number of calls. REA may have initialization overhead; caching a query or inspecting a compact evidence view usually matters more than saving one command.

## Default bounded loop

| Stage | Initial ceiling | Escalation only if… |
|---|---|---|
| Resume + triage | ~700 words of read context | target identity is ambiguous |
| Reuse search | 1 targeted local + 1 focused external search | no useful match, new exact identifier appears |
| Binary/app overview | 1 bounded summary | format/provider mismatch needs diagnosing |
| Search | 2–5 relevant terms, <=20 top hits | strongest lead fails |
| References | <=2 hops, <=10 nodes/hop | data flow crosses a known boundary |
| Decompile | 1–3 relevant functions/modules per iteration | direct proof requires one dependency |
| Tool response shown to LLM | ideally <=1,500 tokens each | need a precise longer excerpt to verify |
| Progress/summary | <=150 words per checkpoint | user explicitly requests detailed report |

These are starting heuristics, **not hard safety limits**. A single expensive call is warranted when it resolves the question; hundreds of small redundant calls are not.

## Query quality gate

Before invoking a tool, fill this mentally: `question | expected result | follow-up on yes | follow-up on no | stopping point`. If a call has no plausible effect on the decision, skip it.

## Return only information needed

- Prefer identifier/path/address/one-line summary over full function bodies.
- Prefer section, package, import, module or type filters before global scans.
- For CLI, use **documented** output controls such as `--token-limit` when supported; save JSON to disk and project compact fields rather than printing raw JSON. Verify flags using the installed `--help`.
- For JS/Electron, reuse REA's `inspect-analysis-view` on saved application Evidence. Ask for `summary`, then a particular page or module, not an entire multi-megabyte graph.
- Do not duplicate evidence in `STATE.md`, `FINDINGS.md`, and reports. Point to a canonical finding ID.
- Don't copy verbose third-party README files; save links with the 1–2 relevant symbols/functions.

## Stop / replan triggers

- No discriminating evidence after **two progressively better** attempts: change lead/tool or label blocked.
- Provider error: inspect error/remediation once, correct configuration once; no unbounded retry loop.
- Unrequested breadth: stop and present a scoped next option.
- Contradictory address from another version: record mismatch; do not guess translation.
- Need additional permissions: do not improvise runtime action.

## Checkpoint compression

Every meaningful branch leaves only: target ID, objective, confirmed facts, refs/evidence IDs, disproven hypotheses, active lead, next exact call, budget used. On resume, read this summary, **not the whole chat or tool history**.

## Tool-call batching

Batch small independent lookups only when result volume remains bounded. Do not batch huge `decompile-all`/`get-everything` operations. Limit parallelism to one agent by default and avoid unnecessary duplicate provider startup.
