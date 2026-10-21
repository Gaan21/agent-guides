# RLS performance

For slow policies or large datasets. Optimization never relaxes authorization or
substitutes privileged execution for user-context measurement.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [RLS safety](rls.md), [patterns](rls-patterns.md), [tests](database-tests.md) |

## Policy performance obligations

- Index policy/ownership/tenant/membership and relevant FK/filter columns. Inspect
  the actual access path; an index's existence alone does not prove it is used.
- New policies must wrap row-independent identity lookup with SELECT auth.uid().
  Row-independent helper results may benefit from an initplan. Do not claim every
  SELECT-wrapped function caches once: correlated row arguments remain row-dependent.
  Check helper return types and array/subquery semantics before changing predicates.
- Add explicit client filters matching permitted actor/tenant scope, without
  treating them as security. Specify the intended database role in each policy.
- Prefer membership subqueries/IN or appropriate ANY expressions over unnecessary
  joins when equivalent and measured better. Large membership sets need measurement.
- Keep invoker default. A necessary definer bypass must satisfy non-exposed schema,
  qualified references, hardened search_path and minimum grants. Complexity alone
  is not justification; do not mandate moving all complex logic to definers.
- Measure EXPLAIN (ANALYZE, BUFFERS), statistics, row counts and representative
  latency under intended roles. ANALYZE executes the statement: use authorized,
  isolated fixtures, especially for writes. Sequential scans can be appropriate;
  do not force an index solely to satisfy a visual plan heuristic.
- Recheck negative authorization paths after every optimization. Record baseline,
  workload, plan and outcome against the project's performance objective. External
  benchmark numbers do not promise the same improvement or a universal latency.
- Diagnose remaining latency by index definitions, statistics, table growth,
  membership queries and connection pressure before choosing partitioning or scale.

Completion requires relevant indexes/plans, explicit role/client filters, justified
helper privileges, applicable policy tests and measured project performance targets.
[Official recommendations](https://supabase.com/docs/guides/database/postgres/row-level-security#rls-performance-recommendations).
