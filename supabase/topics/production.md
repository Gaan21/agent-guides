# Production readiness

Before first production deploy and periodic audits, cover all adopted services.
For scoped releases apply all readiness obligations relevant to affected services;
this topic is not a prerequisite for an unrelated local-only handler edit.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Hardening](hardening.md), [monitoring](monitoring.md) |
| Database access | [RLS](rls.md), [database tests](database-tests.md) |
| Schema or policy change | [Migrations](migrations.md) |
| Edge Function change | [Edge auth](edge-auth.md), [Edge tests](edge-tests.md) |
| Deployment | [Deployment](deployment.md) |

## Mandatory readiness review

- Audit exposed schemas/tables for RLS and intended per-operation policies; test
  real role boundaries. No unexplained permissive policy or public lookup exception.
  Definers belong in non-exposed schemas with minimum grants and safe resolution.
- Resolve critical Security Advisor findings. Keep secrets server-side, documented
  environment variable names, ignored secret files and distinct environment keys.
- Require TLS/SSL enforcement and appropriate network restrictions for database
  connections. Verify actual connection security; network rules never replace RLS
  and may not apply uniformly across services. Rotate default database credentials.
- Verify backups and PITR, suitable retention and an isolated restore test. Establish
  RTO/RPO and manual backup before critical changes; do not assume a purchased plan
  alone guarantees recoverability or coverage of every service's data.
- Review indexes/FKs/critical plans, actual load, pooling and headroom. Address slow
  queries and bad scans, but do not turn example hit ratios, query counts or compute
  tiers into universal scaling promises.
- Version every migration, keep published history immutable, validate idempotency,
  clean seeds and rollback. Approved CI/host checks precede staged and authorized
  production deployment; no manual remote fallback in an Actions-only project.
- Configure Auth token lifetime/refresh rotation appropriately, trusted claims,
  OAuth redirects/client secrets and signup/login abuse controls. Verify branded
  email templates, sender and production redirects where email is used.
- Review Edge auth, CORS, secrets, errors, runtime limits and unit/integration tests;
  configure approved error tracking/alerts for critical functions.
- Storage requires object policies, private-by-default buckets, file size/MIME
  controls and scoped upload access. Public assets may use image optimization/CDN;
  record old-file cleanup and retention without installing automatic jobs here.
- Define privacy/retention, user export and deletion obligations. Compliance review
  is required where relevant; select the applicable agreement/project controls with
  qualified owner/legal review, never claim HIPAA/SOC2/PCI compliance from a checklist.
- Restrict dashboard roles and database credentials; require MFA, revoke departed
  users/tokens and avoid sharing the administrator password. Document least-privilege
  team access rather than tying authority automatically to job seniority.
- Maintain schema source in migrations, permission/API shape, migration/recovery/
  on-call runbooks, client inputs/outputs, rate limits and operational ownership.
  Documentation must not become a conflicting hand-maintained schema source.

## Deployment day and ongoing review

Require recent verified backup, stable staging, understood recovery plan, alerts,
prepared smoke tests and notified on-call staff. Communicate a maintenance window
where needed. Only the authorized mechanism deploys. Verify metrics/smoke results
and monitor the initial post-release period, including the first day.
Weekly review reports/advisors/backups; monthly access/secrets/disk and restore
testing; quarterly full security/readiness/capacity review. Preserve stricter local
cadence. Missing required readiness checks block closure, not a warning-only release.

Reference-only review baseline: 2026-10-21. Plan tiers, retention windows, runtime
quotas, legal eligibility and service exclusions must be checked for the actual
project; this bundle makes no current pricing, legal or latency promises.
[Official checklist](https://supabase.com/docs/guides/platform/going-into-prod),
[HIPAA](https://supabase.com/docs/guides/security/hipaa-compliance),
[shared responsibility](https://supabase.com/docs/guides/deployment/shared-responsibility-model).
