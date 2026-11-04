# Inventory

One independently selectable bundle, with local dependencies and no automatic
cross-bundle activation. The declaration is the complete installed-file inventory.

| File | Role / when to read |
| --- | --- |
| [ENTRY.md](ENTRY.md) | Scope, always-on rules and navigation |
| [Coverage](topics/coverage.md) | What is product text, review scope, what automation covers; requires entry |
| [Evidence](topics/evidence.md) | Tests proportional to the change and how to close a doubt; requires coverage |
| [NOTICE.md](NOTICE.md) | Provenance, changes and exclusions |
| [LICENSE](LICENSE) | Full Apache-2.0 terms |
| `guidance-bundle.json` | Schema-1 entry/file/notice declaration |

Stack details (resource files, generators, libraries) stay in the stack bundles;
product languages and product-specific boundaries stay in the project's contract.
No detector, script or configuration is installed by this bundle.
