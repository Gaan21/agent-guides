# Services and EF Core data access

Dependency: [architecture](architecture.md). Performance changes additionally need
[performance](performance.md); database tests need [testing](testing.md).

## Services

Implement interfaces and constructor-inject required DAOs. Keep domain rules in
services, map Models to output DTOs before returning and never depend on HTTP
Request/HttpContext. Coordinate data access without leaking persistence details.
Use explicit success/rejection outcomes for public domain operations and expected
validation failures; preserve typed data versus no-data cases and actual error
semantics. Concrete type/factory names come from the selected project, not this guide.
Unexpected technical, precondition and configuration exceptions remain distinct.

## Persistence

- DAOs implement interfaces; keep CRUD/query behavior separate from business rules.
- Use AsNoTracking for read-only entities; do not disable tracking for updates that
  need it. Include needed relationships deliberately to avoid lazy-loading surprises.
- Accept and propagate CancellationToken for async application/data operations;
  framework lifecycle signatures are not changed to force an extra parameter.
- Materialize query results before returning across the DAO boundary. Return Models
  rather than presentation DTOs, and do not export IQueryable to callers.
- Configure keys, lengths, constraints and relationships in the model configuration.
  Do not infer concrete entities, fields or migrations from examples.
- Prefer DbContext pooling where appropriate for the chosen application lifetime
  and state model. Pooling is not universally mandatory; test-provider replacement
  must account for actual registrations and cannot be proved by one removal snippet.
- Scoped lifetime is the normal service/DAO default. No shared mutable DbContext
  across concurrent work; a scoped object alone does not guarantee serial execution.
- Production/development schema changes follow the project's migration contract.
  Disposable test schema creation is not a migration recipe for a persistent DB.

Verify provider/version-specific translation against the actual query/provider before
claiming support. Keep documented product exceptions alongside general batching
advice; do not automatically rewrite working queries or replace the provider.
