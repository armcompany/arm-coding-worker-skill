# Universal execution profile

Use this baseline for any capable coding model, local or hosted, with unknown or known metadata. Assume finite context, fallible tools, repository access where exposed, and optional shell access. Do not probe private configuration or guess capabilities from a model name.

1. Keep the objective, acceptance criteria, affected files/contracts, current check, and next action in working context.
2. Search before expanding context. Read dependencies as needed; preserve relevant public interfaces and failure output even when shortening context.
3. Work in one coherent implementation unit, validate it, then proceed to the next dependent unit.
4. Confirm tool argument schemas and inspect actual results. A submitted command is not a completed operation.
5. Use a short plan for simple changes; explicit checkpoints for cross-layer work, interruptions, or approaching context limits.

Adapt to observed constraints:

| Available capability or constraint | Execution adjustment |
| --- | --- |
| Small context or unreliable long instructions | Smaller work units, focused reads, explicit next action, more checkpoints |
| Limited tool calling or structured output | One operation at a time; validate arguments before calling; inspect returned state |
| Stronger reasoning or larger context | Broader impact analysis when justified; retain targeted reads and review gates |
| High latency or cost limit | Batch independent reads; avoid redundant checks; do not omit required validation |
| No shell | Use exposed test/build/file capabilities; document checks that remain unavailable |
| No visual input or browser/device tool | Use available nonvisual checks; report visual/runtime validation gaps separately |

An optional [Qwen Coder profile](qwen-coder.md) provides a more explicit execution cadence when selected by the user or parent, or when exposed metadata identifies that family. Its defaults are tunable workflow choices, not claims that every version has the same capabilities. With absent metadata and no selection, stay with this baseline.

Profiles may tune granularity, context, planning, calls, output shape, and checkpoints. They cannot weaken search/read discipline, validation, diff review, user-work preservation, or authorization. Routing and actual model switching remain host responsibilities; do not claim a switch without host evidence.
