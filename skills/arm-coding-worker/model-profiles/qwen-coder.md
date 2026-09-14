# Optional Qwen Coder execution profile

Apply over [the default](default.md) only when selected or when the host identifies the active model accordingly. No particular version, context size, tool syntax, benchmark advantage, or provider is assumed. This is an explicit cadence useful for constrained coding sessions; it is not required by the worker core.

Keep a compact execution card, in working state or an existing checkpoint:

```text
Objective: fix the calculation without changing the public contract
Current unit: domain calculation and its regression test
Evidence: implementation, callers, and test paths already inspected
Next operation: run the failing regression test
Exit criterion: regression and affected API checks pass; diff reviewed
```

- Break large plans into atomic behavior changes with an explicit check. Keep dependent API/client changes within one coherent acceptance unit.
- Search aggressively by relevant symbol or behavior before requesting more files. After a truncated read, retrieve the missing relevant range rather than guessing.
- Prefer one precise patch and one targeted verification per iteration. Group adjacent edits only when they implement the same behavior.
- Before a tool call, confirm the tool exists and its required fields. After a schema error, read the returned error/schema and correct the call; do not invent tool names or repeatedly submit the same arguments.
- On a failure, record `observation → hypothesis → next check` as concise operational facts. Carry forward the actual unresolved error.
- Refresh the execution card after each validated unit and before context handoff. Reload current files before applying a remembered patch.
- Keep reporting short, with explicit check outcomes and stopping conditions. Use machine output only when requested by the parent.

Increase unit size only when observed context and tool reliability support it. Retain all core gates at every cadence; reduced context is never permission to skip consumer analysis, tests, or diff review.
