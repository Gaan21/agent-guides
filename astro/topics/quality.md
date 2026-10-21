# Quality contract and tooling permissions

Applicable to all Astro changes; read details before changing quality config,
debugging gates or evaluating lint dependencies. Requires
[foundation](foundation.md). No checks are installed or autoactivated by reading.

## Mode and truthful evidence

Factory work uses the host's own validation/branch/PR/publication mechanism;
do not create a competing pipeline or repeat its actions. Manual work receives
formatting/lint/type feedback after logical blocks or relevant changes, not a
mandatory per-file check and not a numeric file/time/line trigger. Fix malformed
files within the task. Do not defer all feedback to closure, nor run full validate
after each file. Use existing approved project commands, not a retired helper.

Full final validation retains all four gates in order:

| Gate | Command | Establishes / does not establish |
| --- | --- | --- |
| Formatting | `pnpm format:check` | Consistent Astro/TS/CSS/Markdown/JSON/JS formatting, not types or logic |
| Lint | `pnpm lint` | Configured Astro/TS quality/a11y diagnostics, not visual formatting/build correctness |
| Types | `pnpm astro check` | Astro frontmatter/template, collection and prop type checks, not runtime correctness |
| Build | `pnpm build` | Compiled static output and expected sitemap/image output, not all source quality |

`pnpm validate` runs those gates in sequence. `pnpm check` is equivalent only if
the existing script actually invokes astro check; plain tsc is not its substitute.
CI MUST retain all four gates. No merge with gate errors; SEO changes additionally
require no build warnings. UI/components/layout/CSS work always requires complete
final validate, not only touched-file feedback.
The adopted tools use eslint-plugin-astro and prettier-plugin-astro; their actual
configured versions/rules, not plugin names alone, determine diagnostic coverage.

Record actual commands/results, scope and unavailable checks. Missing/failing
mandatory checks block closure and commit/push; consult owner/host blocked-work
handling. Never remove/skip gates for speed or call a pattern-counted helper's
“clean” message proof. Manual successful validated closure performs scoped
commit/push without another prompt on the agreed branch; PR is integration
default, not a branch-away mandate. No unapproved merge/release/activation.

## Before changing tooling

- Read this topic first. Changes need documented justification in the review
  record (PR description when used). eslint.config.mjs, .prettierrc.json and CI
  workflow changes require approval; CI may expand or fix bugs, never lose gates.
- Keep strictest. Only justified paths/include/exclude adjustments; never exclude
  files to hide type errors. Do not modify validate; add new scripts only if needed.
- Inline eslint-disable or prettier-ignore needs explicit user approval and
  documented reason. TS-ignore/TS-expect-error needs an explanatory comment;
  do not use suppression to conceal an unresolved error.
- Assess health/need before incremental TypeScript-eslint minor updates or a
  plugin for an identified recurring issue. Stylelint, Biome migration, replacing
  Prettier or adding Husky/lint-staged/commitlint requires a new explicit documented
  decision. No hooks or new operational dependency follows from this bundle.
- Formatter astroCompressHTML must match Astro compressHTML semantics; validate
  installed support and rendered spacing without silently changing that policy.

## Lint versus judgment

Unambiguous repeated patterns may justify static checks: any/casts, missing
alt/accessibility names, missing typed Props or unused imports. Context-dependent
hydration, global/scoped boundaries, naming, collection applicability and component
extraction still need review. A generic plugin does not automatically enforce
all local rules; missing aria attributes are contextual, not universally errors.
For guidance changes review affected companion-linter obligations/diagnostic
coverage, feasible checks and residual human/behavior tests. Do not alter a
consumer's lint configuration or claim enforcement from prose alone.

At closure confirm relevant block feedback and full final results, config-change
approval/justification, no unapproved inline suppression, and unchanged CI gates.
