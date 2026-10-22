# Flutter engineering

Applies to Flutter/Dart work in the selected scope. Read native project/folder
authority and task contracts first. Existing architecture, lint selections and
exceptions remain authoritative; selecting this bundle installs no executable lint.
Implementation and review share one retained project/source/selection identity;
never independently resolve latest or edit a live guidance snapshot.

Always preserve layers, strict class-containing names, member order and selective
typing; public domain operations return Result, while infallible getters/internal
calculations return direct values. Preserve immutable values, explicit ownership,
visible failures, localized copy and awaited critical completion.

Read relevant topics and their required dependencies **before applicable work**.
Reuse text still in context; read new topics as scope changes or context is lost.
After compaction or a summary, reread topics needed for the next edit unless their
actual text remains visible in context; topic names or read-history are not enough.
No all-topic or per-patch reading is required.

| Work | Required local reading |
| --- | --- |
| Names, declarations or API changes | [Conventions](conventions.md) |
| Entities, use cases (any use case, including validation-only), repositories, sources, mapping or DI | [Layers and values](layers.md), [Failures](failures.md) |
| Presentation: ViewModels, state, actions, screens, navigation, themes or settings | [UI](ui.md); [Resources](resources.md) and [Operations](operations.md) for lifecycle/async work |
| Controllers, streams, dialogs, forms or disposal | [Resources](resources.md), [Operations](operations.md) |
| Async work, retries, authentication or completion | [Operations](operations.md), [Failures](failures.md) |
| Offline storage or synchronization | [Offline](offline.md), [Operations](operations.md), [Failures](failures.md) |
| Dates, localized copy or diagnostics | [Time and copy](time-copy.md), [Failures](failures.md) |
| Tests or validation (including test-only edits) | [Testing](testing.md), [Verification](verification.md), and the affected topic's requirements |
| Guidance updates or control claims | [Verification](verification.md) |

Missing required local APIs/contracts block affected implementation: report the
gap, do not invent interfaces or fall back to retired loading/scripts. Consult
[upstream](references.md) only for unresolved decisions; stop when resolved.

Factory work defers branches, tools, checks, PRs and publication to its host flow.
Manual validated closure performs scoped commit/push on the agreed branch without
another prompt; missing/failing mandatory checks block closure and commit/push.
Clarify unknown mode/authority. This is not release, deployment, consumer migration,
new lint activation or private-content publication authorization. Suppressions and
policy changes need explicit approval. Preserve working consumer delivery.
