# Localization evidence and review

Applies when choosing tests for a localization change, closing a doubt, or
reviewing such a change. Depends on the [entry](../ENTRY.md) and
[coverage](coverage.md).

## Evidence proportional to the change

| Change or doubt | Minimum useful evidence |
| --- | --- |
| Direct visible text, mechanism unchanged | Available format/generation checks, literal detector and a look at the consumer; no getter or pure-layout tests |
| Error → code → translator → notice | Trigger the failure in the producer (use case, view model or equivalent) and check code/arguments; test the real handler/consumer with the localized output |
| Helper, variable or callback with an unclear destination | Trace producer and consumer; if reading does not prove the destination, test the consumer with the affected path's input |
| Technical-only or mixed use | Confirm log and visible output separately; keep the translation when it has real visible use, without translating the log to justify it |
| Dynamic or remote code | Table of accepted codes and a parameterized test of the real consumer; also test the unknown code and its safe fallback |
| Parameters, plural, select or languages | Synthetic fixtures for the relevant variants in the affected languages; check substitution and chosen branch, not only that it compiles |
| Native prompt, accessibility, notification or export | Fake of the adapter or inspection of the output meant for the user; finding a text widget is not enough |
| Language selection or per-language content | Check choice, persistence/routing and effective output; selector and resources declare the same languages |
| Legal or separate editorial content | Matching version per supported language, path/identifier and metadata; review the affected versions without claiming legal equivalence |

- Reuse existing tests when their assertions cover the path and the variants of
  the change. Producer and consumer evidence may be combined through the same
  code/arguments: no end-to-end test per message is needed.
- Parameterize the shared mechanism; add a regression test for the connection that
  was broken. For language-selection mechanisms use at least two languages with
  different outputs.
- Use a browser or device only when widget, unit or adapter tests cannot show what
  is needed and the task allows it. If permission or a dependency is missing, stop
  and explain the limit.

## Closing a doubt without creating an exception

- The implementer identifies the key/code and path, the affected change, the
  concrete test or trace, expected and actual result, and limits. Evidence lives in
  tests and in files the task scope allows; no new inventory per key and no files
  outside the scope. A "reviewed" claim, a test that only mentions the key or a list
  of exclusions does not resolve the doubt.
- The reviewer checks that the evidence belongs to the same candidate and to the
  real consumer, runs the specific test needed or contrasts a traceable
  deterministic result, and cites the test/command path and name or the concrete
  trace. If reading the code is enough, explain both ends of the path and why no
  other test is needed. No demand for linguistic perfection or redundant tests.
- A relevant doubt without enough evidence to accept the change is a blocking
  finding; if the review format has a not-verified list, mention it there too, but
  never hide it there while accepting. An out-of-scope defect is reported and
  escalated, not fixed without authorization and not turned into a waiver. Changing
  the candidate invalidates the affected evidence. Neither the test nor the agent's
  opinion authorizes publication, merge or deployment.
