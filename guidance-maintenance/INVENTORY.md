# Bundle inventory

Independent schema-1 guidance-maintenance bundle. Selecting it does not select
another bundle, install tools or lints, change a consumer or guarantee model
compliance.

| File | Applicability and local dependencies |
| --- | --- |
| ENTRY.md | Always when selected: scope, invariants, mode boundary, reading conditions |
| topics/authoring.md | Writing/changing guidance, structure, consumer findings; entry + linter impact |
| topics/audit.md | Audits, duplicates, examples, references, upstream drift; entry + authoring |
| topics/rights.md | Third-party material, licenses, notices, public output; entry + authoring |
| topics/lint-impact.md | Every guidance change and every companion-linter change; entry + authoring |
| NOTICE.md | License, adaptation notice, external rights boundary |
| LICENSE | Complete Apache-2.0 license text |
| guidance-bundle.json | Exact file/notices declaration; no runtime selector |

Not applicable: ordinary product or code tasks that do not change guidance. All
requirements remain mandatory in their scope, including exceptions. Missing
guidance requires reporting the gap, not inventing a workflow or weakening rules.
