# Deferred Flutter guidance and lint improvements

Owner direction recorded 2026-10-21. Low-priority follow-up, not a new task board
or a prerequisite to T05. The CLI task board remains authoritative. These notes
record intended review, not implemented lint behavior or consumer migration.

## Preserve the baseline

- Retain presentation/domain/data boundaries and architectural controls. Consider
  narrowly approved alternatives only for a concrete need; do not build a new
  configuration framework or relax boundaries to remove boilerplate.
- Strict naming, member order and selective explicit typing belong to common
  Flutter guidance, not one product's private architecture.
- Keep guidance content, the Dart linter and the Python delivery CLI separate.
  Existing consumers retain their installed contracts until an authorized change.

## Status — 2026-10-21

The linter (commit `7b11533` and follow-up) now enables every rule by default, with
per-rule disabling and no presets. Items 1 and 2 are implemented there: Freezed is
an ordinary rule a project disables if unused, a shallow generator-independent
immutability rule was added, and Result checks exempt synchronous getters and
private helpers. Matching guidance lines were added to `flutter/layers.md` and
`flutter/failures.md`. Item 3 remains a written proposal in the linter's
`docs/deferred-guidance-alignment.md`; no base-class change.

## Review candidates (original text)

1. **Immutable values without a mandatory generator.** Freezed should not be a
   universal requirement. Assess inexpensive structural checks without claiming
   deep immutability; otherwise make the generator convention optional and check
   it only where explicitly adopted. Dependency presence alone does not select
   that convention for every entity. Evaluate alternatives and mutation tests.
2. **Explicit domain outcomes.** Preserve Result-style outcomes for domain
   operations, even when currently simple. Owner accepted: infallible getters and
   internal calculations return values directly; pure functions with expected
   rejection still use Result. Review detector coverage and expected failures
   versus programming defects. Consumer/linter changes remain deferred.
3. **Base classes.** Compare reuse and lifecycle/error responsibilities against
   composition and official recommendations. Do not prescribe replacement bases
   or migrate an existing architecture without evidence and separate approval.

## Required guidance/lint impact review

Priority: high importance for every future guidance change, applied during T05
review; no separate automation project is required. Generator-independent checks,
Result detector improvements and base-class alternatives have low urgency and
medium importance. They do not block lossless bundle preparation.

For every guidance addition, modification or removal:

- Identify affected obligations, scopes, exceptions and diagnostic IDs.
- Review the companion linter for consistency, including obsolete checks.
- Decide whether a new or improved lint is feasible and worthwhile; record
  remaining behavior-test or human-review obligations where static checks cannot
  establish compliance. Do not equate a signature or annotation with semantics.
- For lint changes, update corresponding guidance, limitations and focused tests;
  review defaults/options and consumer compatibility in the reverse direction.
- Retain one candidate identity for implementation/review. Do not silently activate
  new configuration, update consumers or resolve latest independently for review.

Companion follow-up: [dart-architecture-lints](https://github.com/Gaan21/dart-architecture-lints).
Official comparison sources: [Flutter recommendations](https://docs.flutter.dev/app-architecture/recommendations)
and [Result pattern](https://docs.flutter.dev/app-architecture/design-patterns/result).
These links are references, not permission to import third-party text or configs.
