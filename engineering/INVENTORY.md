# Bundle inventory

Independent schema-1 engineering bundle. Selecting it does not select another
bundle, install tools or lints, change a consumer or guarantee model compliance.

| File | Applicability and local dependencies |
| --- | --- |
| ENTRY.md | Always: authority, always-on principles, mode boundary, reading conditions |
| topics/code-quality.md | Names, constants, duplication, abstraction, file growth, lint findings; entry |
| topics/boundaries.md | External data and responsibility placement; entry + code quality |
| topics/sources.md | Errors, external sources, dependencies, tools; entry |
| NOTICE.md | License, adaptation notice, external rights boundary |
| LICENSE | Complete Apache-2.0 license text |
| guidance-bundle.json | Exact file/notices declaration; no runtime selector |

Not applicable: read-only questions without code, guidance maintenance (a separate
bundle) and stack-specific gates. All requirements remain mandatory in their
scope, including exceptions. Numeric hints (duplicated lines, file length) are
signals, never budgets or limits. Missing guidance requires reporting the gap,
not inventing a workflow or weakening these principles.
