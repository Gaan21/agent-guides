# Architecture, connections and exposure

Applies to environment, key, connection, API and RPC decisions.

## Required dependencies

| Condition | Required topics |
| --- | --- |
| Database access | [RLS](rls.md) |
| Schema or policy change | [Schema](schema.md), [RLS](rls.md), [migrations](migrations.md) |

## Boundaries and keys

Postgres owns durable data, constraints, transactions and RLS. Auth issues user
tokens; the Data API exposes database access subject to grants and RLS. Storage
needs object policies; Realtime subscriptions need deliberate table/event scope.
Edge Functions provide request logic, not durable in-memory state.

Use publishable keys in clients and separate secret keys per backend service and
environment. Never put secret/service-role keys in clients, source or logs. Record
service ownership for selective rotation/revocation. API keys and user JWTs have
different purposes: use the API key header for API keys, Authorization for the user
token. Do not mistake possession of a publishable key for an authenticated user.
Prefer asymmetric signing and verified JWKS where supported; validate issuer,
audience, signature and expiry as applicable. Rotation requires an explicit overlap
and revocation plan accounting for token lifetime and verifier caches, not a fixed
wait guessed from documentation. Existing legacy keys need an owner-approved
migration; selecting this guidance does not rotate or disable them.

## Connections

Choose direct or session pooling for persistent clients; use transaction pooling
for short-lived serverless database connections and disable unsupported prepared
statements in that mode. Check installed driver/platform capabilities, IPv4/IPv6
and current pooler documentation. SDK Data API requests do not open a client-side
Postgres pool. Bound application pools and batch concurrency without exhausting
connections reserved for Auth, Storage and the API. Monitor active/idle sessions.

## Exposure and RPC

Disable an unused Data API. In this bundle's adopted convention expose only a
dedicated `api` schema and keep implementation/sensitive objects non-exposed.
Apply this convention through authorized migrations/configuration, not an implicit
move of an existing product schema. Grant schema usage and object privileges only
to intended roles; remove unnecessary exposed schemas/search paths.

Use queries with RLS for simple CRUD; use RPC for business validation, aggregates
or atomic operations, not redundant SELECT wrappers. Invoker is the default;
definer requires justified privilege elevation, a non-exposed schema, controlled
ownership, explicit minimum execution grants and a hardened search path.
Client-facing views must respect underlying RLS (security-invoker where supported).
Pre-request hooks can add API checks/quotas but do not protect unrelated services.

Keep local, staging/preview and production environments separate, with distinct
keys and non-sensitive fixtures. Record connection/exposure decisions, owners,
rotation and backup/recovery plans. Never infer operational authority from a recipe.

[Official keys](https://supabase.com/docs/guides/api/api-keys),
[connections](https://supabase.com/docs/guides/database/connecting-to-postgres),
[JWTs](https://supabase.com/docs/guides/auth/jwts),
[Data API hardening](https://supabase.com/docs/guides/api/hardening-data-api).
