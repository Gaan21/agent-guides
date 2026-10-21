# UI design

For visual interface design/review, design systems, component libraries, interaction
and accessibility decisions. Not a universal framework manual or a task planner.

## Always

- Read existing tokens/theme, reusable components and relevant local stack/product
  contracts before proposing changes. Respect native screen and shell exceptions.
- Local design decisions govern external inspiration, under project security,
  ownership and stack authority. Do not duplicate the existing design system or
  replace tokens, branding, architecture or components from a generic reference.
- Meet at least WCAG 2.1 AA: contrast 4.5:1 normal text and 3:1 large text.
  Respect platform target sizes, reduced motion and relevant semantic roles.
- Specify all applicable states, including empty, loading and error, not just the
  happy path. Validate both modes when dark mode is active.
- Factory owns tools, branches, review and publication: add no parallel workflow.
  Manual validated closure uses scoped commit/push on the agreed branch without
  another prompt, unless repository/host instructions require separate authorization.
  Missing/failing required checks block closure and commit/push; report and consult.

## Read for the affected design

| Work | Required detail | Dependencies |
| --- | --- | --- |
| Layout, tokens, components or platform consistency | [Design](topics/design.md) | This entry; existing design and stack contracts |
| Contrast, targets, semantics, dark mode or animation | [Accessibility](topics/accessibility.md) | Design and this entry |
| Developer specifications or final design review | [Handoff](topics/handoff.md) | Design and accessibility |
| An unresolved standards/reference question | [References](references.md) | Applicable local topic first |

Do not read every reference or redesign unaffected UI on each patch. Ordinary
non-visual code changes need no design exploration. External references remain
optional technical support, not installed skills, generators or copied datasets.

[Inventory](INVENTORY.md) · [Notices](NOTICE.md) · [License](LICENSE)
