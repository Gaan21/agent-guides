# Localization

For any product with user-facing text, in any stack or localization system. Covers
what must be translated, how to write code that stays translatable, and the evidence
that a change is covered. Not a framework manual: the stack bundle and the project's
own contract say which files, tools and languages apply.

## Always

- No change introduces untranslated product text in the outputs it creates or
  changes. Every product text reaches its consumer in each supported language, in
  the effective language chosen for that screen or request.
- Product text comes only from the project's localization system. Never fall back
  to the base language or to a technical key when a translation is missing.
- Logs and internal errors are written in one technical language (English) and are
  never shown. An error that can reach a person carries a code that the UI turns
  into its translation; unknown codes also get a localized, safe output.
- A legitimate literal in code is justified on the line before with
  `i18n-ok: <reason>`. A justification is not a general exception.
- Do not lower a check, delete keys or fabricate references to make a report pass.
  A pre-existing defect outside the scope is reported, not silently fixed or hidden.
- If the project or its localization system is not covered by the available
  checks, stop accepting the affected change and ask; never assume there is no
  localization.

## Read for the affected work

| Work | Required detail |
| --- | --- |
| Adding or changing text, error codes, translators, helpers, language selection or consumers | [Coverage](topics/coverage.md) |
| Choosing tests, closing a doubt, or reviewing a localization change | [Evidence](topics/evidence.md) and [Coverage](topics/coverage.md) |

Read the detail before the affected change and reuse it while in context. Ordinary
changes without user-facing text need no localization reading.

[Inventory](INVENTORY.md) · [License and notices](NOTICE.md)
