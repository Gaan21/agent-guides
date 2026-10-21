# Design handoff and verification

Applies when delivering specifications or reviewing finished design. Depends on
[design](design.md) and [accessibility](accessibility.md), including their entry rules.

## Developer specifications

- Describe structure, referenced/new tokens, reusable components, applicable states,
  animations/timing and dark variants. Explain why the design solves the objective.
- Identify local/native screen contracts and exceptions that constrain implementation;
  do not invent product APIs, base classes or brand values from generic examples.
- Confirm tokens are defined or referenced without magic values; all component
  states and meaningful edge cases are specified; existing components were checked.
- Record actual accessibility validation: contrast at least WCAG 2.1 AA, target
  sizes and semantics, both modes if dark mode is active, and reduced-motion behavior.
- Distinguish proposed design, implemented behavior, measured validation and not-run
  checks. A visually plausible mockup does not prove accessibility or runtime behavior.

## Reference and change boundaries

- Local design guidance is authoritative over community recommendations, subject
  to project and stack authority. External references are technical support only.
- For a requested/performed reference comparison, follow the
  [references](../references.md) conditional comparison contract, section "Conditional
  comparison contract", before adopting a delta or systemic proposal. Reuse host
  evidence rather than introducing a separate review/report workflow.
- Broad visual exploration is optional when explicitly requested or useful to the
  design objective. Validate any candidate against existing tokens, accessibility,
  performance, stack and product context before proposing adoption.
- Do not persist generated design-system files unless the human explicitly asks.
  This bundle includes no generator, script, palette database or external skill.
- Do not install a design tool or change host configuration to follow a reference.
  No external default stack, theme or new global style overrides the selected stack.
- Use the factory's established handoff/review/checks; do not create a second result
  file, reviewer, branch or publication routine. Manual work uses the entry's scoped
  validated-closure rule. Missing/failing required checks block closure and commit/push;
  report the gap and consult instead of claiming the design is complete.
