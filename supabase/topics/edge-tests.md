# Edge Function validation

For every new/changed function. Tests cover actual affected interfaces, not
unrelated SQL or deployment work. No applicable authentication test is optional.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Design](edge-design.md), [authentication](edge-auth.md) |
| Database access | [RLS](rls.md), [database tests](database-tests.md) |
| Schema or policy change | [Migrations](migrations.md) |
| Deployment | [Deployment](deployment.md) |

## Validation obligations

Unit tests with injectable authentication, RPC, mail and other dependencies are
mandatory. Keep an isolated handler test beside each function; mock real external
services. Unit tests do not require a running stack, but they do not replace required
integration coverage of actual authentication and affected interfaces. Keep
required authentication integration coverage even for a no-DB webhook;
database paths also require local DB/RLS integration coverage.

Required cases include auth failure (401/403), invalid/unsupported operation,
invalid JSON (400), method rejection (405), dependency/RPC exceptions mapped to the
right status, business rejection mapping, and success with correct payload and
server-derived actor. Assert behavior rather than merely fetching a URL.

Integration tests use real test JWTs from an approved Auth fixture/sign-in flow,
not an assumed CLI auth command or production tokens. Test absent/expired/invalid
tokens or incorrect webhook secrets, CORS/preflight, intended user RLS, and restricted
admin pathways. Build controlled synthetic seeds and known local state; reset only
the approved disposable environment. No sensitive fixtures or unapproved real effects.

Run the applicable Deno unit/integration tests and verify clean formatting before
commit/deploy. Use the host-approved permission profile; broad Deno permissions in
an example are not a grant. Capture actual command/exit status; unavailable/failing
required tests block closure/commit/push. CI must run applicable DB and Edge tests
before deploy; staging smoke complements, not replaces, those tests.

Keep the test pyramid deliberate: SQL/RLS/function tests at the base, handler unit
and local integration coverage next, minimal login/key-operation smoke at the top.
Full applicable suite at integration. Preserve smoke/E2E and short performance checks;
execution follows the expressly approved factory mechanism or manual request, with
isolation. This guidance defines no CI calendar. These checks do not substitute for
mandatory validation. Review final per-function auth config,
inputs, statuses, actor propagation, private logs, tests and formatting together.
[Official tests](https://supabase.com/docs/guides/functions/unit-test).
