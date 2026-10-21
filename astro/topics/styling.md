# Tokens and scoped styles

Read BEFORE changing tokens/global CSS or choosing a component's style strategy.
Requires [foundation](foundation.md) and [design/reference](design-reference.md).
Chosen baseline: CSS custom properties plus native scoped component styles;
no CSS Modules layered over Astro scoping and no initial Tailwind dependency.
Tailwind adoption requires a new explicit documented owner decision.

## Single token source

`src/styles/tokens.css` defines custom properties in `:root`, no element selectors
or presentation. Keep semantic colors (including hover, surface variants, border,
muted text, error/success), typography families/sizes/weights/line heights, spacing,
radii, shadows and layout variables here. Reuse the approved theme; do not reset
its palette or scale from sample values. Component colors/sizes/spacing use
`var(--token-name)`, not new hardcoded values or a second inline token source.
The documented media-query breakpoint literals are reference thresholds, not a
license for arbitrary hardcoded visual spacing. Escalate ambiguous non-token
values rather than broadening exceptions silently.

## Exactly one style responsibility

| Location | Allowed |
| --- | --- |
| `tokens.css` | Token definitions only |
| `global.css` reset/base | Minimal box sizing/reset; html/body/base headings/links; base typography |
| `global.css` accessibility/layout | Focus-visible, screen-reader utility, keyboard skip link, container width/padding, page shell and growing main region |
| `global.css` shared utilities | Generic button/section utilities ONLY when at least three unrelated components use them |
| Component `.astro` style | All remaining component-specific presentation, scoped by default |

Global CSS imports tokens. Import global CSS once in the root layout. Do not add
component-named global classes, section-specific complex animations, or selectors
depending on component internals. Single-component utilities move to scoped CSS;
complex variant growth calls for evaluating component extraction, not a global
dumping ground. A comment citing one consumer is not evidence of shared reuse.

Use light BEM: block, block__element, block--modifier. Components own their
structure and style together; use tokens for padding/background/font/color and
documented media-query thresholds for responsive changes. Never use `style
is:global` in leaf components; only in a layout when essential. Do not import
global CSS repeatedly or duplicate token definitions.

## Verification

New tokens belong in tokens.css, not inline. Confirm global classes meet their
layer/reuse condition, no component styles leaked globally, and local component
styles remain scoped. No hardcoded component color/spacing. Verify contrast and
visible keyboard focus, then use [quality](quality.md) feedback/final checks.
Reset and focus examples are not permission to rewrite an existing theme or to
introduce a styling framework.

Reference: [Astro styling](https://docs.astro.build/en/guides/styling/).
