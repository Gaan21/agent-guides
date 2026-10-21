# Quality gates and behavioral evidence

Applies to code changes and check diagnosis. Read relevant technical topic first;
[integrations](integrations.md) adds conditional runtime/i18n gates.

## Base and mode

Every code change requires lint, typecheck and build at validated closure. With the
adopted pnpm scripts these are `pnpm lint`, `pnpm typecheck`, `pnpm build`.
Next.js 16 linting uses ESLint CLI, not removed `next lint`; the official baseline
is `eslint-config-next/core-web-vitals` plus `eslint-config-next/typescript`.
Respect additional native plugin/rule and full-validation requirements. This bundle
does not install scripts, configs, plugins, dependencies or runtime mechanisms.

Manual feedback is by relevant blocks/changes with complete final applicable gates,
not an invented per-file/task-size cadence. Factory owns its checks/mechanism; do
not add a competing pipeline. Required checks must actually pass: missing tools,
environment failure or absent coverage cannot be relabeled success. Block closure
and commit/push, report exact results/impact and consult owner/host blocked handling.
Do not hide failures, lower lint severity or add ignores/exclusions without approval.

## Risk matrix (base gates always remain)

| Changed surface | Additional evidence |
| --- | --- |
| Simple copy/style/minor layout | Brief reproducible smoke/manual |
| Segment loading/error/not-found | E2E of affected flow |
| Server Action mutation | E2E happy path and at least one expected error |
| External HTTP Handler | Contract test: integration or reproducible manual; E2E if UI affected |
| Auth/authz/tenant scope | Allowed/denied E2E, or equivalent manual evidence if no automated coverage |
| Input validation | Invalid case by E2E/integration/manual appropriate to surface |
| Cache/data/revalidation | E2E of affected read/mutation refresh; equivalent real-flow evidence where permitted |
| Env/config | Required-config startup/fail-fast verification and no exposure |
| Pure logic with branches | Unit tests; adopted runner `pnpm test:unit` (Vitest) |
| Message/i18n flow | Mandatory project i18n consistency check in addition to base |
| OpenNext/Workers runtime impact | Target preview/runtime verification in addition to base/flow checks |
| Proxy | Bounded matcher, reproducible changed behavior and base gates |

Manual evidence is an allowed evidence form only where the risk matrix permits it,
not a blanket substitute for unavailable mandatory E2E/unit/build/runtime checks.
Record scenario, reproducible steps, expected result actually observed and brief
reason no automated test exists. Explain a genuinely inapplicable optional E2E/runtime
gate; do not waive a mandatory applicable one by writing a justification.

## Test-level selection

Unit isolates a function/hook/module; component tests isolated stable props/events;
integration tests module/layer contracts; E2E tests real browser flows in a production-
like environment; snapshots only support stable UI. Choose the minimum level that
provides real signal; do not duplicate scenarios at multiple levels without reason.
User-visible navigation/auth/redirect/error/mutation contracts favor E2E; pure logic
favors unit/integration. Do not make snapshots the sole business evidence.

For async Server Components prioritize E2E and pure server/shared logic tests rather
than forcing full-component unit rendering. Extract testable pure logic from a
`server-only` file into `*.utils.ts` without Next/React/server-only dependencies;
adopted tests live in `tests/unit/<module>.test.ts`. Do not weaken server boundaries
just to make a test import work. Branching helpers/mappings/state machines/domain
calculations, stable extracted contracts and logic awkward to cover with real-session
E2E merit unit tests. Trivial branchless functions and logic already adequately
covered by types+existing E2E do not need cosmetic duplicate tests.

Vitest is the adopted pure-TS/ESM runner, not a universal choice. Component/integration/
snapshot categories do not imply an installed standardized runner. Reconsider with
the owner before switching to Jest/React component tooling; do not silently migrate.

No exhaustive E2E suite for a trivial change unless native policy requires it, but
no sensitive closure on technical gates alone, CI-only claims instead of required
local checks or tests that merely reproduce implementation. Validate denial/error/
refresh as appropriate, correct ownership, server/client boundaries and secret safety.
Report actual commands, outcomes and blockers, not just “tested”. Browser host-library
failures are environment blockers, not passing tests. Do not claim host validation
proves client loading or model compliance.
