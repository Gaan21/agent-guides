# Environment and static deployment

Read before environment consumption, secrets, configuration or Pages deployment
changes. Requires [foundation](foundation.md); sitemap/head changes also require
[SEO/performance](seo-performance.md), tooling changes [quality](quality.md).

## Environment boundary

Only when the site consumes environment variables, define a typed `astro:env`
schema in `astro.config.mjs` with required/optional fields and appropriate
`envField` types from `astro/config`. A site with no variables declares no
unnecessary schema.
Import schema variables from `astro:env/client` or `astro:env/server` in components
and TS modules. Context/access define exposure: do not confuse this schema API
with the `PUBLIC_` prefix convention of `import.meta.env`.

`PUBLIC_*` in import.meta.env can be read on client and server; non-public values
remain server-side. Never prefix secrets PUBLIC_ or send server secrets through
rendered HTML/client props. Schema client variables must be public, never secret.
Keep `.env.local` ignored and never commit secrets.

Do not import `astro:env` in astro.config.mjs. Use process.env for environment
already provided to config; .env files are not automatically loaded there.
Schema validation timing depends on access: public values are validated for
builds, secrets normally at runtime, with explicit secret-validation options
when needed. Do not claim every required secret is guaranteed to fail the build;
verify the actual configuration and report missing required values truthfully.

## Adopted static Pages target

Use explicit `output: 'static'`, the approved site origin, and sitemap integration.
All pages are prerendered in this adopted policy: no adapter. Do not add auth,
SSR or edge functions as an incidental deployment fix. Any change to that scope
requires an explicit documented decision first, including adapter implications.
`hybrid` is an obsolete output value; modern Astro can support on-demand routes
even under static output, but that capability does not change this site's policy.

Cloudflare Pages uses build command `pnpm build`, output directory `dist`, and
the correct project subdirectory as root in a monorepo. Production branch is the
team-agreed branch, not an instruction to create or switch to main. Factory
controls deployment/publication through its own mechanism; no Wrangler/Workers
workflow, executable wrapper or live configuration change is authorized here.

Verify site/sitemap, env exposure/validation and real build output with the
[quality contract](quality.md). Required unavailable or failing checks block
closure, not merely a warning in a commit.

References: [Environment variables](https://docs.astro.build/en/guides/environment-variables/),
[rendering modes](https://docs.astro.build/en/guides/upgrade-to/v5/#removed-hybrid-rendering-mode).
