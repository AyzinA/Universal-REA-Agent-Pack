# Task

- **Target:** `<exact absolute file path | app bundle | directory | URL>`
- **Question:** `<one precise feature, function, memory layout, crash, protocol, or behavior>`
- **Deliverable:** `analysis` (default) | `implementation` | `plugin` | `port` | `bug fix` | `comparison`
- **Output codebase / language:** `<only if implementation requested>`
- **Acceptance criteria:** `<measurable evidence, behavior, or test>`
- **Binary version/build:** `detect; do not guess`
- **Constraints:** `single agent; lean output; scope-limited search`
- **Permissions:** `read-only static inspection` (default; state any approved runtime actions)
- **Resource budget:** `default / custom max calls, time, or output`
- **Relevant existing source or SDK:** `<path/URL if known>`

## Notes

A broad “analyze everything” instruction is costly. If the exact area is initially unknown, do a **bounded capability/architecture overview**, report prioritized next questions, and stop rather than recursively decompiling everything.
