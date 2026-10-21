# Completion, concurrency, retry and background work

Applies to async operations and lifecycle initialization. Required:
[failures](failures.md), [resources](resources.md); [offline](offline.md) when selected.

- Before implementation identify operation key, inputs, result/error owner,
  criticality, concurrency policy, stale-result rule, cancellation, retry and teardown.
- Await contracted acceptance before success/navigation. Online acceptance can
  require server confirmation; an approved offline flow can accept a durable local
  write visibly pending sync. Local acceptance is never remote acknowledgment.
- Critical writes are not fire-and-forget. Consume Result failures even when no
  exception is thrown. Cancellation of a Future does not undo server side effects;
  define idempotency and late acknowledgment handling.
- Replaceable reads may cancel/discard stale results; duplicate writes use approved
  single-flight/shared completion. Independent parallel reads require a justified
  operation contract. Preserve existing stricter per-screen concurrency restrictions.
- Multiple initial-load/refresh/retry triggers share the same in-flight completion
  where they represent one load. Clear it on success/failure; refresh returns that
  Future so callers can await actual completion and later retries can execute.
- State getters and pure calculations are synchronous. I/O returns asynchronous
  outcomes; do not add async without an await when direct Future propagation suffices.
  VM actions await domain results and update state/effects; UI callbacks may await
  the approved action contract. Preserve native restrictions on handlers.

## Build and background ownership

- Do not notify/mutate state so the tree becomes invalid during build. Where native
  policy forbids detached provider-construction work, use the approved deferred
  lifecycle seam with lifetime/mounted checks. Post-frame is a technique, not proof
  of ownership or a universal ban on asynchronous initialization.
- Preserve loading-before-await and expected-failure handling for initial loads.
  Programmer Error behavior follows local policy, not a blanket catch-all promise.
- Detached work requires noncritical purpose, exact selected justification syntax,
  an error owner and completion/reporting policy. When categorized reasons are
  selected use `unawaited-ok: category - reason` in the installed accepted position.
  Typical selected categories include disposal, synchronous callbacks, telemetry,
  cleanup, post-frame initialization and noncritical prefetch; inspect actual syntax.
- Do not hide discarded work in microtasks, wrapper Futures, timers or ignore calls.
  A tag does not establish harmlessness; preserve consumer approval for suppressions.

## Retry and authentication

- One documented retry owner. Resolve adapter/source/repository/coordinator authority
  before moving retry behavior; never add independent loops in multiple layers.
- Classify transient errors, ordinary client rejection and authentication refresh
  separately. Do not blindly retry permanent client failures. Bound attempts/backoff,
  cancellation and idempotency according to the actual protocol, not a generic table.
- Verify serialized refresh, expired credentials and failure recovery. A status-code
  lexical check does not prove one refresh or safe replay of a nonrepeatable write.
- Search debounce duration is product-selected. Test rapid typing, clear/dispose and
  stale responses with controlled time; do not couple state owners to copy a sample.

Test timeout/permanent rejection, double taps, stale responses, concurrent refresh,
retry cancellation, navigation before acceptance and post-disposal completion.
