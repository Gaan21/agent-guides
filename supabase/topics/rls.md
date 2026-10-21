# RLS fundamentals and privilege safety

Required before implementing authorization policies or changing database access
that depends on them; not required for an existing no-DB webhook validation edit.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Patterns](rls-patterns.md), [tests](database-tests.md) |
| Schema or policy change | [Migrations](migrations.md) |
| Performance diagnosis | [RLS performance](rls-performance.md) |

## Enforcement

Enable RLS explicitly in migrations on every exposed table, including public
lookup tables; intentional public reads still need an explicit justified policy.
Do not rely on Studio creation defaults or changes not retained in version control.
With RLS enabled and no applicable policies, ordinary API roles are denied rows;
table/schema privileges remain a separate prerequisite. Owners, elevated roles and
definer execution have different bypass semantics and must be reviewed separately.

Specify intended roles explicitly. `anon` and `authenticated` represent request
database roles, not equivalent trust levels. A secret/service-role backend can
bypass RLS; do not use it to make user tests succeed. Validate real user tokens.

USING controls visible existing rows for SELECT/UPDATE/DELETE; WITH CHECK validates
new rows for INSERT/UPDATE. Updates need both existing-row and replacement-row
authorization, and appropriate read access. Test every allowed operation; an absent
write policy can intentionally forbid that operation.

Permissive policies combine with OR. Restrictive policies constrain applicable
permissive access with AND; they do not independently grant access. Review combined
policies, not just each predicate in isolation.

Use authenticated identity (`auth.uid()`) and trusted authorization claims. Never
authorize using user-editable user_metadata, including verification flags. Trusted
app_metadata is server-managed but JWT claims can become stale until token refresh;
revocation-sensitive decisions may need current protected backend state.
Use `(SELECT auth.uid())` in new policies; index authorization columns.

## Helpers and exposure

Prefer SECURITY INVOKER. SECURITY DEFINER requires a justified privileged operation,
non-exposed helper schema, qualified object names and a restricted search_path
(for example empty with fully qualified references). Prevent untrusted schema/object
resolution, revoke default PUBLIC execution and grant the minimum intended roles.
Review function owner privileges, schema usage and all callers; private placement
alone is not authorization. Do not automatically elevate complex policies.

## Verification and diagnosis

Simulate roles/claims within local transactional tests, then verify applicable real
client/JWT paths. Roll back fixtures. Diagnose grants, schema exposure, token
identity/expiry and intended policies separately. A filtered SELECT normally yields
no rows, not an authorization exception. Do not “fix” permission errors by adding
USING(true), disabling RLS or granting broad privileges. If an unauthorized remote
change occurred, stop and use the owner's drift-reconciliation process; a guide
does not authorize pull/repair/deploy or an immediate unvalidated commit.

Completion: explicit enablement, justified policies/roles for applicable operations,
indexed predicates, minimum grants and passing positive/negative tests.
[Official RLS](https://supabase.com/docs/guides/database/postgres/row-level-security),
[function safety](https://www.postgresql.org/docs/current/sql-createfunction.html).
