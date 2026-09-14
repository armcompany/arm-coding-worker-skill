# Context-driven validation

Before implementation, identify what will prove the requested outcome. Discover actual commands, working directories, fixtures, services, and required environments from the repository. Separate required acceptance gates from optional confidence checks; do not downgrade a required check after it fails or becomes unavailable.

For behavior changes, add or extend meaningful tests when the repository supports them. For a bug, reproduce the defect and establish a regression check that detects the original failure before the fix when feasible. If no test harness exists, declare and run a suitable reproducible manual or scripted check. Do not install a framework solely for a trivial edit or write tests that merely mirror implementation text.

## Select checks by affected behavior

| Change | Likely evidence, adjusted to repository conventions |
| --- | --- |
| Domain logic/API | Boundary and error cases, unit/integration tests, contract checks, types, build, API smoke when relevant |
| Web UI | Component behavior, forms/states, applicable types/lint/build, browser interactions, responsiveness and accessibility |
| Mobile | Logic/navigation tests, integration, affected native build targets and device/simulator behavior |
| Persistence | Migration/schema checks, representative data, constraints, transactions, old/new consumer compatibility |
| Shared package/library/SDK | Package tests/build/exports, public API compatibility, affected consumer tests/builds |
| Infrastructure | Syntax/format, validation, render/plan and policy checks in the authorized environment |
| CLI/desktop | Invocation or launch, errors/exit codes, packaging, affected OS/runtime behavior |
| Performance | Reproducible before/after measurements on comparable workloads |
| Security | Exploit/regression case, denied paths, privilege and data-isolation boundaries |

Run changed-module checks first, then affected packages/applications. Before completion, run the broadest reasonable checks justified by dependencies, risk, and repository requirements. Root configuration or shared contracts can justify broader validation; an isolated label change usually does not justify every monorepo build.

Use known sandbox/test targets for runtime, database, and integration checks. Validate real boundaries when required: a mock cannot prove external service delivery, and a web build cannot prove native mobile behavior. Browser/device checks must inspect the actual rendered or running feature when relevant tooling is available.

Record command or tool action, working directory/target, actual outcome, and concise evidence such as test counts or failure location. Keep full logs available where useful without exposing secrets. Wait for running processes or CI to finish before recording a result; command submission and partial output do not establish `PASS`.

## Outcomes

- `PASS`: check ran to completion and satisfied its assertion.
- `FAIL`: check ran and failed; record diagnosis and whether caused-by-change, pre-existing, environmental, dependency-related, configuration-related, or unknown.
- `NOT_RUN`: check did not execute; record the concrete missing prerequisite or reason.
- `NOT_APPLICABLE`: check does not apply to the established scope; explain briefly when non-obvious.

Compare with prior evidence or an isolated baseline when feasible before calling a failure pre-existing. Do not revert user files to establish that baseline. A diagnosed pre-existing failure may remain outside scope, but a required failing gate still prevents `completed` unless the authorized owner explicitly changes acceptance criteria. Report that decision and remaining risk.

## Final diff review

Inspect status, diff, staged diff, and new file contents through Git or equivalent tools. For a workspace without version control, compare against the initial inventory or captured originals and inspect all created/changed files; disclose that Git review was unavailable.

Review scope, accidental deletion/formatting, debug output, generated artifacts, secrets/credentials, unnecessary dependencies, stubs, incomplete TODOs, disabled checks, and compatibility. Review every changed file; distinguish worker changes from pre-existing user changes. Any corrective edit invalidates affected prior checks and requires proportionate revalidation.

Report implementation and validation separately. For example: “Implementation is present; API tests pass; required iOS build NOT_RUN because Xcode is unavailable; status blocked.” Never turn unavailable tooling into a passing result or an unqualified completion claim.
