# Failures, visible outcomes and diagnostics

Applies to results, validation, RPCs and reporting. Required: [layers](layers.md)
for boundary changes; [time and copy](time-copy.md) for user messages.

- Preserve the selected Result/AppException-style protocol and stable localized
  error identifiers. Exhaustively consume success and failure. Never turn failure
  into silent null/empty data or synthetic success; await failed nonthrowing Futures.
- Inspect inherited methods, capture boundaries and generic ordering. Distinguish
  expected operational/validation failures from programmer defects according to
  native debug/release policy. No lexical detector proves a call chain cannot throw.
- Internal conversion/rethrow behavior follows the installed guard contract; public
  failures retain typed outcomes. Do not invent universal no-throw guarantees or
  catch all defects merely to satisfy a signature.
- Preserve original diagnostic context, specific failure type and stack trace when
  adapting errors. Avoid repeated wrapping that erases a specific mapping/validation
  failure. Do not duplicate ad-hoc try/catch when an approved boundary owns capture.
- Transport success is not business acceptance. Check the actual server rejection
  envelope, including absent/malformed success fields, stable codes and reason
  semantics. Do not copy unverified RPC helper names or backend formats.
- One visible error owner per action: persistent error state, ephemeral effect or
  approved background status. Preserve stricter native mandatory-effect rules;
  do not compensate for hidden failures with duplicate widget toasts/reporting.
- Technical exception messages are not user copy. Resolve approved stable codes
  through the installed localization system and verify arguments/translations.

## Diagnostic ownership and confidentiality

- Assign one reporting owner across source→repository→domain→UI. Preserve legitimate
  technical events separately from already captured failures. Global error handlers
  must not silence critical defects; use the actual installed reporting API.
- Use structured, deterministic context and redacted metadata. Keep secrets,
  credentials and sensitive personal data out of messages and nested/dynamic fields.
  A literal-key check or replacing print with a logger does not establish privacy.
- Verify local versus remote levels, allowlists, deduplication, rate limits and sink
  behavior. Filter valueless ephemeral/unknown navigation events where selected.
  Exact logging receivers, canonical scopes and budgets are project contracts.
- Test one-report behavior, stack preservation, server rejection, translated errors,
  nested redaction and remote routing. Detector registration is not executed proof.
