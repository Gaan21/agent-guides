# Multitenancy

Applies to company/workspace/team isolation in database work.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Schema](schema.md), [RLS](rls.md), [patterns](rls-patterns.md), [database tests](database-tests.md) |

## Isolation obligations

- Put indexed tenant scope on each multi-tenant table. Define membership and
  owner/admin/member capabilities explicitly; membership tables also need protected
  grants and RLS, not self-editable privilege fields.
- Policies must enforce tenant membership for reads and writes. Validate both actor
  and destination tenant on inserts/updates; actor ownership alone cannot establish
  that a row belongs to the actor's tenant. Test attempted tenant reassignment.
- Avoid uncontrolled cross-tenant joins. Prefer simple membership subqueries;
  elevated helpers are exceptional and must satisfy definer hardening, not bypass
  isolation merely to avoid a JOIN or recursion.
- Tenant administration is scoped to the target tenant and permitted capability,
  never a global role inferred from client payloads. Revoke default helper execution
  and grant only intended roles; test the helper as well as each consuming policy.
- Seeds/migrations must not mix sensitive tenant data or hardcode production tenant
  IDs. Use synthetic per-environment fixtures and controlled selections.
- RLS provides logical isolation. Where hard isolation is required, assess separate
  projects per tenant; record operational/security consequences rather than claim
  network restrictions alone isolate Data API tenant rows.
- Use composite indexes for frequent tenant/order access paths when measured useful.
  Test two distinct tenants and their users in local/CI smoke coverage, including
  positive/negative SELECT/INSERT/UPDATE/DELETE and administrator boundaries.

Completion requires an isolation choice, indexed scope, protected membership,
per-operation policies and passing negative cross-tenant tests.
[Official RLS](https://supabase.com/docs/guides/database/postgres/row-level-security).
