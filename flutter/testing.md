# Behavior and risk-based tests

Applies to test changes and validation selection. Required:
[verification](verification.md) and each changed topic's behavioral obligations.

- Use the simplest sufficient layer: pure/domain unit tests, widget rendering/actions,
  real collaboration integration tests, explicitly requested E2E. Classify effects;
  an in-memory DB collaboration is not an isolated no-I/O unit test.
- Isolate unit tests from real network/disk/clock; use interface mocks/fakes and real
  immutable values/builders. Native test contracts may be stricter. Domain tests do
  not import presentation infrastructure; presentation does not reach data directly.
- Arrange–Act–Assert; one behavior per test, descriptive names and meaningful
  assertions. Configure doubles/listeners before actions; await complete outcomes.
  Do not use global verify-no-more-interactions as a ritual or rely on test order.
- Use controlled time for debounce/timers/retry; avoid real sleeps. Do not mix fake
  time with awaited real operations. Reset fixtures, DI/global state, subscriptions,
  routers, databases and owned VMs at teardown; check post-disposal events.
- Cover success/failure and applicable branches: validation/defaults, mapper technical
  rejection/codec round trips, server rejection, create/update IDs, stack preservation.
- For VMs cover initial/loading/data/empty/error, refresh, previous-data retention,
  ordered effects, duplicate calls, stale responses and cleanup. Include every failing
  public action required by native error-effect policy; no universal test-count cap.
- For UI cover state rendering, meaningful interactions, stable row identity,
  reactive theme/locale and route/tab persistence. Use real router/shell collaboration
  when needed; do not assume a mock tests its lifecycle/guards/deep links.
- Choose stable unambiguous keys/types/icons for interaction finders. Text is valid
  when testing copy/localization; preserve stricter project finder policies.
- Use bounded pump steps with controlled time for periodic timers/infinite animation;
  pumpAndSettle only when the work can settle. Condition waits need explicit limits
  and useful failure messages, not unbounded retries that conceal regressions.
- Meaningful visuals and DI wiring are legitimate risks. Generated code/trivial
  getters need no ritual tests, but test boundary behavior/equality/codecs where
  relevant. Golden baselines need stable environment and reviewed differences;
  no blanket legacy retrofit or universal tool requirement.
- Preserve actual consumer coverage/check baselines. No universal pyramid quota,
  coverage percentage, timing target or numeric maximum substitutes for risk cases.
  Quarantine cannot turn a required failed check into a successful closure.

## E2E boundary

Manual work runs an E2E matrix only on explicit user request, never automatically at
task close. Factory work uses its expressly approved mechanism, without a parallel
manual workflow. Both modes retain isolation and the applicable validation contract;
this guidance defines no CI calendar. Use the verified consumer harness/fixtures and
isolated synthetic backend data, not
production. Reuse approved stable keys, condition waits, runtime-error capture,
cleanup and post-checks. Verify actual platform/driver support and unavailable targets.
Flutter integration suites initialize IntegrationTestWidgetsFlutterBinding and use
testWidgets where the selected harness requires it; flutter drive additionally needs
the matching integration driver. Do not infer a platform matrix from a tutorial.
