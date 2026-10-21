# On-demand upstream references

Original navigation notes; external works are linked, not bundled. Open only the
reference relevant to an unresolved decision; stop when resolved. Preserve upstream
DO/PREFER/CONSIDER and conditional strength. Project restrictions may be stricter;
references do not override native contracts or activate executable controls.

| Topic | Official reference | Caveat |
| --- | --- | --- |
| Style/types/errors/async | [Effective Dart](https://dart.dev/effective-dart) | Inference retains static typing; formatter is not architecture review |
| Lint dependency/include | [flutter_lints](https://pub.dev/packages/flutter_lints) | Dependency, include, effective configuration and execution are separate |
| Async-gap context | [use_build_context_synchronously](https://dart.dev/tools/linter-rules/use_build_context_synchronously) | Does not prove overlay rebuild lifetime safety |
| Future consumption | [unawaited_futures](https://dart.dev/tools/linter-rules/unawaited_futures) | Not background criticality/error ownership or suppression approval |
| Sink cleanup | [close_sinks](https://dart.dev/tools/linter-rules/close_sinks) | Bounded detector, not every ownership/control-flow path |
| Architecture | [Recommendations](https://docs.flutter.dev/app-architecture/recommendations) | Domain/separate models conditional upstream; preserve adopted layers locally; no universal generator |
| Responsibilities | [Architecture guide](https://docs.flutter.dev/app-architecture/guide) | Upstream service is not automatically an installed DataSource/base API |
| Test levels | [Testing](https://docs.flutter.dev/testing/overview) | Cost/confidence, not numeric quotas |
| Offline strategies | [Offline-first](https://docs.flutter.dev/app-architecture/design-patterns/offline-first) | Not an actual outbox/auth/company-time protocol |
| Dialogs/lifecycle | [showDialog](https://api.flutter.dev/flutter/material/showDialog.html) | Verify context, result and actual installed API |
| Pop interception | [PopScope](https://api.flutter.dev/flutter/widgets/PopScope-class.html) | Preserve selected save/exit behavior |
| Integration harness | [Integration tests](https://docs.flutter.dev/testing/integration-tests) | Explicit request and verified consumer matrix/driver |
| Localization | [Internationalization](https://docs.flutter.dev/ui/accessibility-and-internationalization/internationalization) | Preserve selected resources and migration authority |
| Companion controls | [Dart architecture lints](https://github.com/Gaan21/dart-architecture-lints) | Guidance selection does not install or enable a linter |

Legacy source navigation recorded consultation on 2026-10-14. This adaptation did
not access these pages anew; links are mutable, no current availability/API/release
equivalence claim is made. Verify installed-version APIs with dated evidence when
needed. No page SDK label requires an upgrade and no vendor enabled-all set is given.
