# Database and API performance

For latency/throughput work; measurement does not authorize production effects.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Architecture](architecture.md), [monitoring](monitoring.md) |
| Database access | [RLS performance](rls-performance.md) |

## Performance obligations

- Index foreign keys and policy/filter/order columns; consider composite or partial
  indexes for actual access patterns (active/non-deleted/public rows). Measure use,
  selectivity, write cost and size rather than indiscriminately adding indexes.
- Use EXPLAIN (ANALYZE, BUFFERS) on representative critical queries with intended
  roles and safe data. ANALYZE executes statements; do not run destructive diagnosis
  against live data. Compare latency with project objectives, not universal numbers.
- Use explicit actor/tenant filters, minimal projection and pagination on lists.
  Choose cursor or bounded range/offset deliberately; avoid N+1 and unindexed sorts.
  Do not SELECT * on large tables or use RLS as the only query-planning filter.
- Exact counts can be expensive: request them only when needed. Consider transport
  compression/proxy caching where applicable, without leaking sensitive responses.
- Public content may use CDN/cache headers. Private caching needs per-user/tenant
  isolation, controlled keys and invalidation/TTL; never let shared caches expose
  sensitive data. A short TTL alone is not access control.
- Rate limits belong in the approved gateway/hook/function design, with concurrency,
  anonymous identity, retention, transaction behavior and failure semantics reviewed.
  Return 429/retry guidance. Do not import an unhardened public definer hook.
- Bound pools for the actual client mode; persistent direct/session connections
  differ from short-lived transaction mode. Disable unsupported prepared statements
  and reserve capacity for Auth/Storage/API. Inspect idle/long-running sessions.
- Review pg_stat_statements, table growth and planner statistics. Routine vacuum/
  analyze relies on configured maintenance; heavy maintenance such as VACUUM FULL
  needs explicit lock/disk/data-availability planning and approved windows.
- Keep triggers lightweight. Enable Realtime only on needed tables/events with
  filters and permissions; disable unnecessary event publication deliberately.

Completion: measured critical plans, relevant indexes, scoped projections/filters,
pagination, safe cache/quotas and correct pools. Re-run auth tests after changes.
[Official performance](https://supabase.com/docs/guides/database/query-optimization),
[PostgreSQL EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html).
