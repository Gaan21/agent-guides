# Maintainer instructions

- Scope: public common guidance bundles only. English; concise; files below 500 lines.
  No engine code here; the tool is `agent-guides-cli`.
- Start at the agent-guides-cli task board (`docs/tasks/README.md` in that repository)
  and follow the task assigned there. Do not invent a separate board or plan here.
- One self-contained bundle per top-level directory, with `guidance-bundle.json`
  listing every file. Short entry; topic detail read on demand; notices kept.
- Preserve every rule when moving guidance. If common versus product classification
  is uncertain, it belongs in the product's private bundle, not here.
- No private paths, product APIs, product architecture rules, consumer logs,
  classification reports or internal revision pins.
- No automatic staging, commits, pushes or releases; each needs explicit authorization.
- Guidance additions, changes and removals require companion-linter impact review,
  including feasibility of new checks. Read `docs/deferred-improvements.md` for
  deferred proposals; do not treat them as implemented policy or a migration gate.
- When asked about pending work, read `docs/deferred-improvements.md` and the CLI
  task board; report both current delivery work and low-priority follow-up.
