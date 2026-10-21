# Edge authentication and authorization

For authentication/authorization of every new or changed function, including a
no-DB webhook. Database privileges and Storage policies apply when those services
are used; an auth check alone never grants administrative intent.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Edge design](edge-design.md), [tests](edge-tests.md) |
| Database access | [Architecture](architecture.md), [RLS](rls.md) |
| Schema or policy change | [Migrations](migrations.md), [database tests](database-tests.md) |
| Deployment | [Deployment](deployment.md) |

## Authentication obligations

Define each endpoint's caller and trust boundary before implementation. User-facing
requests require a verified user identity and backend tenant/capability checks.
Forwarding an Authorization header or decoding claims is not JWT verification.
Use supported verification with correct signature, issuer, audience and expiry, or
the appropriate trusted Auth server verification flow. Keep user and admin clients
separate; never accept a caller-provided actor ID as independently authenticated.

Gateway JWT verification and handler authentication are complementary configuration
choices. Review the actual installed platform/key compatibility. If a project's
approved pattern disables gateway verification, explicit handler authentication is
mandatory before protected effects. Never publish a blanket disablement as a 401 fix
or silently replace an adopted project's manual authentication strategy.

Public/external webhooks may be exempt from *user JWT* verification, not their own
intended authenticity checks. Verify provider signatures or approved shared-secret
protocol, replay/idempotency controls and payload limits. Internal webhooks must
authenticate the internal caller. Missing/empty expected secrets must fail closed;
do not accept an empty header because configuration defaulted to an empty string.

Prefer user-context RLS for ordinary database access. Server-side secret/service-role
operations require independently authorized administrative intent, validated scope,
minimal inputs/outputs and no privilege escalation from arbitrary user data. Auth
admin metadata changes must not promote users from untrusted payloads. Storage
administration is likewise privileged, not a mandatory bypass for all uploads.

Restrict browser origins/methods/headers; preflight is not an authenticated business
operation. Include required Authorization, API key and SDK headers for intended
clients, without opening unnecessary origins. Rate-limit public endpoints via the
approved gateway/function/backend mechanism; return 429 and retry guidance where
appropriate. A simplistic transactional counter is not a reliable universal quota.

Keep private buckets protected by storage.objects policies; public buckets are only
for genuinely public assets. Validate upload MIME type/size/path/actor and expected
overwrite behavior. Never log tokens or third-party credentials. Investigate 401/403
by verification/configuration and token validity, not by turning off authorization.

[Official authentication](https://supabase.com/docs/guides/functions/auth),
[Storage security](https://supabase.com/docs/guides/storage/security/access-control).
