# Authorized deployment and recovery checks

For deployment/recovery of migrations, functions and production changes, not every
local handler edit. Read affected technical topics. Complete production audits cover
all adopted services; scoped releases still retain every applicable readiness check.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Production](production.md), [hardening](hardening.md), [monitoring](monitoring.md) |
| Database access | [RLS](rls.md), [database tests](database-tests.md) |
| Schema or policy change | [Migrations](migrations.md), [local development](local-development.md) |
| Edge Function change | [Design](edge-design.md), [auth](edge-auth.md), [tests](edge-tests.md) |

## Authority and validation

Use the existing native owner-approved deployment mechanism; no parallel pipeline,
branch policy, credential flow or wrapper is introduced here. An Actions-only
project must deploy solely through its approved Actions from authorized merged
commits: no manual remote db push, function deploy, secrets, link, config, repair or
pull fallback. Missing CI credentials mean local validation/reporting, not permission
to deploy manually. A guide never authorizes remote effects or credential changes.

Validate migration reset, SQL lint, DB/RLS tests and applicable Deno tests/format
before deployment. All required failures or missing checks block closure and
commit/push. No best-effort smoke command can mask a mandatory test failure.
Use separate staging/production projects and per-environment service secrets;
store approved credentials in the host secret store, never source/logs.

Test staging before production; check authorized role/tenant operations, function
authentication/CORS/errors and expected schema behavior. Ensure backups/PITR and
a documented forward-fix/recovery plan. Production deployment requires the host's
approval boundary, not a generic branch name or a template's push trigger.

## Function release

Function code is version-controlled and released by the approved mechanism, not
manually copied into a dashboard. Verify intended gateway/handler auth configuration
as a pair; do not disable JWT verification merely to resolve a 401. Review secret
availability, per-function configuration, restricted CORS and passing tests/format.
Use real client/token success and failure smoke checks in the authorized environment.
Do not deploy untested changes or seed real production with development fixtures.

## Recovery and closeout

Do not edit deployed migrations. Reversal is a reviewed forward migration with data
loss/compatibility assessment; incidents may need PITR into an isolated clone and
then a forward fix. Function rollback redeploys the approved prior code through the
same mechanism without discarding unrelated Git work. No implicit checkout/reset.
Monitor errors, latency, resources and authorization after deployment; retain actual
smoke results and alert/recovery ownership. Report drift/mismatch to the owner rather
than automatically repairing history. Maintain rollback and on-call documentation.

Where a product already accepts operations durably offline, preserve that acceptance
boundary. Queued local persistence is not remote business confirmation; keep pending
state/tombstones until backend acknowledgment and do not reject accepted local work
merely because remote confirmation is unavailable. Do not extend offline behavior
to online-only features without an explicit product decision.

Factory handles publication. Manual scoped commit/push occurs only after validated
completion on the agreed branch; PR default does not mandate another branch or PR
where the owner integration mechanism already exists. Release/merge/protection
bypass or additional publication is not implied by manual closeout permission.
[Official migration deployment](https://supabase.com/docs/guides/deployment/database-migrations).
