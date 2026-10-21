# Audit and references

Applies to periodic audits (quarterly by default, scheduled by the owner), after
major guidance changes, on inconsistencies between guidance documents, when adding
examples, and on fragile or broken references. Depends on the [entry](../ENTRY.md)
rules and [authoring](authoring.md) for the one-source rule.

## Audit checklist

- **Duplicates:** none unresolved. Keep content in its owning document and
  reference it elsewhere; document real variants and when each applies.
- **Examples:** verify each against an official source and record source, version
  and date, or mark it explicitly pending with the reason. Never copy an example
  without checking the current version/API. Valid sources: official documentation,
  official tools, release notes; not blogs or Q&A sites. Prefer replacing a doubtful
  example with original prose and an official link.
- **Terminology:** credentials, keys and tool names follow the current guidance of
  the owning stack bundle.
- **References:** see below.
- Record the audit as complete or partial, with pending items. Do not run legacy
  audit, sync or autofix scripts; no automatic rewriting.

## References and links

- Link complete files, not fragile in-document anchors. Name the target section in
  text, for example: [Authoring](authoring.md), section "One source of truth".
- Same-document references name the heading instead of linking to it; tables of
  contents list section names.
- Relative paths are correct from the referring file; every target exists; link
  text describes the content.
- Validate links with the bundle engine. It checks local files and declarations,
  not section names or every textual reference, so check those during review.

## Delta audit against upstream

1. Select critical guidance and its scope.
2. Map the local rule against the official upstream source.
3. Classify status: current, current but incomplete, misaligned or obsolete.
4. Tag drift: conscious local decision (intentional, documented divergence) or real
   drift (unintentional or undocumented divergence).
5. Define the minimal action: keep, add a context note, update or deprecate.
   Record risk, last verified date and next review trigger.

- Precedence: critical local invariants (repository, security, ownership), then
  local stack/runtime/tooling guidance, then local reference notes, then official
  external references (technical reference only). The most specific and
  restrictive security/ownership rule prevails.
- External references are never final authority or entry points. A guidance entry
  that declares external material as its entry point is real drift: fix the entry.
- Consumers do not write a central register; records live with the guidance source.
  Historical registers are evidence, not current status.

## Completion

- Audit recorded; duplicates resolved or explicit; examples verified or pending;
  no fragile anchors; every referenced file exists; change recorded.

References: [Diátaxis](https://diataxis.fr/),
[Google technical writing](https://developers.google.com/tech-writing).
