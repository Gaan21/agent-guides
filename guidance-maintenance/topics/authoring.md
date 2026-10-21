# Authoring and changing guidance

Applies when creating or changing guidance content. Depends on the
[entry](../ENTRY.md) rules and always on [linter impact](lint-impact.md); read
[rights](rights.md) for material not originally authored by the owner and
[audit](audit.md) for references and examples.

## Audience and language

- Audience: agents and developers. Not end-user help, product documentation or
  help-center content.
- Written guidance is English regardless of the host repository's language policy.
  Conversation may use any language. Existing non-English files are not
  retroactively translated as a side effect.
- Concise: every sentence carries information an agent or developer needs; no
  padding or redundant context.

## Structure

- Short entry: scope, authority, always-on invariants and a conditional reading
  table. Detail lives in topics read on demand; never require reading every topic
  or rereading per patch.
- Each topic states when it applies, its scope, required dependencies and useful
  non-applicability boundaries. Critical rules first, then procedure, completion
  criteria and references.
- Reference long detail instead of duplicating it. Split a document that grows
  into separate responsibilities and respect the repository's file-size rules.
- One self-contained bundle per selectable unit, with a declaration listing every
  file and its notices. No cross-bundle dependency mechanism, runtime selector,
  auto-invocation metadata, sync script or loader directive.
- Metadata and indices organize documents; they do not guarantee native loading
  or invocation. Do not claim enforcement from generated files.

## One source of truth

- One pattern, one owning document. Others reference it; never keep duplicates
  "just in case".
- Real variants: document the differences and when each applies.

## Recording changes

- Compare meaning, conditions, exceptions and modality, not only hashes or ranges.
- Record each moved or changed rule: source, destination, retained meaning,
  verification and any owner decision for a removal or weakening. Detailed
  classification evidence stays in the private maintenance record.
- Update the repository's change record or notice revision line where it keeps one.

## Consumer findings (proposal only)

- Report only concrete findings met during normal work; no extra review pass or
  empty report per task.
- Include the guidance identity in use (source revision), rule file and section,
  observed evidence, impact and classification: violation, contradiction, obsolete
  rule, duplication or excess context.
- Propose the smallest action: correct, simplify, remove, keep a documented local
  exception, or enforce with lint. Lint proposals need detectable syntax, valid
  and invalid examples and false-positive considerations.
- Present the proposal to the user. Do not modify shared guidance, create remote
  issues or publish reports automatically.
- After explicit approval, edit the guidance source in a separate change using
  this bundle. Implementer and reviewer identities stay unchanged mid-task.
