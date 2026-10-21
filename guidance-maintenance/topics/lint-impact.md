# Guidance and linter impact review

Applies to every guidance addition, modification or removal and to every
companion-linter rule addition, change or removal. Depends on the
[entry](../ENTRY.md) rules and [authoring](authoring.md).

## Guidance to linter

- Identify affected obligations, scopes, exceptions and diagnostic IDs.
- Review the companion linter for consistency, including obsolete checks.
- Decide whether a new or improved lint is feasible and worthwhile: detectable
  syntax, valid and invalid examples, false-positive considerations.
- Record remaining behavior-test or human-review obligations where static checks
  cannot establish compliance. A signature or annotation is not semantics.

## Linter to guidance

- For lint changes, update the corresponding guidance, documented limitations and
  focused tests.
- Review defaults, options and consumer compatibility.

## Boundaries

- Implementation and review share one candidate identity; neither resolves latest
  independently.
- Record the review outcome, including no impact. The review does not itself
  install lints, activate configuration, update consumers or redesign detectors;
  those need a task that authorizes them.
- Deferred improvement proposals are not implemented policy or a migration gate.
