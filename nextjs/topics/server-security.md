# Server data access, validation and authorization

Applies to queries, Actions, Route Handlers, shared server functions and tenant data.
Required: [architecture](architecture.md), [boundaries](boundaries.md),
[reads/mutations](reads-cache-mutations.md); [env](env.md) for secrets/config.

## Data access boundaries

Feature-local reads/actions may stay in `_queries`/`_actions`; shared orchestration
and domain/data rules belong in `src/server/`. Delegate when logic grows, features
reuse it or authorization/validation/ownership requires central consistency.
Expose provider-neutral domain functions, not raw SDKs throughout the tree. The
server layer is not a promise to keep a permanent provider/backend architecture.

Normalize every external RPC/SDK/API response before exposing it. `parse*` functions
produce domain types; `normalize*` maps provider errors to domain codes. Callers
must not see raw SDK structures or errors. If 2+ public functions have structurally
identical RPC flow differing only in name, extract a private internal helper. Do not
relocate provider details into UI to avoid normalization.

## Validate callable inputs

Always validate server-side at exposed entrypoints: Action FormData, params and
searchParams before business use, HTTP payloads, and DAL/server functions exposed
to upper layers/different features/external callers. Use schemas, not partial
ad-hoc parsing or client-only validation. Exclusive schemas live in `_schemas`;
shared contracts in `src/server/<domain>/schemas` or equivalent domain module.

A private internal helper may assume validated input only with an explicit internal
contract and no public boundary. Promote validation to the exposure point if it
stops being private or gains callers. Shared location is never a validation exemption.

## Caller identity, permissions and scope

Treat `route.ts` as a public HTTP surface by default; all inputs are external and
untrusted. Every Action must validate inputs, authenticate the user/session,
authorize the operation and verify tenant/ownership where applicable. Every Handler
must validate inputs, verify the caller according to its contract, authorize the
operation and verify tenant/ownership where applicable. A service/signature caller
need not be a browser session, but does need its own real identity verification.

Every multi-tenant operation runs within the correct effective tenant scope.
Validate client-supplied IDs/scopes against identity and actual permissions. Route,
layout, hidden UI, client-side filtering and preliminary Proxy checks are not authz.

## Readable safe primitives

An operation body should read at one level: verify access, get context, execute
operation, map result. Extract low-level parsing into named variables/helpers rather
than mixing inline FormData reads and domain steps. Keep steps intelligible without
opening every support function.

When primitives are always used together by all their callers, combine them in a
convenience helper at the same shared layer (`src/server/<domain>/`), not repeated
inline in each feature. Repeated guard blocks in 3+ Actions are a diagnostic signal,
not permission to duplicate a known all-callers combination until the third copy.

A safe server primitive validates, verifies identity/authz appropriate to the surface,
applies tenant/ownership scope, returns only fields needed by the caller and hides
internal/sensitive details by default. Use bounded per-use-case output DTOs, not
complete entities for convenience. These duties survive extraction/reuse.

Review invalid input, allowed/denied paths, wrong tenant, raw provider leakage,
oversized outputs and action readability. [Quality](quality.md) defines behavior
evidence; moving an operation to server code alone is not successful validation.
