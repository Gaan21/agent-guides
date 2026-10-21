# Resource ownership, overlays and teardown

Applies to controllers, streams, timers, subscriptions, forms and overlays.
Required: [operations](operations.md); [UI](ui.md) for state/route changes.

- Record creator, owner, borrowers, lifetime, transfer and teardown. Owners release
  every owned resource on normal teardown paths and perform required parent cleanup;
  borrowers never dispose external ownership. Verify inherited/helper cleanup.
- Preserve explicit resource-field annotations when selected cleanup detection needs
  them. Review inferred/alias/multiple fields, borrowed resources, inheritance,
  helpers, conditional paths and early returns: a close/super call is not all-path
  evidence. Keep local cleanup ordering requirements.
- Do not put lifecycle resources into mixins/static resource registries under the
  selected architecture unless an approved local exception provides safe ownership.
- Lifecycle-capable internal widgets may own resources when their lifetime requires
  it; a screen suffix alone cannot decide ownership. Preserve native screen bases
  and infrastructure/animation/hardware exceptions, not a universal stateless ban.

## Overlay lifetime and context

- Dialog/sheet resources survive their own lifecycle, including caller removal.
  Prefer a dedicated overlay StatefulWidget State that owns/disposes controllers,
  focus, animation and scroll resources. A caller-local controller/StatefulBuilder
  is not proof of safe overlay ownership.
- For inherited lookups use the overlay builder's context or plain values resolved
  before opening. Do not capture caller context for later overlay rebuild lookups.
  An after-await mounted check does not repair that separate lifetime problem.
- Dialog buttons return a result through the dialog builder's context. Await the
  dialog, check caller mounted, then invoke callbacks or follow-up effects. Coordinate
  later navigation with the route lifecycle.
- Give form exit one owner. Save completion, PopScope, callbacks and navigation must
  not produce duplicate pops. Preserve the product's choice whether successful save
  closes the form or leaves it visible; no universal interaction is imposed.
- Reusable search/filter, single-screen form and overlay resources have distinct
  possible owners. Follow actual lifetime/contracts, not a blanket move into VMs.

Test rapid close/reopen, autofocus, rebuild, caller removal, cancellation, parent
cleanup and post-disposal events. Async-gap mounted checks and sink lints cover
bounded predicates, not all lifecycle behavior.
