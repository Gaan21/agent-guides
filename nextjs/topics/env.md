# Environment, configuration and secrets

Applies to new/changed environment variables, configuration, bootstrap and exposure.
Required: [boundaries](boundaries.md), [server security](server-security.md),
[reads/runtime](reads-cache-mutations.md), [quality](quality.md).

Classify server/private, client/public and build/runtime behavior configuration.
New variables start server/private. `NEXT_PUBLIC_*` requires a real functional client
need, no secret/privilege escalation and acceptable visibility to every inspecting
user. Such values are embedded in the client bundle; do not treat them as secrets
or assume dynamic runtime changes alter an already-built public value.

If a feature works with a server-calculated/injected value, do not make it public.
Do not expose URLs/keys/flags for convenience, hardcode base paths/flags in components
or expand client payloads with unused configuration. Public values cannot implement
a permission boundary.

Centralize reading/parsing in a small server env module, for example `src/server/env/`.
Direct access is allowed there and in applicable runtime bootstrap/config; not
scattered across routes/components or feature modules bypassing the layer. Mark
secret-bearing server env/wrappers `server-only` where applicable.

Validate presence and shape of critical variables on loading that module. Missing
or malformed critical configuration fails fast with a clear server error; no silent
fallback or catch-and-continue unsafe state. Validate what security/operation needs
without building a huge speculative schema.

Never deliver service-role keys, internal tokens, third-party credentials, webhook
signing secrets or write/admin keys in client code, payloads or logs. Error/fallback
messages must not leak env values. Conditional provider key rules are in
[integrations](integrations.md); provider isolation does not waive these duties.

Keep env/config an app/orchestration boundary, not a permanent provider contract.
Provider configuration/wrappers stay behind server modules rather than propagating
vendor details across the feature tree. Runtime decisions or correct auth do not
justify exposing secrets. Check startup/fail-fast behavior and exposure, not just types.
