# Next.js — adopted App Router guidance

Applies to selected Next.js App Router/TypeScript work. These are explicit adopted
conventions, not universal framework requirements. Preserve native project security,
ownership and product decisions; selection does not migrate architecture or tooling.

Always: server-first sensitive data, smallest necessary client boundary, validated
server inputs, surface-appropriate identity/authz/scope, minimum payload, explicit
read/cache strategy and truthful verification. Never infer permissions from UI.

Read relevant topics and their listed local prerequisites before applicable work;
reuse them while in context, refresh after context loss or changed guidance. Do not
load every topic or reread for every patch. Do not apply another stack's rules blindly.

| Work | Read |
| --- | --- |
| Routes, layouts, ownership, shared extraction, types | [Architecture](topics/architecture.md), [boundaries](topics/boundaries.md) |
| Reads, streaming, cache, mutations, Proxy | [Reads and mutations](topics/reads-cache-mutations.md) |
| Actions, HTTP endpoints, validation, auth, tenant data | [Server security](topics/server-security.md) |
| loading/error/not-found, recovery | [Fallbacks](topics/fallbacks.md) |
| Env, secrets, configuration | [Environment](topics/env.md) |
| Checks, unit/E2E/runtime evidence, closure | [Quality](topics/quality.md) |
| Adopted OpenNext/Workers, Supabase, next-intl, Tailwind/shadcn | [Conditional integrations](topics/integrations.md) |
| Risky/multi-surface decisions, optional diagnostics | [Technical decisions](topics/technical-decisions.md) |
| API doubts, upgrades, external contrast | [Reference policy](references.md) |

Use the project's agreed mode: factory mechanisms own tools/branches/PR/publication;
do not create a parallel workflow. Manual work respects the agreed branch, including
develop, and performs scoped commit/push at validated closure without another prompt.
Required missing/failing checks block closure and commit/push; report actual results
and consult owner/host blocked-work handling. PR is the integration default, not a
command to leave an agreed branch or bypass protections. No release authorization.

Local [inventory](inventory.md), [notices](NOTICE.md) and [license](LICENSE).
