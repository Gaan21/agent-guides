# Validation and truthful closeout

Owner-authorized adaptation, revised 2026-10-21.
Dependency: the [entry's mode and authority rules](README.md), section "Always".

## Use the actual environment's checks

- Factory work uses its required tools/checkpoints and acceptance signals. Do not
  invent another pipeline, duplicate executed tools, or replace required checks
  with a generic checklist from this bundle.
- Manual work follows the project's applicable documented validation commands.
  Identify package/root, relevant scope and prerequisites before executing them.
- For code changes, preserve applicable formatting, basic lint on modified files,
  compile/type/build validation and passing existing relevant tests. Use the
  technology's actual commands; documentation-only work does not require unrelated
  code tools. Factory evidence satisfies these obligations through its own workflow,
  not a second pipeline. If applicable gates or commands are unknown, report the
  gap and obtain instructions; silence is not an empty set of required checks.
- This Git bundle does not mandate Dart/Flutter tools in every project, install
  tools, prescribe retry counts, or own technology-specific gate selection.
- Report each check's actual command, scope and exit result; distinguish passed,
  failed, skipped and not run. An unavailable tool is not a pass; neither a source
  file nor a configuration name proves that a check executed or enforced policy.
- Inspect required behavior beyond formatting/linting. A clean analyzer does not
  establish product correctness or successful remote acknowledgment of an operation.

## Blocked checks

- If a mandatory check fails or cannot run, stop closure and commit/push. Explain
  what failed, the affected scope and the missing input/tool/access; ask the user
  or follow the factory's existing blocked-work mechanism. Do not claim completion.
- Preserve failure output and existing protections. Do not suppress a lint, weaken
  tests, change a baseline, skip a hook, add a generic TODO or declare synthetic
  success merely to continue. Exceptions require explicit applicable authorization.
- Do not impose a blanket stop on unrelated safe investigation, but do not use
  investigation as permission to publish unvalidated work or close the task.

## Closeout

- State delivered behavior, changed files, required checks and their results,
  pending checks, limitations and residual risks.
- Factory: use its established result/handoff format; do not create tasks, move
  kanban state or trigger extra publication from these guidelines.
- Manual: after successful validation, perform the scoped commit/push described
  in [commits](commits.md), then report local and remote results separately.
- Read-only advice/research is not automatically a development task to commit.
  Do not report work as accepted merely because an agent claims it is complete.
