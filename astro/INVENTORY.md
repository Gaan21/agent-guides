# Bundle inventory

Independent schema-1 Astro static-site bundle. Selecting it does not select
another bundle, install tools, change a consumer or guarantee model compliance.

| File | Applicability and local dependencies |
| --- | --- |
| ENTRY.md | Always: chosen stack, reading conditions, final gates and mode boundary |
| topics/foundation.md | Before implementation; base dependency of every topic |
| topics/content.md | Collections/Markdown/MDX/legal/FAQ; foundation |
| topics/styling.md | Tokens/global/scoped CSS/dark mode; foundation + design/reference |
| topics/seo-performance.md | Head/SEO/sitemap/assets/hydration/a11y; foundation + design/reference; styling for CSS changes |
| topics/env-deploy.md | Env/secrets/config/Pages; foundation; SEO for sitemap/head and quality for tooling |
| topics/quality.md | Every change retains its contract; detail before tooling/debugging; foundation |
| topics/design-reference.md | Visual/accessibility/interaction choices; foundation; controlled external contrast |
| NOTICE.md | License, adaptation notice, external rights boundary |
| LICENSE | Complete Apache-2.0 license text |
| guidance-bundle.json | Exact file/notices declaration; no runtime selector |

All requirements remain mandatory in their adopted scope, including exceptions
and prerequisites. Read relevant detail before applicable changes and reuse it
while in context; no blanket all-topic or per-patch reading. Missing guidance
requires reporting the gap, not inventing a new workflow or weakening invariants.
