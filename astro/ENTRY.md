# Astro — adopted static-site policy

Select this bundle for the adopted **Astro 7 / fully static / pnpm /
TypeScript strictest** stack. These are chosen conventions, not universal Astro
limitations. Do not upgrade a consumer, add adapters, Tailwind or CSS Modules.
Pause on an invariant mismatch; discuss evidence and obtain owner approval before
changing a decision, then update affected guidance consistently.

Before implementation read [foundation](topics/foundation.md); read applicable
detail below before its edits. Reuse relevant guidance while in context; do not
read every topic or reread per patch. Always preserve typed Props, no `any`, only
documented justified casts and the narrow justified DI assertion exception;
tokens/scoped styles, accessible markup, optimized local images, least hydration,
and secret isolation. Unknown guidance: report the gap and retain these invariants.

| Task content | Required local detail |
| --- | --- |
| Collection, legal/FAQ/guide/blog, schema, Markdown/MDX | [Content](topics/content.md) |
| Styles, CSS, tokens, global/scoped styles, dark mode | [Styling](topics/styling.md) and its design dependency |
| SEO, head/meta/OG/canonical, sitemap, performance, images, hydration, accessibility | [SEO/performance](topics/seo-performance.md) and its design dependency |
| Environment, PUBLIC_, secrets, config, deploy/Pages | [Environment/deploy](topics/env-deploy.md) |
| Tooling, lint/check/build, formatter, CI or gate failures | [Quality](topics/quality.md) |

All changes retain the [quality contract](topics/quality.md): factory work uses
its own validation/branch/publication mechanism, without a second workflow.
Manual work gets feedback by blocks/relevant changes, then full final validation:
`pnpm format:check`, `pnpm lint`, `pnpm astro check`, `pnpm build`, in that order
through `pnpm validate`. CI retains all four; SEO builds must have no warnings.
Missing/failing required checks block closure and commit/push: report actual
results and consult the owner/host blocked-work mechanism. Never weaken gates.
Manual successful validated closure performs scoped commit/push on the agreed
branch without another prompt; no extra branch, merge, release or activation is
authorized. Unknown mode/authority requires clarification.

[Inventory and conditions](INVENTORY.md) · [License and notices](NOTICE.md)
