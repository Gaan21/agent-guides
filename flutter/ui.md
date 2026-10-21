# UI state, composition, navigation and settings

Applies to widgets, VMs, screens, routes and global UI preferences. Required:
[resources](resources.md), [operations](operations.md), [failures](failures.md).
Use [time and copy](time-copy.md) for localization/theme-facing text and dates.

## State and responsibilities

- Separate persistent typed render state (initial/loading/data/empty/error) from
  ordered one-shot effects. Verify no effect replay on rebuild and preserve prior
  data during refresh/error where the product contract requires it.
- Keep domain rules and I/O orchestration out of widgets. Simple formatting,
  visibility, animation, layout and approved routing remain UI concerns. VMs do not
  own BuildContext or UI resource types; preserve native base/infra exceptions.
- Do not wire VMs to other VMs or auxiliary UI-state owners where prohibited.
  Pass typed presentation values/callbacks or approved shared notifier/stream
  services with explicit lifetime. Avoid hidden provider lookups and cycles.
- Resolve the project's top-level screen/shell/base contract before optional complex
  search/filter composition. Availability of generic guidance does not replace bases
  or authorize ad-hoc chrome. Add auxiliary state only when it has real value.
- Shell chrome/actions have explicit owners; tabs publish contextual state without
  coupling shell to concrete VMs. Register/update through the selected lifecycle,
  not state mutation in build. Prevent repeated taps opening duplicate overlays.
- Compose providers in actual dependency order and with clear ownership. Preserve
  selected ordering/single-composition/no-nesting restrictions and state isolation.

## Rendering, identity and routes

- Maintain stable identity keys through list insert/delete/reorder. A fresh unique
  key or position is not stable business identity; static-list exceptions need an
  actual invariant. Constructor-key presence alone proves little.
- Subscribe where updates are needed. Consumer/watch versus Selector/select follows
  dependencies and representative profiling, not a blanket performance claim.
  Precompute genuinely expensive domain-derived collections outside repeated build.
- Use installed design tokens, semantic theme extensions and route/localization
  systems. Pass approved styles to components without context; avoid global theme
  access. Verify SDK APIs before migrations; no universal breakpoint/route quota.
- VMs emit selected navigation effects; the approved UI handler executes them.
  Use the actual router/registry and typed path/query inputs. Each selected go_router
  route needs a builder/pageBuilder/redirect rather than an empty grouping route.
- Choose go versus push from back-stack/deep-link/modal semantics and the installed
  route contract, not a percentage quota or universal claim about URL behavior.
  Verify back/pop interception, deep links, repeated effects and save completion.

## Infrastructure preferences

- Theme/locale/settings can have app-wide lifetimes distinct from domain VMs.
  Preserve root ownership, persistence/default/error policy and selected DI exception.
- Theme/locale changes should update subscribed widgets without accidentally resetting
  router/tab/scroll state. A locale key that recreates navigation is not a generic fix.
- Test initialization, unchanged-value notifications, storage errors, persistence,
  restart where required, per-item updates and tab-state retention. Do not force
  every product to offer a particular settings button, locale set or storage library.
