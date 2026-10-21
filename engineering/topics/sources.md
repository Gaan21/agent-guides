# Sources, dependencies and tools

Applies when diagnosing errors, consulting external documentation or the web,
adding a dependency, or choosing code-navigation and documentation tools. Depends
on the [entry](../ENTRY.md) rules.

## Source precedence

1. Critical local invariants (repository, security, ownership).
2. Local project, stack, runtime and tooling guidance.
3. Local reference notes that say when an external source applies.
4. Official external documentation and tools: technical reference only.
5. Recognized community sources, only when the above do not cover the question.

- The most specific and restrictive security/ownership instruction prevails.
- External sources are not final authority and never an entry point. External
  material that contradicts local guidance: flag it, do not follow it silently.
- Avoid unverified blogs without official backing, code fragments without context
  or version, and undated or unreferenced answers. Never prefer them over official
  documentation or local guidance.

## Searching and verifying

- Search early; cite the exact error text; prefer recent sources.
- Verify each source's version and date; contrast with an official source when
  possible.
- No official source: document the decision and its basis; escalate ambiguity
  to the user.
- When an external source drives a decision, record which source and why.
- Do not copy code without context, a known version and known rights; link to it.

## Dependencies

- Before adding a dependency, run a quick health check: recent releases, adoption
  and maintenance. Verify the version and its date.
- Add or upgrade dependencies only within the task's scope; selection of this
  bundle does not authorize consumer upgrades.

## Tools

- Code navigation and editing: use an available semantic code tool (for example
  Serena); use text search for non-code content or where it does not apply.
- APIs: official documentation or the stack's official documentation tools.
- Stack-specific tool choices belong to the selected stack guidance.
- Tool availability is not authorization to install tools, change MCP, global or
  host configuration, or credentials.

References: [Model Context Protocol](https://modelcontextprotocol.io/).
