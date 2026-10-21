# Names, members and types

Applies to declarations and API changes. Also read [layers](layers.md) when changing
public boundaries and [resources](resources.md) when resource fields are involved.
These are adopted catalog conventions, not claims about universal Flutter style.

## Names and order

- Use snake_case files and UpperCamelCase classes. Use descriptive role names;
  nonprimitive variable names contain the relevant class name in camelCase. Do not
  abbreviate away the class name. Preserve selected detector wrapper/callback
  exceptions and project boundary names; semantic clarity still needs review.
- Order getters/setters, overrides, public methods, private methods. Field and
  constructor ordering and additional suffix/barrel conventions follow local
  authority. Do not silently rewrite an established stricter contract.
- Keep related responsibilities cohesive. Related types may share a file unless
  the existing project requires separate types. Avoid cross-layer dependency cycles.
- Prefer final bindings when not reassigned. Use const where construction and
  arguments are const-eligible, not as a promise that every rebuild disappears.

## Selective annotations

- Annotate public fields/top-level variables, public returns and public declaration
  parameters. Initializing/super formals inherit types.
- Locals and loops may infer static types. Explicitly annotate inferred dynamic and
  locally configured boundary names; annotate when a deliberately selected type is
  important. Use generic collection element types rather than accidental dynamic.
- Keep explicit resource-field types wherever installed cleanup detection requires
  them. Inference is not permission to bypass a selected cleanup obligation.
- Do not universally ban late, null assertions or cohesive type families. Review
  initialization guarantees/nullability; preserve stricter native selections until
  approved changes. Never add synthetic defaults merely to silence a detector.

## Change discipline

Inspect installed detector names, versions, options, severities and exceptions.
Formatter output does not settle API naming, architecture or ownership. A changed
written rule needs linter-impact review (including feasible useful new checks), not
automatic lint installation or consumer migration. No base-class redesign here.
