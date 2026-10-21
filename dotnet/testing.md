# Testing boundaries, fixtures and diagnosis

Dependencies: [architecture](architecture.md), [test quality](test-quality.md).
Time/auth/config helpers additionally require [helpers](test-helpers.md).
See [official references](references.md) for facts; this is not a runnable recipe.

## Selected suite contract

Preserve the project's approved provider and suite strategy. If it has selected
SQLite-only integration tests, retain that condition; do not add a second provider,
replace the suite, mock its DAO pipeline or generalize the choice to all .NET work.
SQLite is relational but not SQL Server: translation, collation, types and functions
differ. Do not claim a percentage of production parity or coverage of provider-only
features. Separate real-provider E2E remains future-only unless explicitly approved.

Unit tests may mock DAO interfaces for service logic or service interfaces for
controller logic. Full-pipeline integration uses actual DAO implementations against
the selected test DB, not hardcoded lists. Never test against production/development DB.

## Factory and service-provider access

Factory Server/Services/client access can initialize the host lazily; a factory
constructor alone does not prove the application is started. Configure dependencies
before host construction. Do not reenter factory Services from host-building callbacks.
For the same ordinary TestServer-backed factory, factory Services and Server.Services
provide the associated application's root service provider; neither creates per-test
DB isolation. Distinguish the provider from scopes and scoped DbContext instances.
Do not claim identity across customized factories, overridden getters or other
hosting modes, nor diagnose missing data from the property spelling alone.
An independently built service provider can diverge from the application's provider.

## Fixture lifetime and SQLite

- A new xUnit test-class instance is created for each test. A class fixture is shared
  among tests in that class; a collection fixture can span multiple classes.
  New test objects do not reset a shared fixture/database/clock.
- Test-class construction precedes its async initialization; cleanup follows the
  test. Async lifecycle interfaces differ by xUnit version; use the installed contract.
- Under xUnit's usual collection-parallel mode, tests in one collection run serially,
  and different collections may run concurrently. Runner/version/configuration can
  change behavior; inspect actual scope rather than assuming all tests are parallel
  or serial. Assembly-wide serialization also affects otherwise independent units.
- A private in-memory SQLite DB normally lasts as long as its owned open connection.
  Open before participating contexts/requests use it, keep it alive for the intended
  fixture/test lifetime and close only after users finish. Reopening a private memory
  connection loses prior schema/data; named/shared modes have different semantics.
- Shared mutable DB state must not race. Preserve adopted serialization or isolation;
  isolated class fixtures still need isolation between methods sharing that fixture.
  Independent factories are not automatically independent if they share external state.
- For the adopted disposable SQLite suite, use EnsureCreated without migrations;
  avoid EnsureDeleted/rebuilding schema on every seed. Persistent databases retain
  their migration contract. Verify foreign-key enforcement explicitly.

## Seeding, cleanup and failures

Factory owns provider replacement, test environment, connection lifecycle and any
lazy schema helper. A seed helper can own schema creation, SaveChanges and tracker
clearing; callers must not duplicate those actions or bypass an uninitialized schema.
Use per-test unique markers and generated IDs retrieved from persisted rows, not
fixed/random guessed IDs. Seed resources when permissions/happy behavior need them;
pure validation or authentication failures need no unrelated data.

Shared mutating tests clean only owned rows/touched tables in FK-safe order with
reliable lifecycle cleanup. Avoid global seeds, order dependencies and indiscriminate
deletes. Fresh per-test state/read-only scenarios may not need the same cleanup;
document the actual fixture lifetime rather than asserting class scope isolates methods.

For missing table/data: inspect connection/schema, provider registration, actual DAO
and seed IDs. For suite-only flakes: inspect shared state, cleanup and concurrency.
For slow tests: inspect repeated schema creation and excessive cleanup, then measure.

## Real-provider reference boundary

Future real-provider E2E requires an explicitly dedicated test DB, external secrets,
safe owned-row cleanup, generated IDs/markers and verified transaction participation.
Do not use schema deletion/creation or mass cleanup against real shared databases.
Preserve any adopted rollback requirement, but TransactionScope around a test is
not proof that HTTP request writes enlist. Async flow, server execution context,
connection/provider behavior and platform support must be established separately.
A seed-only rollback canary proves no more than its exercised seed path. No runnable
HTTP rollback guarantee, infrastructure or test-strategy change is supplied here.
