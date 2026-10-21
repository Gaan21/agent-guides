# SEO, assets, performance and accessibility

Read before metadata/head/OG/canonical/sitemap, images/fonts, hydration,
performance or accessibility changes. Requires [foundation](foundation.md) and
[design/reference](design-reference.md); styling changes also require
[styling](styling.md). These are adopted site requirements, not claims that
Astro automatically implements them.

## Head and discovery

- Set the approved `site` URL in configuration for sitemap and absolute metadata.
  Every page has canonical metadata derived from `Astro.url` or the configured
  site, never a hardcoded per-page domain string.
- A typed reusable head component owns charset, viewport, title, description,
  canonical, optional noindex/nofollow, OG and Twitter metadata plus favicons.
  Required props are title/description; image, canonical override and noindex
  are explicit optional props with deliberate defaults. Use the selected site's
  approved name in titles, avoiding duplication when title already equals name.
- Preserve OG website type, URL/title/description/image/site name and Twitter
  summary_large_image/title/description/image. Resolve image URLs against site.
  Keep SVG and PNG favicon references. Root layout composes that head, global
  CSS and per-page head slot, with the approved document language. Forward
  optional props without violating strictest's exact optional-property rules.
- Integrate `@astrojs/sitemap`; verify generated sitemap-index.xml and its sitemap
  files in the build. Exclude draft/admin routes when applicable, not legitimate
  pages by accidental filtering. Supply `public/robots.txt` with `User-agent: *`,
  `Allow: /` and an absolute sitemap-index URL for the configured site.
- Stable OG URLs use `public/og/`, default `default.png` at 1200×630 and per-page
  descriptive images. Do not move OG into hashed source-asset output.

## Images, fonts and hydration

- Import product/content images from `src/assets/` and use `Image` from
  `astro:assets`; no raw img for those images. Alt is mandatory (and checked by
  the image component). Always specify width/height to avoid CLS. Hero/above-fold
  images load eagerly; the rest load lazily. Name assets descriptively in
  kebab-case, not generic numbered names.
- Favicon/OG use public URL strings. Web fonts live in `public/fonts/` and are
  linked from the head; public assets are never JS imports.
- Decide whether client JS is needed at all. If not, use static HTML. Only
  critical above-fold interaction warrants client:load; below-fold uses
  client:visible, non-critical uses client:idle. Evaluate the least aggressive
  suitable directive rather than hydrating everything. Module-level window or
  document use is the narrow client:only exception, with framework specified.
- Performance recommendations follow the real flow's risk. No structural rewrite
  without bottleneck evidence; local quality requirements remain the final gate.

## Semantics and keyboard access

- One h1 per page; no skipped heading levels. Use appropriate main/nav/header/
  footer/section/article landmarks and descriptive links, never only “click here”.
- Keep visible keyboard focus and a skip link at layout start whose target is the
  real main-content region. Use native CSS to make it visible on focus; a
  Tailwind-only utility name does not implement this requirement in this stack.
- Label navigation meaningfully; icon-only buttons require accessible names.
  Preserve form/keyboard usability and semantic roles, not ARIA added blindly.
- WCAG AA contrast: at least 4.5:1 normal text, 3:1 large text. Validate token
  contrast with a tool before defining colors; confirm focus and skip-link
  functionality, not just presence of markup.

## Completion

Verify the typed head and all metadata, configured site, sitemap build output,
robots/default OG, heading hierarchy, working focus/skip path, alt/dimensions and
hydration choice. Type checks must pass and SEO-related builds must have NO
warnings; use [quality](quality.md). Passing build alone proves neither contrast
nor screen-reader behavior.

References: [Sitemap](https://docs.astro.build/en/guides/integrations-guide/sitemap/),
[images](https://docs.astro.build/en/guides/images/),
[client directives](https://docs.astro.build/en/reference/directives-reference/#client-directives).
