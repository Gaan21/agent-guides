# Code quality

Applies when writing or changing code in any stack. Depends on the
[entry](../ENTRY.md) rules; read [boundaries](boundaries.md) when the change
touches external data or responsibility placement. Stack and project guidance,
existing APIs and lint selections prevail where they are more specific.

## Descriptive names

- Names express intent. Files, classes/types, functions and variables answer
  "what is it / what does it do?" without extra context, in every stack.
- No gratuitous abbreviations or generic names: `userAccessState`, not `s`;
  `PendingApprovalPage`, not `Page`; `getUserAccessState`, not `getState`.
- Keep stack-mandated suffixes, member order and naming conventions, generated
  names and existing public APIs. Do not rename for taste, translate symbols or
  impose a convention that contradicts the stack's; renames stay within task scope.

## Constants and enumerations

- Avoid scattered magic strings and values: one definition point per domain concept.
- TypeScript: prefer `const` objects with `as const` plus a derived union type over
  native `enum`. A native `enum` emits runtime code and is not erasable type-only
  syntax, so type-stripping execution and erasable-syntax settings reject it.
  `const enum` cross-module/ambient use can depend on declarations, inlining or
  runtime emission that the actual compiler/transpiler may not support consistently;
  version skew can also matter. Same-file use does not inherently require cross-file
  analysis. Verify the actual compilation strategy rather than declaring every
  const enum incompatible with per-file transpilation. See the
  [TypeScript enums handbook](https://www.typescriptlang.org/docs/handbook/enums.html).
- Existing project conventions and lint rules prevail; do not migrate existing
  enumerations outside task scope.

## Structural duplication

- A block of roughly 3–5 lines copied to create a new function, method or class is
  an unextracted helper. Strongest signal: copy-paste that changes only a method
  name, endpoint or remote procedure. Line counts are a signal, not a budget.
- Extract at the correct level of the stack architecture, not always the highest
  or most shared one. Respect layer, ownership and dependency boundaries.

## Uniform abstraction level

- Each function or method narrates its logic at one level of abstraction.
- Do not mix low-level parsing with domain logic in one body; that forces readers,
  human or agent, to switch mental levels.
- Goal: the main body is readable without opening any support function.

## Responsibilities and file growth

- Keep each file focused on a coherent responsibility.
- A code file growing toward about 500 lines is a review signal: consider
  refactoring or splitting it by responsibility when that improves clarity.
- It is a signal, not a limit: it never blocks work, forces a split or overrides
  project, stack or generated-file conventions.

## Lint and analyzer findings

- Never add inline ignore comments, file-level ignores, or rule/path exclusions in
  lint, analyzer or custom-lint configuration without explicit user approval.
- Fix the cause of a finding. Required gates come from the stack/project guidance
  or the factory; this bundle adds none and never weakens them.
