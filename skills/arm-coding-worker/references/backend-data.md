# Backend, contracts, and persistence

## API and domain

Follow the repository's routes/controllers, services/use cases, repositories, DTOs/schemas, entities and error conventions. Locate existing equivalents before adding endpoints or abstractions. Preserve the detected REST, GraphQL or gRPC style.

Trace client → contract → API → domain → persistence. Before contract changes, search all consumers and generated clients, including external consumers documented in specs or version policy. Consider semantic compatibility as well as shape. Update necessary clients and contract tests together; regenerate generated artifacts from their source.

Apply validation, authentication, authorization, transactions, concurrency, idempotency, error handling, caching, queues/events, and observability only where the behavior requires them. Preserve denial paths and avoid leaking sensitive internals. An ordinary endpoint does not justify a new architecture.

For cross-layer features, establish the existing contract or authorized compatibility change first, implement affected components in dependency order, and validate their integration. Mocked UI/API checks do not prove the real boundary. Do not fabricate a successful external delivery when email, payment, or another service is unavailable.

## Data changes

Before editing persistence, inspect schema, migrations, ORM/data-access conventions, consumers, and deployment ordering. Determine whether a schema change is needed at all. Identify compatibility requirements for old and new application versions, constraints, indexes, transactions, backfills, locking, and representative data volume where relevant.

Prefer additive/expand-contract migrations when existing consumers must continue operating. Establish rollback or forward-recovery appropriate to the data change; a rollback script does not necessarily restore deleted data. Do not rewrite an already applied migration as if production history were disposable.

Validate migrations in an authorized disposable/local environment with representative data and affected application behavior. Check data preservation and constraints, not only successful SQL parsing. Resolve the target connection before execution without printing credentials. Preparing a migration does not authorize applying it to production, resetting a database, or discarding user data.

Account deletion, recovery tokens, permissions, billing, and other sensitive data flows also require [security](security.md). Resolve missing business decisions such as retention or deletion policy before irreversible behavior; repository evidence may already define them.
