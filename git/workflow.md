# Branches, worktrees and integration

Owner-authorized adaptation, revised 2026-10-21.
Dependency: the [entry's mode and authority rules](README.md), section "Always".

## Start from the actual environment

- Inspect status, staged/unstaged changes, current branch and repository instructions.
  Treat unfamiliar changes as existing work; do not reset, discard or overwrite them.
- In a factory, use its assigned checkout/worktree, branch and lifecycle. Do not
  create tasks, change task state or independently initialize another flow.
- In manual work, stay on the agreed branch. `develop` is valid when selected by
  the user; do not create/switch a branch merely because a task or session started.
- Where a new branch is requested, follow the repository's naming convention.
  Feature, fix, chore and docs prefixes express intent; no sprint/task-ID naming
  scheme is imposed on projects that do not use one.
- Do not turn read-only analysis into Git mutation or infer authorization to clone,
  install tools, change remotes, initialize submodules or refresh guidance.

## Concurrent work

- Separate simultaneous branch checkouts into separate worktrees when needed and
  authorized. Switching branches in one shared working directory affects everyone
  using that directory; never change another worker's checkout underneath them.
- Linked worktrees have separate indexes/checkouts but share branches, tags and Git
  objects. A branch normally cannot be checked out in two worktrees simultaneously.
- Inspect existing worktrees before choosing a location. Respect the host's assigned
  root and the same pinned guidance identity for implementation and review; do not
  infer automatic guidance loading from creating or entering a worktree.
- Before cleanup, verify ownership and pending changes. Do not force-remove a dirty
  worktree, delete branches or prune shared state as an automatic closeout step.

## Integration and conflicts

- PR is the default integration route when integration is needed. Use the
  [review procedure](review.md); respect the configured target and protections.
- A factory owns its integration steps. Manual work directly on an agreed branch
  does not need a redundant feature branch/PR merely to perform the approved push.
- A user may authorize another integration route, including a local merge; explicit
  approval does not bypass protected-branch controls or a conflicting host policy.
- Fetch/pull/rebase/merge can change state. Follow the approved workflow rather than
  automatically updating or rewriting the branch at session startup.
- If conflicts arise, pause, preserve the current state, report conflicting files
  and await resolution instructions unless resolution is already explicitly covered
  by the approved user/host workflow. Apparent simplicity is not authorization.
  In a factory, use its existing conflict/blocked-work mechanism, not a second
  approval pipeline. Do not choose ours/theirs, rewrite history or force a
  protected-branch push as a shortcut.
- Missing Git, credentials or repository context blocks the affected Git operation;
  report it. Do not initialize, install or reconfigure the environment silently.
