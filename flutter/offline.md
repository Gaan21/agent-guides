# Offline contracts, only when selected

Read for existing/approved offline or synchronization work, not online-only features.
Required: [operations](operations.md), [failures](failures.md), [layers](layers.md),
[time](time-copy.md). Do not extend offline behavior without a product decision.

- Choose read/write/sync strategy from requirements. Preserve selected local truth
  and UI-local reads; online-only and local-first features need not share strategy.
- Durable local writes need operation identity/idempotency, metadata, pending/error
  visibility, restart recovery and explicit acknowledgment/merge rules. Await durable
  local acceptance before reporting it, while distinguishing remote confirmation.
- Preserve pending local changes during remote merges. Use approved version or
  modification-clock semantics, never sync bookkeeping time as the conflict clock.
- Keep deletion evidence/tombstones and pending state until confirmed acknowledgment.
  A failed remote Result must not be ignored then replaced with synthetic success.
- Use transactions for required atomic batches/merges and recovery. Actual IDs,
  outbox fields, operation order, indexes, WAL, pagination, retention and maintenance
  require selected storage/protocol contracts and measured configuration.
- Test rollback, pending restart/merge, failed delete acknowledgment, skewed clocks,
  reconnect/auth failure and visible error recovery. Never copy a sample that clears
  pending state after merely awaiting a failed nonthrowing result.
- Check service reachability, not just network-interface status. Captive portals,
  probe endpoints/timeouts/budgets and cautious failure behavior follow the product;
  no universal external probe service or network permission is introduced here.
- Coordinate sync/auth through approved owners; prevent overlapping periodic cycles,
  release timers/subscriptions and expose pending/syncing/synced/error state as
  required. Retry success means actual accepted outcome, not absence of an exception.
- Background sync is noncritical only after the operation's accepted durable write;
  its failure still has an owner and visible pending/error policy. Do not discard
  a critical write or hide required completion behind background scheduling.
