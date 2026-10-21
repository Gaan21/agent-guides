# Route/feature architecture

Applies when adding or moving routes, features, server data code or shared types.
Required companions: [boundaries](boundaries.md), [reads/mutations](reads-cache-mutations.md)
for data work and [server security](server-security.md) for callable operations.

## Adopted ownership model

- `src/app/`: routes/layouts, screen composition and route-local feature code.
- `src/components/`: UI genuinely reused across features, no domain business logic.
- `src/lib/`: domain-agnostic pure helpers, formatters/constants and technical utilities;
  not a catch-all for business logic or data access.
- `src/server/`: shared server data/orchestration/domain logic, not tied to one route.
- Start local. Extract for confirmed reuse, clearly shared domain ownership or a
  central consistency requirement, not speculative future reuse. No flat catch-all
  or ceremonial clean-architecture layers by default.

Inside a route, use private folders only when they add clarity: `_components` for
local UI, `_queries` for reads, `_actions` for internal mutations, `_schemas` for
input/params/form parsing. Do not create empty layers by habit.

Keep composition, exclusive actions/queries and flow-specific schemas close to the
route while ownership is clear. Extract genuinely shared UI, reused data access and
common domain logic. Reuse in 2+ routes/features is a strong signal, not a blind
threshold: clearly shared domain ownership can justify earlier extraction. Do not
duplicate a query/action just to avoid shared extraction.

## Server data location

Sensitive data access does not belong directly in UI/page/client files. A server
page composes and calls the server data layer; it does not become that layer.
Local reads/mutations live in `_queries`/`_actions`; shared reads/mutations in
`src/server/<domain>/queries` and `src/server/<domain>/mutations`.
`route.ts` is an HTTP boundary. Delegate nontrivial domain logic to `src/server/`
rather than concentrating it in the handler. Location never waives cache/security.
Provider-specific rules apply only under [adopted integrations](integrations.md).

## Domain constants and TypeScript

Use descriptive names conveying intent for files, functions, classes and variables;
avoid abbreviations/generic names and scattered magic strings. Give each domain
concept one definition point. Adopt const objects with `as const` plus value union
types for states/constants, and discriminated unions for states with extra data,
rather than native enums. Native enums emit runtime constructs; do not introduce
them, or fragile const-enum assumptions, to bypass the adopted convention.
Do not claim every enum necessarily fails a particular bundler.

Shared domain constants live in `src/server/<domain>/constants.ts`; exclusive
feature constants in `_schemas` or a local constants file. Client-shared types
must also respect the neutral type-module boundary in [boundaries](boundaries.md).
Advanced types are justified by actual domain-risk reduction, not cleverness.

Extract structurally repeated helpers at the correct layer: copying a body while
changing only the operation/provider name signals missing reuse. Normalize external
data at its boundary. Keep function bodies at one abstraction level, readable as
steps without opening every helper. These rules do not justify premature extraction.

Do not introduce a dependency without clear need and a maintenance/health check
(recent releases, adoption and ongoing maintenance). Prefer official version-dated
references. Adding a package is not evidence its architecture or tooling is adopted.

Before editing, establish domain/route, local folders actually needed, local versus
shared ownership, one server data entry, and read/mutation/security strategy.
Product-specific time, design and ownership contracts retain their own authority;
generic directory roles do not override a native explicit exception.
