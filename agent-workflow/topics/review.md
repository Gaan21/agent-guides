# Independent review

Use when the owner requests or accepts independent review of implemented work.
Depends on [reading](reading.md) and [validation](validation.md). Factory review
is authoritative: do not launch a second reviewer or mandate a subagent/tool/model.
Otherwise offer review where useful; the owner decides whether and how to run it.

## Inputs and boundaries

- Review cold: reconstruct the expected behavior from acceptance, non-goals,
  applicable local instructions, the complete change set and validation evidence,
  not the implementer's chat memory. Retain the same guidance/task identity.
- Include staged, unstaged and untracked relevant files and the implementer's
  summary. Use the host's evidence location or supplied summary, not a compulsory
  new handoff file. Missing inputs are findings, not permission to guess.
- Detect each affected stack from actual paths. Read its entry and relevant topics
  and dependencies; verify its gates against named evidence. Explain legitimate
  non-applicability, such as documentation-only changes, rather than inventing tests.
- Review all affected surfaces, their coordination and contracts. Multiple stacks or
  surfaces are not themselves defects: no automatic Medium finding. Report concrete
  defects with severity justified by their actual risk.
- Declare inaccessible necessary evidence unverified; missing obligatory verification
  blocks affected acceptance. Do not invent a finding severity or approve blindly.
  Factory retains authority over assignments, checks, review and closure; introduce
  no duplicate pipeline.
- When behavior may change, consult the product's required knowledge/help/disclosure
  and closeout contract through its entry and smallest relevant slice. Missing
  required product authority needs a human decision; do not assume an exemption.
- Review is report-only: no fixes, writes, staging, commits, branch/PR/remote changes
  or external system mutations. Do not inspect real customer data. Use only authorized
  read-only evidence; tool availability does not grant live data access.

## What to assess

- Compare behavior and changes with acceptance and non-goals. Verify permissions,
  data integrity, failure visibility, time, synchronization and other applicable risks.
- Verify each required stack gate's command, scope and actual result. An implementer
  summary missing a gate is a validation gap unless documented non-applicability holds.
- Check applicable product closeout requirements precisely; do not infer missing
  declarations from a diff or auto-correct a classification for the implementer.
- Keep implementation defects separate from suspected stale, contradictory or
  excessive guidance. Do not block on stale guidance without a concrete risk;
  explain the concern and propose the smallest owner-controlled follow-up.
- Include independent judgment even when no guideline covers the issue. Missing
  required inputs warrant a high-severity finding and a human-decision verdict.
  For verification evidence gaps, use the acceptance boundary above instead of an
  automatic severity; the missing scope/change-set/authority input rule still applies.

## Offer conditions, not task limits

Useful signals: behavior/copy meaning, permissions/auth/isolation, migrations,
backend functions, compliance/reporting, or changes across surfaces. A large diff
may justify an offer but sets no numeric task cap or forced split. An explicit
request remains sufficient. Normally skip unsolicited offers for isolated literal
translations, format/lint-only changes, behavior-neutral dependency bumps or purely
mechanical refactors with unchanged tests; do not skip semantic risk because a diff
is small. Product-specific triggers and exceptions remain with local authority.

## Report

Use the host's required format. Otherwise report:

- Findings: severity, concrete issue, file/section or line reference.
- Acceptance: pass/partial/fail and what is missing or outside scope.
- Guidance: relevant slices read, compliance and separate drift concerns.
- Applicable product-contract checks: actual outcomes, gaps and non-applicability.
- Validation: commands/evidence, per-stack gates, missing or unverified checks.
- Independent judgment: concerns beyond written rules, or explicitly none.
- Verdict: approve, changes requested, or needs human decision.

The report is evidence for the owner/host, not an automatic fix, merge, publication
or acceptance action. Never disguise unverified checks as passes.
