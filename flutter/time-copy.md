# Time and localized copy

Applies to timestamps, civil dates, formatting and user-visible text. Required:
[failures](failures.md); [layers](layers.md) for serialized boundary changes.

- Separate current-time acquisition, persisted instants, civil/date-only values and
  display timezone. Use an injectable/testable clock seam; verify its actual zone.
- Preserve the consumer's instant serialization contract, including UTC where
  selected. Device-local conversion is not a business/company timezone converter.
  Keep backend-resolved reporting/admin exceptions explicit.
- Epoch milliseconds identify an instant independently of display zone; an extra
  UTC conversion is not needed merely to read that value. Civil dates need explicit
  scope, not blanket UTC conversion of every date constructor.
- Do not treat local picker values as already-UTC instants. Missing business-time
  authority blocks contract-changing work; never invent a company timezone/helper.
- Test device/business-zone differences, midnight, DST, date-only boundaries and
  serialization round trips with controlled time, not names or redundant syntax.
- User-visible copy uses the selected localization resources and stable error-code
  mappings, not technical exception messages. Keep placeholders/argument meanings
  valid across every supported locale.
- Do not mix localization systems or silently migrate keys/argument conventions.
  Preserve existing legacy or generated-code selections; ask on conflicting systems.
  Named argument constants and typed generated methods follow the installed API.
- Verify translated errors, fallback/default behavior and missing-key/placeholder
  checks. A lint recognizing a literal does not prove localization completeness.
