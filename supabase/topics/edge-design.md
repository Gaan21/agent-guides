# Edge Function design

For new/changed functions. Browser clients require CORS; Storage access requires
explicit bucket/object policies and limits. Follow only applicable dependencies;
a no-DB existing webhook change does not require SQL/migration/deployment topics.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Always | [Authentication](edge-auth.md), [tests](edge-tests.md) |
| Database access | [Architecture](architecture.md), [RLS](rls.md) |
| Schema or policy change | [Migrations](migrations.md), [database tests](database-tests.md) |
| Deployment | [Deployment](deployment.md) |

## Handler obligations

- Functions use the supported Deno/TypeScript runtime and Web APIs. Keep request
  behavior stateless and retry/idempotency-safe; durable state belongs in a database.
  Isolates may be reused: never depend on per-request clean memory for security.
- Use functions for webhooks, trusted integrations/proxies, server-side auth logic
  or bounded request processing; simple authorized CRUD usually belongs in the
  Data API. UI logic stays client-side, files in Storage, durable/long batch work
  in an approved job/queue/scheduler. Assess actual platform runtime constraints.
- Prefer cohesive functions over unnecessary fragmentation; share common validation,
  errors, logging, auth and clients in `_shared/` without duplicating business rules.
- Validate JSON types/limits and methods before effects. Return consistent JSON and
  meaningful HTTP outcomes: input 400, auth 401/403, not-found 404, method 405,
  conflict where applicable, quota 429, unexpected dependency/server failure 500.
  Handle malformed JSON separately from internal defects; avoid exposing raw errors.
- Export a request handler with injectable dependencies for deterministic tests.
  Start serving only in the entry execution path; wrap a multi-argument handler
  in a one-request lambda so runtime metadata is not mistaken for injected deps.
- Keep secrets in approved environment/secret storage, never source or logged CLI
  arguments. Fail closed on missing required values; do not substitute empty secrets.
- Use user-context clients for RLS where appropriate; admin clients are exceptional
  privileged capabilities with explicit authorization and bounded returned fields.
- Pin compatible dependencies deliberately, prefer small pure libraries and avoid
  native dependencies unsupported by the runtime. Formatting must be clean.
- Restrict CORS to intended origins, methods and required SDK headers; answer preflight
  promptly and include proper response headers on failures too. CORS is not auth.
- Log minimal structured method/path/status/duration/correlation information without
  tokens, sensitive URLs/payloads, PII or raw stacks in client responses. Optional
  external error tracking must obey the same data controls and not duplicate reports.
- Design for the project's latency objective; slow/expensive work needs bounded
  dependencies, optimized queries or an approved job/queue, not a fabricated platform
  limit. Avoid N+1 and use the appropriate database connection mode if connecting
  directly; Data API clients are not direct Postgres pools.

Do not promise global nearest-region execution, cold-start latency, fresh isolates
or fixed plan quotas. Verify version/platform limits before making such decisions.
[Official functions](https://supabase.com/docs/guides/functions),
[limits](https://supabase.com/docs/guides/functions/limits),
[Deno](https://docs.deno.com/).
