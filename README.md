# agent-guides

Public catalog of common authored guidance for coding agents. Content only: the
tool that installs, pins and connects these guides is
[agent-guides-cli](https://github.com/Gaan21/agent-guides-cli).

Status: **T05 bounded preparation accepted; source available on `develop`** after
authorized upload. Ten common technology/topic bundles are not a stable release
or consumer activation. See the
[agent-guides-cli task board](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/tasks/README.md).
That board owns order, status and acceptance; this repository has no board of its own.

Future maintainers: [deferred guidance/lint improvements](docs/deferred-improvements.md)
records non-priority follow-up and the required cross-package impact review.

## Layout

The published source includes Git, Flutter, Astro, Next.js, Supabase, .NET, engineering,
guidance maintenance, agent workflow and UI design. Independent R1–R5 correction
reviews passed their bounded scopes; see the CLI's
[T05 acceptance](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/tasks/T05-acceptance.md)
for checks and limits. The owner-authorized T05 source upload is complete; future
publication actions require their own authorization. This is not a stable release
or instruction to migrate consumers.

One self-contained bundle per stack or topic, each in its own top-level directory:

```text
flutter/                 # one selectable bundle
  guidance-bundle.json   # schema 1: id, entry, files, notices
  README.md              # short entry: always-on rules and when to read each topic
  ...                    # topic documents, notices
```

Each project explicitly selects its technology/topic bundles, for example Git +
Flutter + Supabase or Git + Next.js. Catalog availability does not activate every
bundle. Existing private product contracts are not published as common guidance.

Bundle format:
[schema 1](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/preparation.md#self-contained-bundle-schema-1).
A project selects one or more bundles; all bundles from this repository share one
recorded commit, so an update moves every selected bundle together
([ADR 0003](https://github.com/Gaan21/agent-guides-cli/blob/develop/docs/decisions/0003-tool-and-guides-repositories.md)).

## What belongs here

- Reusable guidance that is clearly not specific to one product.
- Never product APIs, private paths, product architecture rules or consumer logs.
  Product-specific or uncertain content goes to that product's private bundle
  (the private `agent-guides-private-projects` product catalog).
- Notices and attribution travel with each bundle.

Legacy Flutter delivery stays in
[flutter-agent-guidelines](https://github.com/Gaan21/flutter-agent-guidelines) until
its consumers are migrated (T06); it is not deleted or edited from here.
