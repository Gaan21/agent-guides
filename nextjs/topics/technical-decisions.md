# Technical decisions and optional diagnostics

Applies to risky/multi-surface work; local changes use the short entry and relevant
topic instead of a whole playbook. This is technical decision support, not task
planning, kanban, branch management or a second factory workflow.

Before applicable edits establish:
- Server/client boundary and real client need.
- Read/mutation, cache/runtime strategy, tag/refresh behavior and SA versus HTTP.
- Local/shared ownership, validation, caller identity/authz/tenant scope.
- Minimum client payload; segment loading/error/not-found impact.
- Env/exposure, adopted i18n policy, and relevant metadata/OG policy.
- If Proxy changes, bounded matcher, real Action/Handler authorization and a
  reproducible test; required verification level from [quality](quality.md).

Risk signals: permissions/tenant scope, data/cache/mutations, HTTP/Proxy, env,
fallback behavior, shared domain code or contracts across layers/surfaces. Treat
unclear cases as risky. Trivial means local and no such relevant functional impact.
Do not reopen closed policies or invent behavior/UX/naming/infra contracts. Consult
existing product/design authority before visual decisions; escalate when uncovered,
conflicting with the task or requiring a genuinely new decision. Do not ask again
for decisions already resolved. Keep changes within requested scope.

Optional evidence format: changed paths+goal; applicable topics/decisions; actual
checks/results; permitted manual scenario+steps+observed expected result+reason;
limits/blockers. Optional pre-edit/pre-close checklists can use the technical fields
above. Do not impose intake templates or task lifecycle bureaucracy.

## No new runtime mechanisms

Do not introduce Next-specific hooks by default. Playbook/technical judgment, relevant
guidance and real gates are the base, not ad-hoc remembered rules. Avoid fragile
semantic heuristics, single-tool dependencies, unprovided infrastructure and duplicate
architecture in plugins/hooks. Potential objective repetitive-error checks are future
proposals only: demand real benefit, low noise, manageable maintenance and approval.
Never install delivery hooks or assert active enforcement from generated files.

MCP is optional diagnostics/context, not required authority, auth validation or gate
replacement. Host/factory owns tool choice; Next-oriented diagnostics may be proposed
when useful, not forced. If an aid fails, identify what failed, real impact and safe
workaround/impossibility. Continue manual reasoning only within allowed work; required
checks still block validated closure if unavailable. Do not delegate blindly.

Keep responsibilities separate: entry navigates, topic defines technical rule,
host tools support execution and observed checks provide evidence. Avoid duplicated
inconsistent rules, noisy false positives and promises of complete detection.
