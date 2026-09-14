# Repository discovery and classification

Start from the actual workspace root and applicable repository instructions. Inspect a shallow map and relevant manifests before deep reads. Exclude dependencies, build outputs, caches, and generated assets from broad searches unless they are the subject of the task.

Use evidence to identify architecture, applications, shared packages, stack versions, package managers, command working directories, runtime targets, and testing/build boundaries. Read README/setup instructions, architecture documents, environment examples, CI, scripts, lint/format/test configuration, and representative code. Do not dump secret-bearing environment files.

## Signals, not assumptions

| Evidence | Inspect next |
| --- | --- |
| `package.json`; pnpm/Yarn/npm/Bun lockfiles | Dependencies, scripts, engines, package manager field, framework versions |
| `pnpm-workspace.yaml`, workspace declarations, `turbo.json`, `nx.json`, Lerna config | Package graph, task dependencies, filters, affected-project support |
| `pom.xml`, `build.gradle`, `settings.gradle`, `gradle.properties` | Maven/Gradle wrappers, modules, plugins, target Java/Kotlin, tests |
| `pyproject.toml`, requirements/lockfiles | Python environment manager, frameworks, test/type/lint settings |
| `go.mod`, `Cargo.toml`, `*.sln`, `*.csproj` | Modules/workspaces, targets, tests, public packages |
| `Gemfile`, `composer.json`, framework configuration | Server architecture, dependency management, scripts |
| `Podfile`, `*.xcodeproj`, `*.xcworkspace`, `Package.swift` | Native targets, schemes, dependencies, platform build prerequisites |
| `pubspec.yaml`, Android/iOS folders, Expo/React Native configuration | Mobile framework, plugins, native overrides, supported platforms |
| Dockerfile, Compose files, Terraform, Kubernetes, Helm, CI workflows | Environment boundaries, delivery commands, validation and deployment separation |
| `apps/`, `packages/`, `services/`, `frontend/`, `backend/`, `api/`, `mobile/`, `src/` | Actual ownership and call relationships; names alone do not establish architecture |

Confirm backend frameworks such as NestJS, Express, Fastify, Spring, FastAPI, Django, Flask, Rails, Go or .NET from dependencies and code. Identify REST, GraphQL or gRPC contracts and controllers/routes, services/use cases, repositories, entities, DTOs/schemas, migrations, jobs, queues, events, auth, caching, and observability where present.

For React, Next.js, Vue, Angular, Svelte, Vite, Remix or Astro, locate routing, state, API clients, forms, styling, tokens, components, responsive and accessibility conventions. For React Native/Expo, Android Kotlin/Java, iOS Swift, Flutter or multiplatform, locate navigation, native modules, lifecycle and platform configuration.

Infrastructure can include Docker/Compose, Kubernetes, Terraform, Helm, GitHub Actions, GitLab CI, Bitbucket Pipelines, Vercel, Cloudflare, AWS, Azure or GCP. Its presence does not place it in task scope.

## Describe multiple dimensions

Use any relevant labels: `api`, `frontend`, `full-stack`, `mobile`, `mobile-api`, `desktop`, `cli`, `library`, `sdk`, `infrastructure`, `monorepo`, `multi-app`, `mixed`, `unknown`.

Example discovery record:

```yaml
architecture: monorepo
applications: [web, api, mobile]
shared_packages: [ui, auth, contracts]
task_type: bugfix
affected_layers: [api]
evidence: "Calculation implementation and callers reside in the API; client contract unchanged."
```

A manifest can be stale and a lockfile can belong to another package. Resolve conflicting signals with CI and actual source usage. Record unresolved uncertainty instead of guessing a stack or running all package managers.

For an empty project, establish from the task and workspace evidence whether greenfield creation is intended; an explicit creation request is sufficient. Use supplied architecture/design decisions; choose minimal conventional foundations when choices are routine. Ask only about missing decisions with material product or technical consequences.
