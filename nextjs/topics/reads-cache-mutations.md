# Reads, cache, mutations and Proxy

Applies to reads/streaming, rendering/runtime, mutation surfaces and invalidation.
Required: [architecture](architecture.md), [boundaries](boundaries.md),
[server security](server-security.md), [quality](quality.md); runtime integrations
also require [conditional integrations](integrations.md).

## Adopted cache model

Keep `cacheComponents` disabled in this adopted model. Use `fetch`/`unstable_cache`
with explicit revalidation and invalidation; this is a conscious model choice,
not a statement that newer cache features are unsupported. Do not switch models
without a new explicit decision. Review when the relevant framework model changes.

Every business read must explicitly choose `no-store` or caching with `revalidate`
and `tags`; do not rely on implicit defaults. Authenticated/multi-tenant sensitive
reads are dynamic (`no-store`) by default. Cache only stable, shared, nonsensitive
data unless there is an explicit safe strategy. Never cache session/tenant data
casually or mix tagged reads with mutations that omit invalidation.

Classify each read as public/sensitive and blocking/nonblocking. Business data is
server-first; keep secrets out of the browser. Start independent promises and
resolve with `Promise.all` where applicable; do not parallelize dependent operations
or create avoidable waterfalls. Record the chosen read strategy in code or scoped
change evidence. Use `Suspense`/segment loading for perceptible
uncached latency, respecting [fallback ownership](fallbacks.md). Read-only fetching
does not decide mutation or endpoint authorization; apply the companions above.

## Surfaces and security

Internal UI mutation → Server Action. Third-party/integration/webhook/external HTTP
contract → Route Handler. Do not convert everything to a Route Handler for convenience.
Server Actions validate input, authenticate user/context and authorize the operation.
Route Handlers validate input and verify the caller appropriate to the contract
(user/service/signature/token), with authorization and ownership where applicable.
Neither a Server Action nor being behind UI establishes security.

## Tags and invalidation

Adopt these minimum tag forms:
- `entity:<name>`
- `entity:<name>:<id>`
- `entity:<name>:scope:<scope>`

Choose the simplest specific maintainable form. Scope values must be stable and
predictable, with consistent semantics/format across features. Avoid complex
taxonomies without a real need; explicitly justify additional variants.

Invalidate after mutation, tag-first. In the documented Next.js 16 API,
`revalidateTag` takes a tag and profile; do not prescribe the deprecated single-arg
form. The adopted default profile is `max` for stale-while-revalidate. External
webhook/Route Handler immediate expiry uses the explicit zero-expiry option;
Server Actions needing immediate consistency for the caller prefer `updateTag`.
Verify signatures against the actual installed version rather than guessing APIs.
`revalidatePath` is a distinct path/layout invalidation operation, not a fallback
for a failed tag operation; use it only for clearly route/view-specific impact.

Before implementing, declare read strategy, internal UI versus external HTTP
surface, tags, required immediate versus eventual refresh and post-mutation
invalidation. Preserve validation, caller identity/authz/ownership and tenant scope.
Functional evidence must show the expected refresh, not merely a successful build.

## Proxy in Next.js 16

Use Proxy only for lightweight technical rewrite/redirect/path normalization or
preliminary filters. No domain logic/data access or substitution for auth/authz.
Real input validation, identity and authorization remain in Actions/Handlers.
If touched, require a bounded explicit matcher (not the entire app by default),
reproducible manual/automated behavior verification and lint/typecheck/build.
Framework naming does not prove the adapter supports a feature/runtime combination;
check the installed target and [runtime constraints](integrations.md).

## Assets and metadata

Use `next/image`; ordinary image elements require justified exceptions. Restrict
external origins with a strict `images.remotePatterns` allowlist. Use App Router
Metadata API (`metadata`/`generateMetadata`), not ad-hoc manual head markup except
specific framework-supported cases. Product/public-surface SEO/OG policy remains
local; do not invent special marketing work as part of a private application task.
