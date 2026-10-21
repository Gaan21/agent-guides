# Isolated local development

For local database migration/testing setup. Use the existing owner workflow and
isolated synthetic-data stacks, never production as a test environment. An isolated
handler unit test does not require starting or resetting an unrelated database.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Database tests](database-tests.md) |
| Schema or policy change | [Migrations](migrations.md) |
| Edge Function change | [Edge tests](edge-tests.md) |

## Local environment obligations

- Verify approved CLI/runtime versions and an available Docker engine before
  starting the local stack. Guidance is not installation, login or hook permission.
- Confirm project, working directory, ports, data ownership and reset scope before
  local start/reset. Do not touch another project's stack or existing developer data.
- Local reset reconstructs migrations and seeds and destroys local test state;
  apply it only to the approved disposable stack. A migration-up check can supplement
  but not replace the required clean-reset check.
- Use local status/logs, migration history and local diff for diagnosis. Local Studio
  is an authoring aid; persist its changes in reviewed migrations and reset to verify.
- Dashboard/MCP are secondary inspection/observability only; even read-only remote
  inspection requires task relevance and authorized access. No schema writes there.
- For occupied ports identify the owning process; use its approved shutdown or
  owner-approved alternate ports. Do not prescribe kill -9 or delete volumes/global
  compose resources. Orphan cleanup requires exact scope and data-loss authorization.
- Preserve full command status/output when a migration fails. Piping output through
  head or swallowing failures cannot establish successful reset/lint/tests.
- Keep migration source and local fixtures versioned after successful validation.
  Do not infer authority to mark remote history applied because a pull found no diff.
- If auth or local services fail, stop blind retries, report facts and consult the
  host/owner recovery mechanism. Missing required tools block validated completion.

Completion: intended Docker/CLI stack available, new versioned idempotent migration,
successful clean local reset, applicable lint/tests and reviewed state/diff.
[Official local development](https://supabase.com/docs/guides/local-development).
