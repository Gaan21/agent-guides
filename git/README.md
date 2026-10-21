# Git collaboration

Owner-authorized adaptation, revised 2026-10-21. Applies when this bundle is
selected for a project. It governs Git collaboration, not technology-specific code
rules, project planning or the task manager's lifecycle.

## Always

- **Factory-managed work:** follow the factory's assigned branch, tools, validation
  and publication flow. Do not run a second manual Git workflow, create additional
  branches/PRs, or duplicate commits/pushes. This bundle does not override the host.
- **Manual work:** keep the agreed branch, including `develop` when requested.
  At successful close, commit and push the task's validated changes without a
  separate approval prompt. This does not authorize unrelated changes or merges.
- If the mode or host instructions are unclear, clarify before Git mutation.
  No generic rule bypasses a repository protection, guard, permission or restriction.
- A failed or unavailable mandatory check blocks closure and commit/push; report
  the exact gap and ask. Never call an unexecuted check successful.
- Preserve unrelated work, secrets safety and independently reviewable task scope.
  There are no universal line/file/time caps or task-creation procedures here.

## Read before applicable actions

| Work | Required detail |
| --- | --- |
| Branch/worktree setup, conflicts or integration | [Workflow](workflow.md) |
| Stage, commit or push | [Commit and publication](commits.md), including [checks](checks.md) |
| PR or merge outside a factory-owned flow | [Review](review.md), including [checks](checks.md) |
| Report missing/failed validation or close work | [Checks and closeout](checks.md) |

Read relevant detail before the action; reuse it while available in context.
Read again after context loss or changed instructions, not before every patch.
Do not load all topics for a read-only question. Availability is not authorization
to install Git/CLI tools, change credentials, hooks, global settings or branch policy.

[License and notices](NOTICE.md).
