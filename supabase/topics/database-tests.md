# Database, RLS, function and trigger tests

Required for changed database behavior and before calling policies secure, not a
no-DB handler-only edit. Preserve positive and negative authorization coverage.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [RLS](rls.md), [patterns](rls-patterns.md), [local development](local-development.md) |
| Schema or policy change | [Migrations](migrations.md) |
| Deployment | [Deployment](deployment.md) |

## Test execution

Use pgTAP locally and in CI. Enable its extension in the approved test environment;
keep SQL test files separated by policy/function/trigger concern. Run the approved
database test command (commonly `supabase test db`, or an authorized pg_prove path).
This names a validation obligation, not permission to start/alter an environment.

## Required behavioral coverage

- For each policy/allowed operation test SELECT/INSERT/UPDATE/DELETE positive and
  negative actor cases: own, another actor, another tenant and anonymous as relevant.
- Cover destination-tenant/owner changes, sensitive fields, manager/admin boundaries,
  restrictive-policy conjunctions and helper function outcomes.
- Use correct role and request claims inside an isolated transaction. Create complete
  synthetic identity/membership fixtures with valid IDs and required grants/FKs.
  Differentiate ordinary-role tests from privileged fixture setup.
- Expect denied SELECTs to filter rows when that is PostgreSQL behavior; distinguish
  privilege errors from policy filtering and insert/update check violations.
- Function/trigger tests cover success and rejected inputs, effects and invariants.
  A trigger using transaction-stable now() need not produce a strictly later time
  than created_at in the same transaction. Test the actual contract deterministically.
- Assert outcomes, not only table/policy existence or a successful HTTP transport.
  Match pgTAP planned assertion count and appropriate error code/message overloads.
- Roll back fixtures; no persistent sensitive data, inter-file ordering assumptions,
  real external effects or brittle fixed current timestamps. Record special fixtures.
- Add representative role-aware performance tests/EXPLAIN where policy cost matters.

Run the full applicable DB/RLS suite before integration/deployment; staging gets
controlled smoke checks. A required unavailable or failing test blocks closure and
publication. Record actual command, environment and exit status, not `|| true`.

[Official database tests](https://supabase.com/docs/guides/local-development/testing/overview),
[pgTAP](https://pgtap.org/documentation.html).
