# Supabase bundle inventory

The declaration is the exact machine inventory; this is the authored reading map.
All Markdown is original guidance with reference-only external links.

| File | Purpose |
| --- | --- |
| [Entry](README.md) | Always-applicable boundaries and selective reading |
| [Architecture](topics/architecture.md) | Keys, pools, layers, API exposure, RPC |
| [Schema](topics/schema.md) | Types, naming, constraints, indexes, time |
| [Tenants](topics/tenants.md) | Membership, capability and tenant isolation |
| [RLS](topics/rls.md) | Policy semantics, trusted claims and helper safety |
| [Patterns](topics/rls-patterns.md) | Owner/team/role/public/hierarchy/share |
| [RLS performance](topics/rls-performance.md) | Plans, indexes, safe caching |
| [Migrations](topics/migrations.md) | Idempotency, data movement, forward recovery |
| [Local development](topics/local-development.md) | Isolated stack and diagnosis |
| [Database tests](topics/database-tests.md) | pgTAP, CRUD and function/trigger coverage |
| [Deployment](topics/deployment.md) | Native authority, checks, staged recovery |
| [Edge design](topics/edge-design.md) | Stateless handlers, errors, dependencies |
| [Edge auth](topics/edge-auth.md) | User/webhook/admin trust, CORS, Storage |
| [Edge tests](topics/edge-tests.md) | Injected unit and real-auth integration |
| [Performance](topics/performance.md) | DB/API, quotas/cache, maintenance |
| [Monitoring](topics/monitoring.md) | Advisors, alerts, safe logs and reviews |
| [Production](topics/production.md) | Readiness, privacy/compliance, operations |
| [Hardening](topics/hardening.md) | Least privilege and authorized containment |
| [NOTICE](NOTICE.md) | Attribution, adaptation and reference boundary |
| [LICENSE](LICENSE) | Complete Apache License 2.0 |

`guidance-bundle.json` declares schema 1, entry, every delivered file and notices.
There are no optional undeclared local dependencies or executable assets.
