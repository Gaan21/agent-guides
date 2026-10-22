# Migrations and data changes

For database schema/functions/triggers/policies. Consumers escalate structural work
to the backend owner. Local authoring does not itself authorize a deployment.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Every migration | [Local development](local-development.md), [tests](database-tests.md) |
| Table/type/relationship or structural schema changes | [Schema](schema.md) |
| Policies, permissions, grants, tenant boundaries, security functions or exposed schema changes | [RLS](rls.md) |
| Deployment | [Deployment](deployment.md) |

Read only matching dependencies: a comment-only migration does not require schema
design or RLS detail. This never exempts migration validation or the entry's
always-on security rules; inspect the diff before declaring a topic unaffected.

## Invariants

CLI-managed, version-controlled migrations are the schema source of truth. No
ad-hoc remote Dashboard/SQL Editor/MCP changes. Published migrations are immutable;
fixes and rollback use new forward migrations. Keep descriptive timestamped names,
group related changes and explain non-obvious SQL. Do not enforce task/line caps.

Migrations must be deliberately idempotent: protect table/column/index existence,
and handle policy/trigger creation too. IF NOT EXISTS alone can conceal an object
whose definition is wrong; verify the intended resulting state. Scope catalog
existence checks by schema, table and object name, not a globally ambiguous name.
Order dependencies: schema, indexes, RLS/policies/grants, then optional controlled
reference/seed data. Keep every intermediate exposed state safe.

## Local authoring

Create a new migration and write/review SQL. Local Studio changes may be captured
with a local diff; review the generated migration and add missing RLS, grants,
indexes and constraints. Test rebuilding from zero with local reset and seeds;
applying only a new migration does not prove clean reconstruction works.
Run local SQL/plpgsql lint with no new errors and the DB/RLS/function tests.
Check actual schema/diff and existing-data upgrade behavior, not only empty fixtures.

No sensitive or environment-specific data in migrations/seeds. Use synthetic seeds,
explicit conflict handling and protected reference-data inserts. An ON CONFLICT
clause needs a meaningful uniqueness constraint; it does not make arbitrary seeds
safe or production-appropriate. Hardcoded production UUIDs are not fixture design.

## Data movement and locks

Use short transactions and controlled batches for large changes. PostgreSQL UPDATE
does not accept a direct LIMIT: select a bounded deterministic set of keys, update
those rows and track progress without overwriting batch-size control. Design for
restart, concurrency, lock duration and partial failure; validate completion.
Avoid long blocking ALTERs. Large index creation may use CONCURRENTLY only outside
transaction blocks; review migration-runner behavior and failure cleanup first.

For incompatible type/name changes use expand/backfill/switch/contract steps with
client compatibility and validation between stages. A shadow-column rename is not
permission to drop old data before all consumers migrate. Reversal may lose data;
document backup/restore and forward-fix plans before destructive work.

## Drift and failures

Inspect approved history/state before creating migrations. Remote drift or history
mismatch requires owner-authorized reconciliation, not automatic remote-wins,
pull/repair/relink or editing an applied migration. A failed test blocks closure.
Investigate grants/ownership accurately; policies do not have an independently
transferable owner via ALTER POLICY OWNER. Ownership repair needs approved scope.
Authentication/circuit-breaker failures require stopping uncontrolled retries and
following the host's recovery procedure, not a scripted credential reset.

Before production: local reset/lint/tests pass, RLS/grants/indexes reviewed, no
sensitive seeds, staging verified, recent backup and a documented rollback plan.
[Official migrations](https://supabase.com/docs/guides/deployment/database-migrations),
[PostgreSQL ALTER POLICY](https://www.postgresql.org/docs/current/sql-alterpolicy.html).
