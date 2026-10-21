# Bundle inventory

One selectable `nextjs` schema-1 bundle; entry is [README](README.md).
Every topic is local. No external skill/runtime/script installation or cross-bundle
dependency resolution. Integrations apply only under the project's adopted scope.

| File | Purpose |
| --- | --- |
| `guidance-bundle.json` | Exact declaration/inventory and notice selection |
| `README.md` | Short invariants, applicability and navigation |
| `topics/architecture.md` | Hybrid route/feature ownership and TypeScript conventions |
| `topics/boundaries.md` | Small client surface, minimum DTO and shared types |
| `topics/reads-cache-mutations.md` | Explicit reads, adopted cache/tags, mutations/Proxy/assets/metadata |
| `topics/server-security.md` | DAL normalization, server validation, authz and tenant scope |
| `topics/fallbacks.md` | Segment loading, expected/unexpected failures and visibility |
| `topics/env.md` | Private-default configuration and fail-fast secret protection |
| `topics/quality.md` | Complete base/risk gates and truthful evidence |
| `topics/integrations.md` | Conditional Workers/OpenNext/Supabase/i18n/UI/testing constraints |
| `topics/technical-decisions.md` | Technical predecisions, escalation and optional diagnostic limits |
| `references.md` | Local precedence and official external reading links |
| `NOTICE.md` | Attribution, adaptation and third-party boundary |
| `LICENSE` | Full Apache-2.0 license text |

Local prerequisites at each topic preserve security/cache/quality implications
without requiring unrelated topic reads. Native product locale, design, time,
ownership and full-check requirements remain independent authority. This guidance
does not change installed lints, authorize production actions or certify compliance.
