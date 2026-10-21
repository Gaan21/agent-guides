# Pull requests and integration review

Owner-authorized adaptation, revised 2026-10-21.
Dependencies: [entry](README.md), section "Always", and [checks](checks.md).

- Factory-managed branches and PRs follow the factory mechanism; do not create a
  duplicate PR or redefine its target, approval steps or completion signals.
- For manual integration, prefer a PR. Confirm the intended source/target under
  the repository's policy; do not hard-code `develop` for all repositories.
- Manual work on an explicitly agreed `develop` branch is allowed. Its normal
  validated commit/push does not require manufacturing a feature branch or PR.
- Do not create or merge a manual PR without the applicable user/host instruction.
  Commit/push permission alone is not PR/merge, release, deploy or branch-deletion
  permission. Never bypass protected-branch review/check requirements.
- Only submit review-ready work: acceptance criteria addressed, applicable tests
  and gates passed, and residual limitations honestly recorded. Failed or unavailable
  mandatory checks block closure, not merely add a warning to a ready-for-review claim.
- Use the repository's title/template; otherwise use a Conventional Commit-style
  title and include a task reference when applicable.
- Review summary: purpose and changed behavior, files/scope, acceptance checklist,
  tests and exit results, skipped/not-run checks, known risks and relevant references.
  Do not fill it with unrelated technology checks or claim every gate applies.
- Before creation, verify the intended commits were pushed. If the approved GitHub
  CLI route is unavailable/unauthenticated, report the gap and ask; a manual plan is
  not a created PR. Do not repair credentials or switch hosting destinations silently.
- Wait for the applicable review/merge authorization and checks. Do not infer
  acceptance or move task state because a PR was created or a push succeeded.
