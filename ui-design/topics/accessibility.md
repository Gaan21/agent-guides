# Accessibility, motion and dark mode

Applies to visual and interaction decisions. Depends on [design](design.md) and
the [entry](../ENTRY.md). Follow local native/platform constraints as well as
these design requirements; do not lower an adopted stronger requirement.

## Accessible states and interaction

- Never ignore WCAG 2.1 AA at minimum: normal-text contrast at least 4.5:1,
  large-text contrast at least 3:1. Validate actual foreground/background pairs,
  including the states specified in the design; do not assume token names prove it.
- Validate semantic tags or native semantic roles and interaction target sizes.
  The local web design baseline is a 44px minimum touch target; native platforms
  use iOS 44 by 44 points or Android 48 by 48 dp, not interchangeable CSS units.
- Preserve applicable keyboard/focus and assistive interaction behavior required by
  the local platform/stack contract. Consult [standards](../references.md) for an
  unresolved accessibility question; do not import an external checklist as policy.
- Include empty, error, loading, disabled and other edge states as well as the
  happy path. Error and loading feedback must be part of the design handoff.

## Motion

- Budget feedback below 300ms and transitions below 500ms. These are design motion
  requirements, not task-duration budgets or evidence of measured performance.
- Respect `prefers-reduced-motion` on web and the corresponding platform setting
  in native UI. Do not propose animation that disregards the applicable setting.
- Describe animation intent, states and timing. Do not add excessive blur/shadows
  in long lists; check representative context rather than assuming visual effects
  are free. Existing local performance and accessibility policies still govern.

## Dark mode

- Adapt by semantic roles such as surface, onSurface, primary and error, not by
  replacing arbitrary hex values. Use the existing theme/token contract and its
  platform equivalents; these illustrative roles do not prescribe symbol names.
- Verify contrast in both modes before ending when dark mode is active. Include
  applicable state variants, not just the default static view.
- Switch modes without flashing; an animated theme or platform equivalent may
  implement the transition, subject to reduced motion and existing stack contracts.
- If dark mode is not required, record that boundary rather than inventing a
  second theme or silently treating the applicable contrast check as optional.
