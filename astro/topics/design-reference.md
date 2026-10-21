# Local design and controlled references

Read before visual design, contrast, accessibility or interaction decisions;
required dependency of [styling](styling.md) and
[SEO/performance](seo-performance.md). Requires [foundation](foundation.md).

## Local design authority

Read existing design tokens and patterns first. Do not duplicate existing
components or override the approved system with community advice. Required inputs
are component/screen objective and context, existing tokens, target platform and
whether dark mode is required. Respect applicable local UI contracts; this bundle
does not supply another platform's screen hierarchy.

Use a minimal visual gap analysis. Document structure (ASCII or description),
tokens used/new, default/hover/disabled/error/loading/empty states, dark variant
when applicable, decisions and developer handoff (structure/tokens/states/motion).
Validate contrast, semantics and a minimum 44px touch target in the web design;
for explicitly cross-platform output respect the relevant 44×44pt iOS or
48×48dp Android minimum instead of treating units as interchangeable.

Define tokens before components, no hardcoded colors/sizes. Meet at least WCAG
2.1 AA: 4.5:1 normal and 3:1 large text. Validate both modes when dark mode is
active; map semantic surface/text/primary/error colors, not hex inversion. Avoid
flashing during mode changes. Design mobile-first with desktop progressive
enhancement, respecting the target platform rather than importing a mobile API.

Feedback motion should stay below 300ms and transitions below 500ms; honor
prefers-reduced-motion. Avoid excessive shadows/blur in long lists. These are UI
motion budgets, not task-duration limits. Never design only the happy path or
animate without reduced-motion handling.

## References support, not override

Local critical security/ownership invariants take precedence, then local stack
and tooling policy, then local reference conditions, then external advice. The
most specific/restrictive security/ownership rule wins. External material never
becomes an entrypoint or final authority; no skill installation/invocation follows.

For UI/forms/keyboard/contrast/semantics, read affected local UI/testing guidance
and compare with [web.dev accessibility](https://web.dev/accessibility) and
[WCAG quick reference](https://www.w3.org/WAI/WCAG21/quickref/). Rank actionable
risks high/medium/low and record differences in the review evidence. Distinguish
intentional documented local decisions from unintended drift; propose only the
minimal keep/context-note/correction action. No broad UI rewrite without scope.

Performance advice follows real flow risk and bottleneck evidence; advanced TS
types must reduce real risk without over-engineering. Existing Vitest tests, if
selected by the project, keep their local testing matrix/gates; improve patterns
without ungrounded scope growth. This bundle adds no testing framework or gate.

Optional broad visual exploration may be used only when useful to that task or
explicitly requested. Community palettes, typography, landing/chart patterns or
stack notes are inspiration, not authority over tokens/accessibility/performance/
product constraints. Do not persist generated design-system files unless the
human explicitly requests them. Community datasets/scripts are not included.

Confirm tokens, full states, contrast in applicable modes, semantics and handoff;
actual user behavior remains a review/test obligation, not a generated-file claim.
