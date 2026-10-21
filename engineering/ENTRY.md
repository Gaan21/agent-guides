# Engineering principles

Select for code work in any stack. The project's native instructions, architecture,
stack guidance, lint selections and existing conventions stay authoritative; these
principles apply beneath them. Selecting this bundle selects no other bundle and
installs no tool, lint, hook or configuration.

## Always

- Fix root causes, not symptoms: when something fails, investigate why.
- Unsure: read more code first; still blocked: ask with short options.
- Conflicting guidance: flag it and choose the safer option. The most specific and
  restrictive security/ownership rule prevails.
- Unrecognized changes probably belong to another agent or person: inspect and
  preserve them, never revert them, and do not assume they are safe to build on.
- Leave brief breadcrumbs for future context in the closure record, commit or PR.
- Add no lint/analyzer suppression or exclusion without explicit user approval.
- **Factory-managed work:** the factory owns branches, tools, validation and
  publication. Do not add branches, checks, PRs or publication of your own.
- **Manual work:** keep the agreed branch. At successful validated closure, commit
  and push the task's validated scope without another prompt, unless repository
  instructions or host protections require separate authorization. No merges,
  releases or consumer activation follow. Unclear mode or authority: clarify first.
- A missing or failing mandatory check blocks closure and commit/push: report the
  actual results and consult the owner or host blocked-work mechanism.
- This bundle defines no task planning, kanban or line/file/duration task limits.

## Read before applicable work

| Work | Required local reading |
| --- | --- |
| Names, constants, duplication, function/class structure, lint findings, file growth | [Code quality](topics/code-quality.md) |
| External data (SDK, API, database, RPC), mapping, where logic or conversion lives | [Boundaries](topics/boundaries.md) and [Code quality](topics/code-quality.md) |
| Diagnosing errors, external documentation, web search, new dependencies, tool choice | [Sources and dependencies](topics/sources.md) |

Read relevant detail before applicable work and reuse it while it is in context.
Read again after context loss or changed scope, not per patch; no all-topic reading
is required. Missing guidance: report the gap and keep these invariants.

[Inventory and conditions](INVENTORY.md) · [License and notices](NOTICE.md)
