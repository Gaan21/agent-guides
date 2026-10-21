# Time, authentication and supporting test helpers

Dependencies: [testing](testing.md), [test quality](test-quality.md).
Helper names, signatures and namespaces come from the project; no runnable APIs
are defined here. Understand/adapt existing helpers instead of duplicating them.

- Time-dependent services/validators inject a controllable clock. Use explicit UTC
  instants for deterministic temporal tests; do not read real wall time in domain
  validation. No fake-clock requirement for behavior unrelated to time.
- Replace the clock in test DI and isolate/reset mutations of a shared clock. A
  factory date is product policy, not a universal calendar. Proposed configurable
  factory constructors must not be described as already implemented.
- Generate auth tokens with test-only key, issuer, audience, claims and expiration
  matching test validation; do not hardcode bearer tokens or use real secrets.
  Test no-token, malformed/expired, insufficient role/resource permission and allowed
  access separately. Do not infer a role/ownership contract from generic examples.
- Create isolated configuration for helper tests, keeping real connection strings
  and secrets out. Register helper dependencies only where needed.
- Bounded async waiting must have an explicit timeout, meaningful condition and
  appropriate cancellation; do not turn a wall-clock polling snippet into a
  deterministic domain clock contract. Use the project's supported helper API.
- Reuse documented helpers in a shared location, with tests of their actual behavior.
  Recipe availability is not evidence of successful integration or installed behavior.
