# Test organization and required checks

Dependencies: [testing](testing.md); for API coverage also [controllers](controllers.md).

- Use descriptive English Method_Scenario_ExpectedResult names and class-under-test
  names. Fact expresses a case; Theory expresses parameterized cases.
- Separate Arrange, Act and Assert, one behavior per test. No unrelated assertions,
  multiple unrelated Acts, conditional test logic or dependencies on execution order.
  Comments help longer tests; clear short tests need no redundant section banners.
- Assert public behavior, not implementation. Check HTTP status first, content type
  when relevant and specific payload semantics. One coherent behavior per test, with
  the assertions needed to verify it: no numeric assertion maximum and no literal
  single-assertion rule. Do not infer a count from examples.
- Organize unit and integration tests separately and by functional area; keep
  fixture/helper infrastructure shared. Split incoherent/large files for navigation,
  not as a universal task-size limit; do not fragment small cohesive tests.
- Cover applicable input validation, missing/invalid/expired authentication, denied
  authorization, absent resources/unexpected faults and successful empty/data/create
  behavior. Actual product roles/status contracts come from selected local policy.
- Before validated closure, the applicable build/tests must pass; report actual
  coverage and no unexplained skips/xUnit warnings or async-void tests.
- Verify connection lifetime, FK enforcement, selected parallelism, real DAO pipeline,
  unique persisted IDs, clock replacement for temporal tests, valid test-auth settings
  and cleanup for shared mutation. No debug Console output, unexplained commented
  code or orphan TODOs; record issues/justification. Document complex test intent,
  edge-case rationale and meaningful test groups.
- Coverage tooling is project/host-selected; no package installation or global check
  redesign is authorized. Missing/failing required checks block closure/commit/push;
  distinguish unavailable evidence from passing behavior. Factory owns its pipeline.
