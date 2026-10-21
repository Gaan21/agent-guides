# Reading and authority

Applies before implementation, snippets and changes of scope. Depends on the
[entry](../ENTRY.md). For review also read [review](review.md); for closeout read
[validation](validation.md). Do not read unrelated topics just because they exist.

## Establish the applicable contract

- Identify the actual project/worktree root, assigned scope and changed boundaries.
  Read root and affected folder instructions; do not infer the consumer from the
  guidance repository's parent directory.
- Local critical security/ownership invariants and approved stack/runtime/tooling
  decisions govern. Local reference notes mediate external technical references;
  those references are not final authority or direct entrypoints. Respect system
  and host instructions; a guidance file does not override them or the user's scope.
- Follow explicit approved local exceptions. If requirements conflict, explain the
  exact conflict and seek the owner/host decision rather than silently relaxing it.
- Required concrete preloads must all be read before writing code. If no preloads
  exist, use the selected stack entry to identify invariants and specific relevant
  topics. Follow their required dependencies, not every reference list recursively.
  No fixed number of starting files may omit an applicable mandatory dependency.
- Choose the most specific topic matching a concrete path, field, boundary or
  pattern. A strong signal needs no permission to read; briefly state the choice
  and reason. Weak context or equally plausible scopes warrant one minimal question.
  Do not ask step by step for actions already defined and authorized.
- If guidance is missing, request a concrete path or record the minimal unresolved
  decision. Consult official version-appropriate sources for technical gaps; ask
  before inventing architecture, interfaces or product behavior. A missing required
  contract blocks affected implementation, not unrelated safe investigation.

## Identity and context

- Use the task's retained identity, including source revisions, selected bundles,
  engine, local policy and overlay identity. Reviewer and implementer share it;
  neither resolves a newer branch independently. A cache path is not identity.
- Preparation/update belongs to the authorized host/tool workflow, not each prompt.
  Do not change live guidance bytes, run a retired loader or silently substitute a
  newer rule mid-review. Report identity mismatches through the existing mechanism.
- Reuse relevant content while it remains in context. Read afresh after context
  loss or when the applicable selection/topic changes; no per-patch reread ritual.
- Source hashes establish integrity, not publisher trust or agent compliance.
  Configuration files and host tests do not establish observed native loading.

## Written output and snippets

- Prefer concise bullets/checklists and explain deltas, not repeated context. Longer
  prose is appropriate when requested. Authored guidance is English; conversation
  may use the user's language. Product document language follows its own contract.
- Cite a file and the section title in text; do not depend on fragile Markdown
  anchors. Check that referenced local files and named sections actually exist.
- Do not generate whole classes/files/screens by default. Snippets of at most 50
  lines are appropriate only when requested, for self-contained specific logic,
  targeted copy/localization/dependency registration, or a minimal application of
  loaded guidance. Read that guidance before the snippet. This is a snippet rule,
  not a task-size cap or a ban on an explicitly requested full implementation.
- A written scope describes context, expected architecture, functional behavior,
  acceptance and verification, not a copied tutorial implementation. Use the optional
  [format](../templates/task.md) only when useful; it has no operational state flow.
