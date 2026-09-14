# Specialized repository work

Read the section matching the actual task. These refinements preserve the core loop.

## Monorepos and shared packages

Identify affected apps/packages, shared dependencies, build boundaries, and downstream consumers using workspace configuration, imports, exports, contracts, and dependency graphs where exposed. Validate the changed package first, then affected consumers. Task filters are useful only when their dependency semantics are understood.

Do not equate a single-file change with isolated impact. Shared authentication expiry, serialization, exports, or runtime behavior can affect web, API, and mobile differently. Root lockfiles/configuration or shared tooling may justify wider validation; isolated application changes do not justify blindly modifying or rebuilding everything.

## Libraries and SDKs

Inspect public exports, compatibility/versioning policy, supported runtimes, generated sources, package contents, documentation/examples, and consumer tests. Validate distribution/build artifacts and usage where affected. Preserve runtime and type-level contracts; a passing internal unit test does not prove published package imports work. Do not publish without authorization.

## CLI and desktop

For CLIs, preserve arguments, stdin/stdout/stderr contracts, exit codes, configuration paths, and supported shells/OS behavior. Use isolated fixtures for filesystem effects. For desktop apps, inspect main/renderer/native boundaries, IPC, permissions, window lifecycle, packaging and target OS. Validate affected runtime behavior and packaging as applicable; one OS build is not evidence for all platforms.

## Legacy and refactoring

Follow existing architecture and compatibility constraints. Modernization must be explicit. Refactoring preserves behavior unless a behavior change is requested: establish current behavior and consumers, inspect tests, then verify equivalence after the patch. Missing tests call for focused characterization, not a wholesale rewrite.

## Performance

Measure a representative baseline, identify the bottleneck, change the relevant cause, and measure again under comparable conditions. Record workload, environment, metric, and correctness checks. Distinguish observed improvements from estimates. Avoid speculative caching, concurrency, or micro-optimizations.

## Dependency upgrades and build fixes

Inspect installed/locked versions, supported runtimes, peer/transitive constraints, and official version-specific breaking changes. Upgrade only requested or necessary dependencies, incrementally when useful. Evaluate migration/codemod effects before execution, inspect resulting changes, maintain lockfiles with the existing package manager, and run affected builds/tests. Inspect warnings and obsolete configuration; remove it only when safely established as obsolete.

A failing install or build can be environmental. Diagnose before replacing packages, deleting lockfiles, or changing global tooling. New dependencies require an identified need not already served by the repository, platform, or existing dependencies.
