# Adopted layered architecture

Read for all implementation. For HTTP changes also read [controllers](controllers.md);
for persistence/business logic read [services/data](services-data.md).

- Controllers own HTTP input validation, authentication/authorization and response
  codes. They call services, never DAOs/DbContext directly, and contain no business logic.
- Services own business operations, domain validation, coordination of DAOs and
  mapping persistence Models to output DTOs. Services receive DTOs or simple
  parameters; controllers do not perform Model-to-DTO mapping.
- DAOs/repositories own persistence queries/CRUD and return Models, not API DTOs.
  No business logic or deferred IQueryable escapes this boundary.
- DbContext owns EF entity mapping, relationships and database constraints.
- Public domain operations use explicit typed outcomes even when currently simple.
  Pure validation with expected rejection also returns an outcome. Infallible
  getters/internal calculations return values directly; do not wrap them mechanically.
- Expected rejection is not an exception. Unexpected technical faults, constructor
  precondition violations and invalid startup configuration can throw; never hide
  them as successful outcomes or expose their internals to clients.
- Keep API DTOs separate from persistence objects. Model/entity identity, grouping
  operations into services instead of separate UseCases, authentication strategies
  and concrete Result classes are project decisions, not inferred framework APIs.

Use descriptive English names: service, DAO, DTO, controller, middleware and
extension suffixes express responsibilities; interfaces use the `I` prefix.
Use the project's established folders and interfaces; no architecture migration is
implied. Services/DAOs use interfaces and constructor injection, normally scoped.
Singletons must be suitable for shared lifetime and must not capture scoped state;
choose other lifetimes only for an actual requirement, not an unverified speed claim.

Preserve adopted local conventions and security/ownership restrictions over external
examples. Record deviations with rule, justification and affected components; use
an ADR for architectural choices, significant trade-offs or disputed decisions.
Changing delivery is not permission to change a product's contracts or lint rules.
