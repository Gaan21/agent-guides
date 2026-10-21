# Measured performance

Dependencies: [architecture](architecture.md), [services/data](services-data.md).
Preserve behavior/security before pursuing speed.

## Queries and lookups

- Profile the bottleneck and establish time/memory/query baseline before optimizing.
  Verify it is a performance problem, not a logic defect.
- Load predictable related data before processing loops; avoid query-per-item N+1.
  Batch IDs/aggregates and deliberately load relationships. Provider translation
  and documented bounded exceptions can constrain batching; do not assume every
  aggregate can be translated into one efficient query.
- Use Dictionary for repeated unique-key lookups, HashSet for existence/duplicates,
  SortedDictionary for ordered lookup. Small non-hot lists may use readable LINQ;
  avoid repeated linear Any/Contains scans in large loops. Keep duplicate-tracking
  sets synchronized with the result collection.
- Read-only EF queries use AsNoTracking. Preserve cancellation and materialization.
- Reduce allocations in measured hot paths: StringBuilder with appropriate capacity
  or string.Join rather than repeated concatenation. LINQ remains appropriate in
  non-critical code; never trade clarity for unmeasured microoptimization.

## Cache conditions

- Request-local caches suit repeatedly read data stable for that request. Keep them
  non-static and respect concurrency; request scope is not proof that work is serial.
- Shared IMemoryCache suits expensive, frequent reads of rarely changing data with
  predictable lifetime. Define invalidation/expiration and account for memory pressure.
  Thread-safe cache operations do not make cached mutable objects safe to share.
- Distributed cache is for an actual multi-instance consistency/cost requirement;
  consider serialization, network latency and infrastructure cost. Do not introduce
  it merely because it appears in a sample.
- Authorization-sensitive cache keys/content require security review; preserve the
  service's DTO/outcome contract rather than returning raw persistence Models.

## Verification

Measure after the change against the baseline; preserve readability, explain the
optimization, add regression checks and document architectural decisions in an ADR.
Monitor meaningful latency percentiles, query counts, allocation and GC behavior;
use project-approved targets, not sample benchmark results as universal SLOs.
Profilers, query tracing, microbenchmarks and telemetry are optional host-selected
tools, not automatic dependencies/configuration or commands mandated by this bundle.
