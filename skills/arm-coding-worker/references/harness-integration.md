# ARM handoff and standalone operation

The worker accepts an ordinary task or a parent task record containing objective, acceptance criteria, constraints, architecture/design decisions, relevant context paths, allowed operations, validation requirements, and optional model profile/budget. Missing optional fields do not block work; infer routine details from repository evidence.

Treat explicit parent decisions as authoritative within user and host constraints. If repository evidence reveals a direct incompatibility, report the exact conflict and available alternatives before implementing that dependent decision. Do not silently substitute architecture or redesign the product.

When `.harness/` exists, inspect its actual format. ARM variants may use `state.json` with mission/plan/journal/checkpoints or `status.md` with phase artifacts. Reconcile the active task with current code and diff. Update only task-relevant records when persistence is authorized. Do not initialize or migrate the parent's state system automatically.

Standalone use requires no parent installation, model router, MCP server, vendor API, or persistent-state directory. A task with sufficient context plus exposed repository tools is enough. This document defines interoperability, not an executable scheduler, permissions system, or guarantee that unavailable tools can run.

## Status semantics

Use the parent's requested serialization and map statuses explicitly; normal human reports need no YAML.

| Worker status | Meaning | Typical ARM mapping |
| --- | --- | --- |
| `completed` | Acceptance criteria and required verification passed; final diff reviewed | `DONE` / `completed` |
| `blocked` | A missing decision, access, authority, service, toolchain, or external prerequisite prevents remaining required work | `BLOCKED` / `blocked` |
| `partial` | Useful work exists, more work remains, and a safe continuation exists; used at checkpoint, budget limit, or handoff | `RUNNING` / `in_progress` with remaining work |
| `failed` | Bounded evidence-driven attempts leave an unresolved technical failure with no supported continuation | `FAILED`, or the parent's supported failure record |

One failed test does not automatically make the whole task `failed`; debug it. Implemented code with a required unavailable check is `blocked` once independent work is exhausted. A passing subset never makes the whole task `completed`. `partial` is not a reason to stop while authorized useful work can continue. Parent status schemas may differ; never invent an unsupported state value.

An evidenced pre-existing, out-of-scope failure in a required gate is `blocked` once independent work is exhausted: identify the needed gate repair or authorized acceptance decision. Do not manufacture failed debugging attempts or repair unrelated code merely to fit a status.

## Output fields

For a machine handoff, expose these concepts in the requested format. Each validation entry carries `outcome`, `required`, `command_or_action`, `target`, `evidence`, and `reason` where applicable; use the outcome vocabulary from [validation](validation.md).

```yaml
task_id: TASK-042
status: blocked
project_context:
  architecture: monorepo
  stack: [React Native, NestJS]
task_scope:
  type: feature
  affected_layers: [mobile, api, auth]
changes:
  files:
    - path: apps/mobile/src/auth/recovery.ts
      purpose: Handle recovery deep links
validation:
  tests:
    outcome: PASS
    required: true
    command_or_action: npm test -- --runInBand
    target: apps/api
    evidence: "Observed exit 0; 18 tests passed"
  ios_build:
    outcome: NOT_RUN
    required: true
    command_or_action: build configured iOS target
    target: apps/mobile/ios
    reason: Xcode unavailable
risks: [iOS recovery flow remains unverified]
remaining_work: [Run required iOS build and recovery flow validation]
next_action: Resume on an authorized host with Xcode
```

This is an illustrative partial record, not actual evidence or a universal command. Include all actual changed files and selected checks, including typecheck/lint/build/integration/platform checks as relevant. Never copy sample counts into a real report.

Preserve task ID, accepted decisions, changed files, validation state, unresolved failures, and next action across models. Unknown model metadata stays unknown. A parent may route implementation, reasoning, or review elsewhere; each worker must re-establish relevant repository state and retain the same completion contract. Budget exhaustion produces an honest checkpoint, not fabricated completion.
