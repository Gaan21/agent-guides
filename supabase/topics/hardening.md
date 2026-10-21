# Hardening and incident response

For production/security work. Apply controls to the adopted services under review;
a complete production audit includes all of them, not just changed code.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Readiness](production.md) |
| Database access | [RLS](rls.md), [architecture](architecture.md) |
| Edge Function change | [Edge auth](edge-auth.md) |
| Deployment | [Deployment](deployment.md) |

## Security obligations

Keep RLS on exposed data; disable unused Data API or deliberately restrict exposure
to the API schema. Use minimum dashboard/database roles, MFA and SSO where available,
appropriate network restrictions and enforced TLS. Keys are segregated per service
and environment, with controlled rotation/revocation and no client secret exposure.
Prefer asymmetric signing where supported; coordinate verifier caches/token expiry.

Keep sensitive data out of logs; use approved application-level encryption where
required. Authorization must use trusted claims/state, not mutable user metadata.
Public Storage is for intentionally public assets, never sensitive/PHI data.
Sensitive regulated workloads require explicit approved service eligibility and
legal/security review before placing data in any function, bucket or integration.
Do not infer that every service supports the project's agreement from generic docs.

Verify backups/PITR, appropriate retention and isolated restore tests, with RTO/RPO,
owners and critical-change backups. Review advisors, resource/backup alerts and
connection/slow-query state; minimum incident contacts must be documented.

## Authorized incident playbooks

- Exposed secret: follow the approved revoke/rotate plan, update affected services
  and verify recovery. Legacy JWT signing-secret incidents need token/signing-key
  consequences reviewed, not an automatic unrelated client migration.
- Suspected unauthorized access: preserve relevant private evidence, escalate and
  use owner-authorized containment (API restriction, key revocation or applicable
  network blocking). RLS still protects rows; network controls have service scope.
- Exposed table without RLS: treat containment as urgent, but execute only through
  the approved incident mechanism. Restore RLS/minimum policies or close exposure
  as authorized; do not unilaterally move schemas or rewrite production data.
- Failed backups/PITR: escalate, obtain approved backup/remediation and re-test
  restore in isolation; do not silently proceed with an unprotected deployment.
- Connection exhaustion: assess pools/long queries and approved capacity tuning;
  short-lived direct DB invocations may need transaction pooling. No indiscriminate
  session termination or volume/process cleanup from a troubleshooting example.

Rollback remains forward-only migration/recovery or approved function redeploy.
Record actual actions, authorization, checks and residual risk; guide text does not
grant emergency credentials or permission to bypass the native deployment mechanism.
[Official security](https://supabase.com/docs/guides/security),
[backups](https://supabase.com/docs/guides/platform/backups).
