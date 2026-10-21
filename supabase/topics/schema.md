# Schema design

For new/refactored tables, not unrelated Edge-only changes.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Architecture](architecture.md), [RLS](rls.md), [migrations](migrations.md) |
| Multitenancy | [Tenants](tenants.md) |

## Schema obligations

- Adopt plural snake_case tables and consistent snake_case columns. Use UUID
  primary/foreign keys, generated UUID defaults and `timestamptz` for real instants.
  Mobile/offline identifiers must not depend on an online sequence allocation.
- Store actual UTC instants, not a device-local civil value relabeled UTC. Product
  timezone/reporting rules remain local authority; civil dates are not instants.
- Include created/updated timestamps; defaults alone do not maintain updated_at.
  Optional actor audit fields reference authenticated identities. Use tombstones
  where the adopted synchronization/deletion contract requires them.
- Define explicit foreign keys, indexes and deletion behavior (CASCADE/RESTRICT as
  appropriate); index policy, frequent join/filter/order columns. Include owner or
  tenant scope at design time. Public visibility must be explicit, not accidental.
- Enforce required/nonempty values, uniqueness and domain constraints in the DB.
  Use CHECK for small domains or stable enums deliberately; use case-insensitive
  text support only where needed. Bound JSONB metadata; do not hide the whole model
  in unstructured JSON. Monetary values need deliberate exact precision/currency;
  do not use floating point for money or assume locale-dependent money types fit.
- Never use user-mutable metadata as authorization authority. Trusted app claims
  are authorization inputs, not a safe place for arbitrary sensitive information.
- Exposed tables require RLS and tested operation-specific policies. Private tables
  require minimum grants too. Do not mistake adding an owner column for enforcement.
- Expose only the intended API shape. Invoker views/functions are preferred;
  elevated helpers need the [RLS hardening](rls.md) controls.

Before completion verify keys/timestamps, constraints/FKs/indexes, tenant ownership,
RLS/grants, API/view exposure and new immutable migration with applicable tests.
Do not edit an applied migration to repair a schema mistake.

[PostgreSQL types](https://www.postgresql.org/docs/current/datatype.html),
[constraints](https://www.postgresql.org/docs/current/ddl-constraints.html).
