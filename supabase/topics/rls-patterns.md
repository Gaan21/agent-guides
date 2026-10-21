# Authorization patterns

Choose the smallest applicable pattern; never paste an unreviewed policy template.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Fundamentals](rls.md), [tests](database-tests.md) |
| Multitenancy | [Tenant rules](tenants.md) |

## Authorization obligations

- **User-owned:** indexed identity FK; explicitly scoped authenticated policies
  for SELECT/INSERT/UPDATE/DELETE. Both USING and WITH CHECK protect updates so
  ownership cannot be reassigned to escape restrictions.
- **Team-based:** indexed team FK and protected membership relation; members read,
  permitted team capabilities create/update, and only explicitly permitted owners
  delete. Scope membership checks to the target row's team. Membership itself must
  not permit self-promotion or grant recursive unrestricted access.
- **Role-based:** use server-managed authorization claims or protected role state,
  not mutable user metadata. Role-changing admin operations are backend-only and
  require independent authorization. Append-only audit data may intentionally
  permit reads/inserts while having no update/delete policy.
- **Public/private:** explicit visibility flag plus own-row access; public in a
  pattern may mean authenticated visibility, not anonymous access. Make that choice
  explicit. Users may change only their own allowed fields; indexes support filters.
- **Parent-child:** child visibility/creation depends on authorized parent access
  and the creating actor. Index parent FKs; validate parent scope as well as child
  ownership. Do not let joins expose an inaccessible parent or another tenant.
- **Expiring sharing:** bind an unguessable token to the intended resource and
  expiry; protect token storage and specify trusted token transport/validation.
  Do not assume a client can set arbitrary request database settings. Sharing is
  additive only within the deliberate policy and must not expose all token rows.
- **Multitenant:** apply [tenant rules](tenants.md), including destination tenant
  validation and scoped capability checks. Product-specific company schemas and
  roles remain local contracts, not universal patterns.

Combine policies deliberately; test interactions and role boundaries. Client-side
filters improve planning only. Avoid unnecessary joins, but preserve authorization
meaning when optimizing; use a hardened definer only for justified privilege needs.
Complete CRUD positive/negative tests, indexes, role declarations and measured
query plans before considering a selected pattern complete.
[Official RLS](https://supabase.com/docs/guides/database/postgres/row-level-security).
