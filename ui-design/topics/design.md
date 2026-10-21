# Tokens, components and platform contracts

For interface design and visual refinement. Depends on the [entry](../ENTRY.md).
For interaction, theme or accessibility decisions also read
[accessibility](accessibility.md); final specifications use [handoff](handoff.md).

## Inputs before design

- Understand the screen/component objective and user context, current design tokens
  (color, typography, spacing), platform constraints and whether dark mode is needed.
  Ask about missing consequential requirements, not every cosmetic implementation step.
- Read the actual theme and design system before proposing new values or components.
  Identify reusable existing patterns, selected screen bases and shell ownership.
- For Flutter output, consult its applicable stack invariants and screen contracts
  first. Keep approved native/infrastructure exceptions; no universal base class or
  screen API is imposed by this bundle. Do the same for other selected stacks.
- Follow stack naming, member conventions and established APIs. Do not rename or
  translate symbols, token names or route contracts to match a generic design recipe.

## Propose the minimum useful delta

- Compare current and target design: use visual gap analysis where useful, not a
  speculative replacement of the whole system.
- Describe the visual structure with an ASCII layout or structured description.
  Reference tokens to reuse or justify tokens to create: colors, typography, spacing.
  Define tokens before components; do not hardcode colors or sizes outside tokens.
- Reuse components and interaction patterns. Never introduce an ad-hoc component
  that duplicates the existing design system; check for a suitable one first.
- Specify default, hover where relevant, disabled, error and loading states, plus
  empty and edge states. Platform differences are deliberate, not missing states.
- State the dark variant when applicable and explain why decisions solve the
  objective rather than merely listing what the UI contains.

## Cross-platform consistency

- Mobile-first; desktop is a progressive extension, not a different accidental UI.
- Respect native platform guidance, such as Material 3 or Cupertino according to
  context, without overriding adopted local component or navigation contracts.
- Minimum touch targets: 44 by 44 points on iOS, 48 by 48 dp on Android; use the
  applicable web guidance for CSS targets. Do not silently equate platform units.
- Performance matters: avoid excessive shadows/blur in long lists. Use the real
  product context and existing performance constraints; do not add libraries,
  global styles or architectural changes merely for visual inspiration.
