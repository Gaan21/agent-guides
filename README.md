# agent-guides

Public catalog of common authored guidance for coding agents. Content only: the
tool that installs, pins and connects these guides is
[agent-guides-cli](https://github.com/Gaan21/agent-guides-cli).

Status: **empty, being prepared.** The first bundle (common Flutter guidance) is
produced by task T05 on the
[agent-guides-cli task board](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/tasks/README.md).
That board owns order, status and acceptance; this repository has no board of its own.

## Layout

One self-contained bundle per stack or topic, each in its own top-level directory:

```text
flutter/                 # planned first bundle
  guidance-bundle.json   # schema 1: id, entry, files, notices
  README.md              # short entry: always-on rules and when to read each topic
  ...                    # topic documents, notices
```

Bundle format:
[schema 1](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/preparation.md#self-contained-bundle-schema-1).
A project selects one or more bundles; all bundles from this repository share one
recorded commit, so an update moves every selected bundle together
([ADR 0003](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/decisions/0003-tool-and-guides-repositories.md)).

## What belongs here

- Reusable guidance that is clearly not specific to one product.
- Never product APIs, private paths, product architecture rules or consumer logs.
  Product-specific or uncertain content goes to that product's private bundle
  (for WorkTracker: the private `worktracker-architecture-guides` repository).
- Notices and attribution travel with each bundle.

Legacy Flutter delivery stays in
[flutter-agent-guidelines](https://github.com/Gaan21/flutter-agent-guidelines) until
its consumers are migrated (T06); it is not deleted or edited from here.
