# Commits and publication

Owner-authorized adaptation, revised 2026-10-21.
Dependencies: [entry](README.md), section "Always", and [checks](checks.md).

## Ownership and scope

- In a factory, hand off to its commit/push mechanism. Do not add a second manual
  commit or publication after the host has already done it.
- In manual work, successful completion authorizes commit and push of the validated
  task changes on the agreed branch, without another approval request. It is not
  permission to commit every edit/message, close unrelated work, merge or release.
- Inspect the complete diff, existing index and untracked files. Use the task's
  explicit scope when provided. Preserve other work and avoid `git add -A` or broad
  staging that could include unrelated files. Do not unstage someone else's work;
  clarify mixed staged content before committing.
- Inspect for secrets, personal/private data and unintended generated artifacts.
  Do not publish credentials or make private material public because checks passed.
- Keep commits atomic and reversible: one coherent idea, with unrelated formatting
  or refactors separate. No universal size/time cap requires creating extra tasks.
- Respect existing hooks/guards. Do not bypass them, change credentials/global Git
  settings or install hook tooling to make a commit succeed.

## Messages

Use repository conventions. Where none replace it, use Conventional Commits:

```text
type: short imperative description (task-id when applicable)

Optional body explaining the reason and important decisions.
Optional breaking-change and reference footers.
```

- Types: `feat`, `fix`, `refactor`, `test`, `docs`, `style`, `chore`, `perf`.
- Keep the subject at most 50 characters under this default convention; include
  the task ID when one exists. Ask about a genuine conflict with local conventions.
- Avoid generic messages such as `wip` or `fix stuff`.
- Do not add AI-tool coauthor/generated-by trailers. Preserve truthful required
  attribution and licensing; never fabricate authorship.

## Publish and report

- Run the required applicable checks before commit. A failed or unavailable required
  check stops closure and commit/push; [report and ask](checks.md), section "Blocked checks".
- Inspect the intended remote, branch and staged diff before committing/pushing.
  Never force-push `main`, `master`, `develop` or another protected branch.
- Set upstream only when required by the agreed new-branch flow; do not change
  remotes or use another destination to work around access/protection failures.
- Verify commit and push results separately. If commit succeeds but push fails,
  retain the local commit, report the failure and ask; do not reset or force-push.
- Report the resulting commit and destination, or the exact unpublished state.
  A successful local commit is not proof that remote publication succeeded.
