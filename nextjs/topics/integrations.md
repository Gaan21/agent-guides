# Conditional local integrations

Read only for integrations actually adopted by the project/task. Selection of this
Next.js bundle does not require adopting every technology below or selecting another
bundle. Required local baseline: [boundaries](boundaries.md),
[server security](server-security.md), [env](env.md), [quality](quality.md),
[reads/cache](reads-cache-mutations.md). Native ownership/contracts still prevail.

## OpenNext, Cloudflare Workers and Wrangler

For a project targeting Workers through `@opennextjs/cloudflare`, retain that runtime
decision and use Next.js's Node.js runtime model, not an assumed Edge-first switch.
This names the Next runtime mode, not a full Node process or all Node APIs inside
Workers. Verify the exact adapter/framework/runtime support and required bindings.
Do not infer feature support from a generic Edge label or current documentation alone.

Runtime-affecting changes require the project's target preview (`pnpm preview` in
the adopted script convention) or its authorized Wrangler runtime verification.
Check existing local Wrangler, declared configuration and bindings on failure;
do not install or modify them just because a guide mentions them. Compatibility
checks are not deployment authorization. Respect platform limits and local gates.
Review on adapter/runtime changes; no automatic upgrade or latest resolution.

### Binary HTTP bodies

Choose a Response body representation accepted by the actual target's runtime and
type declarations. Preserve exactly the intended visible byte range, including
byte offset and byte length. A view may expose only part of a larger backing buffer;
replacing it with the entire backing buffer can send unrelated bytes or secrets.
Using the backing buffer directly requires proof that the visible range is the
entire intended buffer and that its actual buffer kind is accepted by the target.
Otherwise use a target-supported representation/copy restricted to the intended
range. A type assertion neither checks these facts nor converts/copies the bytes.
Do not prescribe a backing-buffer cast as a generic fix for BodyInit type errors.
Check compiler/declaration versions separately from runtime behavior. Tests must
include offset/short views and unwanted-prefix/suffix exclusion where relevant.

## Supabase consumption

Where Supabase is adopted, `supabase-js` is the selected main data client and
Supabase Auth supplies current session identity. No direct scattered SDK calls in
UI/pages: use local/shared server data functions with normalized responses/errors.
RPC is justified by atomicity, complex SQL, performance or domain security, not
the default for simple operations. A public anon key goes client-side only when
strictly necessary; service-role keys always remain server-only.
Consuming a provider never grants schema/migration/config ownership. Respect native
owner contracts and approved test environments; escalate structural work to the owner.
Keep future provider/backend evolution possible without exposing SDK details.

## next-intl v4

Where the project adopts next-intl v4, retain its one-library translation strategy.
Do not introduce competing i18n libraries or switch locale routing/configuration
without an explicit decision. Product base/supported locales, persistence and route
shape remain authoritative local policy; this bundle does not replace them.

Read that policy before editing messages. Use nested namespaces and camelCase keys,
with at most two levels for simple cases. The chosen base catalog defines keys:
add there first and update every supported locale in the same commit. Never hardcode
UI text in place of messages or add keys only to one locale.
RSC uses `getTranslations` from next-intl's server API; client components use
`useTranslations` with the project provider. The root layout gets locale/messages
server-side and passes messages to `NextIntlClientProvider`, setting the one root
HTML language. Do not add another html-lang element or manual head for i18n.
Locale changes must respect the adopted server persistence/validation policy;
do not copy an unchecked setter from an example.

Missing secondary keys and orphan keys are blocking errors; unused keys start as
visible nonblocking warnings. Making unused keys blocking is a separate explicit
strictness decision, not an assumed script flag. Message changes and i18n-flow
changes require the project's actual consistency check plus typecheck/build and
the remaining base gates. Retain the required CI blocking behavior; do not fabricate
script availability or workflow execution from documentation.

For Workers/OpenNext targets, keep rendering dependencies compatible with the
actual target; do not assume all Edge-compatible code has identical deployment
support. Check server request configuration, async request APIs and bundled message
assets, and run target preview when introducing i18n dependencies. Current upstream
guidance is not installed-version or successful-bundle evidence.

## React/TypeScript, Tailwind/shadcn and external testing references

React composition must preserve local feature ownership and minimum server/client
boundaries. TypeScript complexity must reduce actual domain risk. Neither external
best-practices nor upgrade recommendations override adopted architecture.
Tailwind/shadcn work starts from existing components and visual system. External
patterns are support, not universal templates. Global components/styles require
justified impact; systemic theme/setup changes require explicit local approval.
Tailwind-v4/shadcn advanced theming references apply only when that combination is
actually adopted; they do not prove an installed version or authorize replacement.

Playwright references apply to E2E flakiness/retries/browser/CI questions; retain the
local risk matrix, no unapproved global requirement expansion. Vitest references
improve pure-logic tests without unjustified extra scope. Accessibility contrast
applies to forms, keyboard, semantics and contrast while preserving local design
and approved task scope; record actionable high/medium/low findings. Performance
changes follow real flow risk and bottleneck evidence, not speculative restructuring.
Use [reference policy](../references.md); no external skill autoload or installation.
