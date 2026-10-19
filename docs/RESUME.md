# Resumability and single-agent checkpoints

The goal is to retain **verified knowledge**, not the entire model conversation.

Use `work/STATE.md` as the one-page index and `work/FINDINGS.md` as the canonical evidence summary. When useful, save original tool JSON locally under `work/evidence/`, named by target identity and question. Store binary/provider version separately. Do not write secrets or raw proprietary binaries to project Git repos.

## At start

1. Read `work/STATE.md` only (if present).
2. Confirm target identity matches the saved version.
3. Load just the finding referenced by the current lead.
4. Use matching REA snapshot / provider session when possible.
5. Continue from `next_exact_action`; do not rerun the overview without a reason.

## On meaningful progress

Update STATE with: exact target and version, objective, status, accepted/disproven hypotheses, strongest evidence IDs, tests performed, unresolved risks, next exact one or two queries. Keep under ~500 words. Put detailed evidence elsewhere and link it.

## On interruption/error

Save `last_successful_action`, last tool/provider, raw error code, whether an analysis process may still be running, cleanup state and the smallest safe retry. If a provider times out, **do not assume its child process stopped**. Never launch identical work before checking its state.

## Agent discipline

Default: one worker, sequential tasks, no automatic subagents. Do not launch a new worker to continue just because context grows; compress a checkpoint and continue. Never start background indefinite tasks without user authorization. If user explicitly wants multiple workers, separate ownership of modules/outputs and prevent duplicate scans, then merge evidence centrally.

## Completion record

Mark task as `done`, `partial` or `blocked`, state why, list output paths and evidence IDs and specify whether analysis could resume without re-reading original results.
