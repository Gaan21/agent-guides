# Guidance maintenance

Select only for creating, changing, reviewing or auditing agent guidance (bundles,
entries, topics, references, notices) and for companion-linter changes that affect
guidance. Not for ordinary product tasks. Repository maintainer instructions and
host protections stay authoritative. Selecting this bundle selects no other bundle
and installs no tool, lint, hook or configuration.

## Always

- Preserve every rule, exception, condition and dependency modality when moving,
  splitting, deduplicating or summarizing. Removing or weakening a rule needs an
  explicit owner decision, recorded with the change.
- Uncertain common-versus-product classification stays in the private product
  guidance. Public guidance contains no private paths, product APIs, product
  architecture rules, consumer logs, classification reports or internal pins.
- Never edit an installed or live guidance snapshot. Consumer sessions report
  findings as proposals; approved changes happen in the guidance source.
- Every guidance addition, change or removal needs a bidirectional
  [linter impact review](topics/lint-impact.md).
- Original text only under its license; third parties by link and notice.
- **Factory-managed work:** the factory owns branches, tools, validation and
  publication. Do not add branches, checks, PRs or publication of your own.
- **Manual work:** keep the agreed branch. At successful validated closure, commit
  and push the task's validated scope without another prompt, unless repository
  instructions or host protections require separate authorization. No merges,
  releases, other-repository publication or consumer activation follow.
- A missing or failing mandatory check blocks closure and commit/push: report the
  actual results and consult the owner or host blocked-work mechanism.
- This bundle defines no task planning, kanban, task creation or line/file/duration
  task limits; the owner schedules audits.

## Read before applicable work

| Work | Required local reading |
| --- | --- |
| Write, change, split or remove guidance; entry/topic structure; consumer findings | [Authoring](topics/authoring.md) and [Linter impact](topics/lint-impact.md) |
| Audit, duplicates, examples, links/references, upstream drift | [Audit and references](topics/audit.md) and [Authoring](topics/authoring.md) |
| Third-party material, licenses, notices, provenance, public output | [Rights and notices](topics/rights.md) |
| Linter rule added, changed or removed | [Linter impact](topics/lint-impact.md) |

Read relevant detail before applicable work and reuse it while it is in context.
Read again after context loss or changed scope, not per patch; no all-topic reading
is required. Missing guidance: report the gap and keep these invariants.

[Inventory and conditions](INVENTORY.md) · [License and notices](NOTICE.md)
