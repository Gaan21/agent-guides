# Official references and evidence limits

Consult local adopted decisions first, then version-appropriate official documentation
for APIs/mechanics. External examples do not override security/ownership or authorize
architectural changes. Report contradictions; use an ADR for approved policy changes.
The host/factory chooses available tools. No MCP schema, memory deletion instruction,
tool-version guarantee, skill installation or repeated read pipeline is included here.

These links were consulted on 2026-10-21; available documentation/source is not an
installed-version test. Check the actual package/hosting/runner before behavior claims.
No external prose, examples, configurations or executable helpers are incorporated.

- [WebApplicationFactory services API](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.services?view=aspnetcore-8.0)
- [ASP.NET Core 8 factory implementation](https://github.com/dotnet/aspnetcore/blob/v8.0.0/src/Mvc/Mvc.Testing/src/WebApplicationFactory.cs)
- [xUnit shared context and fixture lifetime](https://xunit.net/docs/shared-context)
- [xUnit parallel execution](https://xunit.net/docs/running-tests-in-parallel)
- [EF Core SQLite in-memory testing](https://learn.microsoft.com/en-us/ef/core/testing/testing-without-the-database#sqlite-in-memory)
- [EF Core transaction scope and limitations](https://learn.microsoft.com/en-us/ef/core/saving/transactions)
- [TestServer execution-context boundary](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.testhost.testserver.preserveexecutioncontext?view=aspnetcore-8.0)

For other API questions, retrieve the relevant current official page only as needed.
Do not assume a historical library identifier, sample benchmark or quoted capability
still describes the installed environment.
