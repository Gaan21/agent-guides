# Segment loading, errors and not found

Applies to loading/error/not-found/recovery UI. Required:
[architecture](architecture.md), [boundaries](boundaries.md),
[server security](server-security.md), [reads/mutations](reads-cache-mutations.md),
[quality](quality.md). Fallbacks never replace server validation or authorization.

Use `loading.tsx` where initial segment data has perceptible latency and a stable
fallback helps. Keep it simple/consistent with no business logic. Do not replace
segment loading with scattered global spinners or duplicate local+segment loading
for the same initial read. Submit/button/local-transition spinners remain valid
for user interactions, not as substitutes for initial server-data loading.

Expected validation/business errors belong in normal feature/Action/domain-result
flow with contextual actionable messages. Unexpected render/data exceptions propagate
to the segment error boundary or a higher fallback. Do not route normal business
validation/authz to `error.tsx`.

Segment `error.tsx` handles unexpected failures in its applicable subtree, not
automatically the whole application. Provide a usable nonsensitive message,
retry/reset when meaningful and safe navigation if recovery fails. No sensitive
exception details or permission logic substituting for server checks.

## Adopted visibility convention

For App Router UI, use `notFound()` for a nonexistent resource or an existing
resource whose presence must not be distinguishable under the effective user/tenant
policy. In this adopted convention do not introduce `forbidden()`/`unauthorized()`
as UI conventions without an explicit decision. This is not a universal framework
limitation and does not erase endpoint contract distinctions.

Route Handlers return explicit 401/403 when required by their HTTP contracts.
Validation errors, transient infrastructure failures and authorization failures that
must be communicated as forbidden are not generic not-found cases. Resolve actual
existence/visibility under effective tenant scope on the server, without leaking
out-of-scope resource details. Product visibility policy decides indistinguishability;
do not invent it to hide an authorization failure.

## Global safety nets and copy

Copy is brief, neutral, actionable and nonsensitive, with no internal details.
Do not invent arbitrary tones/messages per feature unless explicitly requested.
Use `global-error.tsx` only as a safety net for failures not caught by segment
boundaries; use global-not-found only for a real global 404 need and with installed
framework support verified. Do not move feature-specific handling to global scope.

Avoid catch-everything UI hiding structural errors, treating every failure identically
or duplicating error patterns without segment criteria. Mutation errors/invalidation
retain their normal flow; fallback client code must not expand the data boundary.
Verify latency/fallback ownership, expected error versus exception, meaningful recovery,
nonexistent/invisible versus invalid/transient cases and no tenant information leaks.
