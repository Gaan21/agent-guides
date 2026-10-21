# Foundation

Required before Astro implementation. This topic supplies the base dependency
for every other topic. The entry's adopted decisions prevail over external
recommendations; official docs explain platform behavior, not permission to
change local policy. Escalate unsupported or conflicting requirements.

## Structure and names

- `src/pages/`: file-based routes (`.astro`, `.md`, `.mdx`, `.ts`); pages use
  kebab-case. Orchestrate layouts/sections, not presentation logic; supply SEO
  metadata via layout props or a named head slot. Static dynamic routes require
  `getStaticPaths()`.
- `src/layouts/`: PascalCase with `Layout` suffix; typed props, default content
  slot and named head slot. HTML structure/global components, no business logic.
- `src/components/`: PascalCase; one file/responsibility. Group head metadata
  under `seo/`, shared header/footer/navigation under `layout/`, reusable controls
  under `ui/`. Landing sections use `Section` suffix; controls have descriptive
  names. No implicit props or frontmatter side effects except own data fetching.
- `src/content/`: collection files; declare collections in `src/content.config.ts`,
  not `src/content/config.ts`. Use kebab-case collection names, plural where
  appropriate (legal, guides, faq); use entry IDs rather than legacy slugs.
- `src/styles/tokens.css` and `global.css`: single tokens plus global base;
  `src/assets/`: imported processed images; `src/lib/`: helpers/shared types with
  camelCase filenames. No extra source folders without justification.
- `public/`: untouched favicon, robots, OG, fonts and deployment headers/redirects;
  reference by URL string, never JS import. Import source assets for optimization.
- Root configuration is `astro.config.mjs`, `tsconfig.json`, `package.json`.
  Pages and content configuration have special meaning, but are not the only
  reserved framework paths: middleware and v7 fetch routing files also exist.
- English code/identifiers. Resolve content locale from the selected site's
  approved requirements, not from an example's language.
- Tokens use semantic `--color-*`, `--font-*`, `--spacing-*` names; environment
  identifiers use SCREAMING_SNAKE_CASE; asset filenames are descriptive kebab-case.

## Types

- Extend `astro/tsconfigs/strictest`; never lower to strict/base.
- Never `any`. Type assertions require documented justification in a comment.
  Non-null assertions are prohibited except very justified dependency injection;
  use explicit narrowing elsewhere.
- Every component declares local `interface Props` in frontmatter, including
  explicit optional fields and union variants rather than unrestricted strings.
  `Astro.props` then receives that interface's type. Use presence-aware optional
  prop forwarding; do not send undefined to a strict optional prop inadvertently.
- Use framework types such as `CollectionEntry`, `GetStaticPaths`,
  `InferGetStaticPropsType` and `ImageMetadata`. Preserve `interface Props` when
  deriving dynamic-page props from static-path inference; do not substitute an
  untyped template or weaken strictness to make an example pass.
- Advanced types must reduce real domain risk, not over-engineer simple features.

## Static components and v7 behavior

Default to static HTML without hydration. Evaluate client JS before adding any
directive; least aggressive suitable directive wins. Below-fold interaction uses
`client:visible`, non-critical widgets use `client:idle`; `client:load` requires
critical above-fold interaction. `client:only` is an exception for browser globals
at module scope, with the relevant framework specified, not a default workaround.
See [SEO/performance](seo-performance.md) when changing hydration or assets.

Astro 7 defaults to `compressHTML: 'jsx'`: newline-containing whitespace can
disappear. Preserve explicit spaces between inline text/elements where needed
and inspect rendered HTML after upgrades. Formatter `astroCompressHTML` must
match the compiler's compression semantics; check supported installed options.
All non-void tags must close. Invalid HTML nesting is not corrected by the Rust
compiler; validate structure rather than relying on old tolerance.

For Markdown pipeline rules read [content](content.md). The fully static pnpm
stack declares `sharp` directly for image processing without an adapter. This
policy is not a claim that every Astro deployment requires that dependency.

## Completion evidence

Check relevant names, typed props, structure, rendered spacing and prohibited
patterns; apply the [quality contract](quality.md). Framework build success is
not proof that every architectural or accessibility obligation was enforced.

References: [Astro 7 behavior](https://docs.astro.build/en/guides/upgrade-to/v7/),
[TypeScript](https://docs.astro.build/en/guides/typescript/).
