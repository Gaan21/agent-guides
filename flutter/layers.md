# Layers, values and dependency lifetimes

Applies to domain/data/DI changes. Required: [failures](failures.md),
[conventions](conventions.md); [time](time-copy.md) for timestamps.

## Responsibility and data boundaries

- Keep presentation, domain decisions and external I/O separated. Domain stays
  independent of presentation and infrastructure I/O. Retain the project's layers;
  do not remove them because an upstream domain layer is conditional.
- Keep domain entities/value objects distinct from serialized data models. Sources
  expose intended data types, not UI/domain objects. Serialization belongs at the
  serialized data boundary; codecs must actually work, not merely carry annotations.
- Repositories coordinate sources/cache/synchronization and map models/entities;
  domain rules/defaults belong to the domain. “Only mapping” is not a complete
  description of repository coordination.
- Mappers are deterministic, pure conversions: no I/O, current clock, silent repair
  or invented business defaults. Reject malformed technical input explicitly with
  field context and preserve mapping failures. Test round trips and missing fields.
- IDs are consistent with actual domain/API types. Define creation/update semantics:
  absent/nullable/generated/local/remote IDs must match the contract. Never invent
  zero/empty sentinel IDs. Do not assume every backend uses the same ID type.

## Values and operations

- Prefer immutable values and safe collections. Validate nested mutation, equality,
  defaults and codec compatibility. A generator annotation does not establish deep
  immutability. Freezed is **not universally mandatory**; existing project generator
  selections remain authoritative, with no forced conversion to another approach.
- Public domain operations, including simple operations and pure validation with
  expected rejection, return the chosen Result protocol. Infallible getters and
  internal calculations return direct values; do not wrap every helper mechanically.
- Preserve installed use-case/base entrypoints, generic ordering, Params contracts
  and orchestration restrictions. Inspect real APIs before use. Do not copy a base
  implementation from a tutorial or introduce wrappers solely to imitate one.
- Avoid dependency cycles. Composition lives where project authority assigns it;
  existing no-usecase-composition or state-owner-isolation rules are not relaxed.

## Composition and lifetime

- Put I/O behind interfaces. Inject dependencies explicitly at composition roots;
  higher layers do not instantiate hidden infrastructure.
- Verify factory versus singleton lifetimes, scope, ownership and teardown. Borrowed
  dependencies are not disposed by borrowers. Inspect actual registrations.
- Infrastructure/settings state may have a different lifetime from domain state;
  do not force UI preferences into domain use cases. Follow native composition
  exceptions rather than imposing one container or registration scheme.
