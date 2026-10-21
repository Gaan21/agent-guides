# Server/client boundaries

Applies to components, client directives, imports and data transfer.
Required: [architecture](architecture.md), [server security](server-security.md) for
data/mutations, [environment](env.md) for config and [reads](reads-cache-mutations.md).

Server Components are the default. A client directive needs an actual browser
runtime requirement: state/events, browser hooks/APIs or a client-only library.
Convenience, server-readable business data, or avoiding composition is not a reason
to convert a whole page/layout. Keep interactive leaves client-side and compose
them from server parents. Keep pages/layouts/domain wrappers/data blocks server-side
unless an actual scoped requirement justifies otherwise.

Review descendant imports: a client boundary pulls dependencies into its bundle.
Do not bring secret-bearing server modules, sensitive data access or heavy server
utilities into that tree. Do not mix interactive UI with server data access or move
data client-side to evade a boundary. Use `server-only` where applicable for sensitive
server modules, not as proof of authorization or data correctness.

## Minimum transfer

Pass small serializable props/DTOs containing only the fields required by the
client interaction. No full-object spreads, complete domain entities for convenience,
secrets, credentials/tokens/internal keys or unused sensitive fields. If a field is
not used by the client it must not be sent. Restrict on the server, not after delivery
to the client: users can inspect props/payloads.

Reads normally arrive from the server parent; an external endpoint is an exception
only when required by contract. Internal UI mutations call Server Actions; external
HTTP contracts use Route Handlers. Every operation still validates and authorizes
at its real server boundary. A layout or hidden control is not a permission check.

## Shared types and action modules

In a module marked with file-level `use server`, exported runtime values must be
async Server Functions. Do not export runtime constants, configuration objects or
synchronous helpers, including indirectly through broad value reexports. Do not
remove the directive to work around the action boundary.

TypeScript type-only declarations/exports are erased; they are not runtime values
or callable network actions. Do not describe `export type` or an interface as a
network-exposed function. Erasure does not establish compatibility with every
framework transform, lint rule or installed compiler version.

The adopted organizational convention remains separate neutral `<feature>.types.ts`
modules without the server directive. Both the action module and client import
their types from that neutral module; do not reexport those types through the action
file or import them from the action file in the client. This is an explicit
organization convention, not a claim that TypeScript types survive at runtime.
Actual Server Function imports for invocation are distinct from type sharing and
must follow the installed framework and native lint rules; do not invent a blanket
ban on the supported Server Function invocation mechanism.

Check real client need, smallest boundary, descendant imports, DTO fields and
neutral type ownership. Validate with the project's installed toolchain; see
[official references](../references.md) and [quality](quality.md).
