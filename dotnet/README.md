# .NET guidance

Applies when this bundle is selected for .NET/ASP.NET Core work. These are adopted
stack conventions, not universal framework requirements. Project-local authority
and explicit exceptions remain authoritative; do not redesign an existing product.

Before applicable edits, read the relevant topics and their dependencies below.
Reuse guidance while in context; read new topics when scope changes and reread
after context loss or guidance changes. Do not load every topic or reread per patch.

| Work | Required reading |
| --- | --- |
| Any implementation | [Architecture](architecture.md) |
| Controller, endpoint, input DTO | [Controllers](controllers.md) + [Security](security.md) |
| Service, expected rejection, DAO, EF query | [Services and data](services-data.md) |
| Authentication, secrets, logging, errors | [Security](security.md) |
| Deployment/security verification | [Deployment](deployment.md) + [Security](security.md) |
| Query, cache or allocation optimization | [Performance](performance.md) + [Services and data](services-data.md) |
| Tests or fixture failures | [Testing](testing.md) + [Test quality](test-quality.md) |
| Time, auth, waiting/config test helpers | [Helpers](test-helpers.md) + [Testing](testing.md) |
| API facts, versions, external advice | [References](references.md) |

Always preserve layer boundaries, explicit outcomes for expected domain rejection,
input/access checks, secret safety and truthful validation results. Selection does
not authorize consumer changes, deployment or a database-provider switch.

Factory mode: host mechanisms own tools, branches, checks, PRs and publication;
do not create a competing pipeline. Manual mode: respect the agreed branch; scoped
commit/push follows successful authorized closure without repeated approval. A PR
is the default integration route, not a command to leave an agreed branch.
Missing/failing mandatory checks block closure and commit/push; report and consult
the owner/host blocked-work mechanism. No task-planning or size/time caps here.

See [inventory](INVENTORY.md) and [notices](NOTICE.md). Presence is not proof of
native loading, model compliance or installed framework behavior.
