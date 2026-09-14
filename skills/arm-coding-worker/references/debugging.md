# Evidence-driven debugging

Use failure → complete relevant error → subsystem → hypothesis → discriminating check → smallest fix → same validation again.

1. Capture the failing command/action, target, exit/result, relevant full error and causal stack. Retrieve truncated sections rather than inferring the missing cause. Redact credentials from reports.
2. Reproduce when safe. Classify the failure as caused-by-change, pre-existing, environmental, dependency-related, configuration-related, or unknown. “Unknown” is preferable to an unsupported attribution.
3. Trace the behavior through relevant implementation, types, callers, contracts, configuration, and tests. Compare working paths or recent changes when useful.
4. Form one falsifiable hypothesis and choose the smallest check that distinguishes it from alternatives. Change one cause at a time.
5. Apply the root-cause fix within task scope, then rerun the original failing validation and affected regression checks. Passing a different check does not resolve the original failure.

If a hypothesis fails, record the new observation and revise it. For a plausibly transient failure, allow at most two executions with unchanged inputs and conditions (the initial attempt plus one retry). A third execution requires a changed condition or supported hypothesis. After three distinct unsuccessful hypotheses, checkpoint and reassess the subsystem, scope, and remaining evidence. Continue only with a supported next path; otherwise hand off a diagnosed failure or exact external blocker.

Do not conceal failures through disabled tests, swallowed exceptions, unsafe casts, unnecessary `any`, lint/compiler suppressions, arbitrary delays, commented-out behavior, or reduced assertions. A suppression requires a concrete technical justification and validation of the affected behavior; it is never a substitute for understanding the failure.

| Temptation | Required response |
| --- | --- |
| “The deadline requires green.” | Preserve the failing evidence and fix the cause; a deadline is not evidence. |
| “The package passes, so consumers are fine.” | Trace behavior and verify affected consumer assumptions. |
| “Run the same install again.” | Identify a changed condition or stop the repeated attempt. |
| “It was already broken.” | Establish baseline evidence and report scope; do not silently ignore a required gate. |

When tooling fails, distinguish malformed tool arguments from command failure, missing capability, denied permission, and unavailable services. Use the host's supported approval/recovery mechanism when necessary; do not bypass a denied operation with another tool.
