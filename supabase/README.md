# Supabase

Read this entry for Supabase work; select relevant detail below and reuse it while
in context. Selection does not relax applicable security or validation obligations.
This independently selectable bundle supplies guidance, not executable tooling.

## Always applicable

- Keep RLS enabled on exposed tables; authorize actor, tenant and capability in
  the backend. Client filters never replace authorization. Keep secrets server-side.
- Version schema, policies, functions and triggers through immutable published
  migrations. Never make ad-hoc remote schema changes or bypass auth for tests.
- Identify the backend owner: a consumer must escalate structural changes rather
  than execute the owner's workflow. Local product contracts remain authoritative.
- Factory mechanisms own tools, branches, checks and publication; do not duplicate
  them. In manual mode respect the agreed branch; scoped commit/push follows
  validated completion without another prompt. PR is the integration default, not
  permission to leave an agreed branch or bypass protections.
- Missing/failing mandatory checks block closure, commit and push. Report actual
  results and use the owner/host blocked-work mechanism. Deployment, credentials,
  remote writes and releases require their own authorized mechanism.

## Read by task

| Work | Required local detail |
| --- | --- |
| Connections, keys, exposure or RPC choice | [Architecture](topics/architecture.md) |
| Tables/types/relationships | [Schema](topics/schema.md); add [tenants](topics/tenants.md) for multitenancy |
| Policies or permissions | [RLS](topics/rls.md), [patterns](topics/rls-patterns.md), [tests](topics/database-tests.md); add [RLS performance](topics/rls-performance.md) when tuning |
| Migrations or local backend | [Migrations](topics/migrations.md), [local development](topics/local-development.md); include affected schema/RLS topics |
| Edge Functions | [Edge design](topics/edge-design.md), [authentication](topics/edge-auth.md), [tests](topics/edge-tests.md) |
| Slow queries/API, caching | [Performance](topics/performance.md), RLS performance when policies contribute |
| Deployment/production/audit | [Deployment](topics/deployment.md), [readiness](topics/production.md), [hardening](topics/hardening.md), [monitoring](topics/monitoring.md) |

Follow topic dependencies only for conditions that apply to the affected work.
"Deployment" means deployment/recovery work, not every local function edit; complete
production audits include all adopted services. No-DB webhook edits retain auth and
negative tests without unrelated SQL/migration/deploy reads. No blanket all-topic/
per-patch reading or automatic cross-bundle activation.
See [inventory](inventory.md) and [notice](NOTICE.md); [license](LICENSE).
