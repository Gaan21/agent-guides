# Boundaries and responsibilities

Applies when code receives external data (SDK, API, database, RPC or another
provider) or when deciding where conversion and logic live. Depends on the
[entry](../ENTRY.md) rules and [code quality](code-quality.md) for extraction level.

## Normalize at the boundary

- Convert external data to the project's domain type at the entry point.
- Callers never see raw provider structures.
- The mechanism varies by stack (for example mappers, DTOs or `parse`/`normalize`
  functions); the principle is the same everywhere. Use the boundary location and
  mechanism the stack or project assigns.

## Responsibility placement

- Place logic and conversion at the level the existing architecture assigns;
  extract shared behavior at the correct level, not always the highest one.
- Existing layers, dependency direction and ownership remain as the project
  defines them. These principles do not authorize an architecture redesign.
- Missing local boundary contracts: report the gap rather than inventing one.
