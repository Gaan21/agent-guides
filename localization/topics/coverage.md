# Localization coverage

Applies when changing texts, error emitters or codes, translators, helpers,
language selection or consumers, and when resolving a doubt raised by a check.
Depends on the [entry](../ENTRY.md). Technology-neutral: it does not require ARB,
JSON, ICU, a given library or the same system in every project.

## What counts as product text

- Screens, titles and metadata, labels, hints, accessibility text, validations,
  notices, operating-system prompts, notifications, reports, files and legal
  documents.
- Reports and downloads follow the effective language, including labels, titles,
  messages and the translatable parts of file names. Legal documents are shown in
  that language even when they live outside the catalog.
- Do not change time zones or business rules to translate a date or a report.
- Not translated by default: logs, telemetry, technical codes, routes, brand names
  and user-written content. This does not turn a product sentence, a file name or
  visible remote data into an automatic exception: justify each case in context,
  never with general lists by key, length, punctuation or folder.
- A backend technical error is never shown directly: convert it into a safe,
  localized message. Never show `message`, `toString()` or an interpolated error.

## Scope of the review

- Review the whole affected path, not only the changed lines: a shared component
  can affect several screens. Integrity checks cover the full declared resources;
  review and targeted tests focus on the impact of the change. No test per key and
  no full manual audit on every change.
- Before enabling an automated literal check on an existing codebase, review it by
  mechanism and justify the relevant destinations. Reuse that evidence only while
  its inputs, contract and consumers do not change.
- A doubt raised by an analyzer is not a confirmed product defect.

## What automation covers and what it does not

- Read the project's localization contract: supported languages, message format,
  content outside the catalog, language selection and existing checkers. It
  describes the product; it does not activate checks or authorize installing tools.
- Keep three controls apart: resource integrity, detection of visible literals and
  review of the path. Use the parser of the real format (ICU where it applies; do
  not read another project's simple translator as ICU). Check keys, empty values,
  parameters and syntax with the available checks and state their limits.
  Aligned catalogs or a correct generation step do not prove there is no text
  written outside the localization system.
- When reporting, separate errors, missing references, measured destinations and
  doubts. Passing tests, build, lint or generation do not mean a localization check
  ran. If one is missing, state that limit; do not install tools or change
  dependencies on your own. The task or host states which checks are active. An
  incomplete resolution does not show that a key is unused. Do not change scripts
  or configuration to weaken the control.
- A static reference does not prove the text is shown. Variables, callbacks,
  transformations, dynamic or remote codes and translators without a localized
  emitter may need specific tests. No auditor guarantees coverage of every path,
  linguistic quality or visual correctness. Do not replace a real path with a
  direct call to a translation or a generated getter.
- Without an explicit choice, the language may resolve to the product's supported
  default; that never justifies another language because a message or document is
  missing in the language already chosen.
