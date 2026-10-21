# Structured content

Read before collections, typed frontmatter, Markdown/MDX or collection-rendering
changes. Requires [foundation](foundation.md). Use collections for repeated
schema-shaped legal pages, guides, FAQ or blog entries; not a unique complex home
layout or external API fetching in this adopted site policy.

## Define and validate

1. Identify collection name, file format and required/optional fields. Keep names
   kebab-case and plural where appropriate. Distinguish Markdown/MDX bodies from
   JSON/YAML data without reintroducing obsolete content/data type declarations.
2. Declare each collection with `defineCollection` in `src/content.config.ts`.
   Use the current Content Layer loader appropriate for its files (the `glob`
   loader from `astro/loaders` for local Markdown/MDX). Import Zod `z` from
   `astro/zod` and declare a schema for EVERY collection, even though the platform
   permits omitting it. Export all collections explicitly.
3. Retain a source folder such as `src/content/legal/` and descriptive file IDs.
   Define the loader's base/pattern deliberately. IDs belong to the loader;
   built-in glob IDs are slugified, not an unconditional filename-without-extension
   guarantee. Use `entry.id`, never legacy `entry.slug`.
4. Validate frontmatter against required/optional schema fields. Typical legal
   metadata in the adopted legal example has required title and last-update date
   plus optional description; preserve approved fields and their requiredness.
   Markdown/MDX must not contain business logic. Never invent legal text: use an
   explicit placeholder until approved content is supplied.

## Query and render

- Use `getCollection` to query a collection and map entries to static-path params
  and typed props for a dynamic page. Use `GetStaticPaths` and static-props
  inference with a local `interface Props`; pass the entry to the appropriate
  typed layout and render its content within that layout.
- For a single entry use `getEntry` and handle undefined before reading data or
  rendering. Preserve the missing-content/404 path rather than asserting presence.
- Import the `render` function from `astro:content` and render the entry with it;
  do not call obsolete `entry.render()`. The rendering result supplies Content,
  headings and processor-related frontmatter where supported by that pipeline.
- `CollectionEntry` supplies typed data from the schema. Body is raw content
  when retained and can be undefined; handle that possibility. Do not assume
  every collection entry has a Markdown body.
- Do not use `Astro.glob()` (removed), legacy config location, legacy collections
  compatibility flags or no-loader/type-only examples as an Astro 7 procedure.

## Markdown pipeline

Astro 7 uses Sätteri by default. Existing remark/rehype plugin requirements need
the supported unified pipeline: `@astrojs/markdown-remark` and
`markdown.processor: unified()`. Do not blindly paste old top-level plugin config
or add dependencies when no plugin requirement exists. A pipeline/dependency
change remains subject to the [quality permissions](quality.md); no consumer
upgrade is authorized by this guidance.

## Verify

Verify declaration/export, loader IDs, schema, valid file frontmatter, typed
query/rendering and missing-entry handling; apply the complete quality contract.
Relevant rendering must preserve layout and metadata, not just type-check.

References: [Content API](https://docs.astro.build/en/reference/modules/astro-content/),
[legacy removal](https://docs.astro.build/en/guides/upgrade-to/v6/),
[Markdown behavior](https://docs.astro.build/en/guides/upgrade-to/v7/).
