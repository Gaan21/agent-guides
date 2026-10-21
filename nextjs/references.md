# References and precedence

Applicable local security/ownership invariants and project rules come first, then
adopted local stack/runtime guidance, then local reference conditions, then external
technical contrast. The more specific/restrictive security/ownership rule wins.
External guidance is never the entrypoint or final authority. Consult only when
the task/API question needs it, after reading relevant local detail; no global
external auto-invoke, vendored skill, tutorial, config or lint-rule import.

Record actionable divergence as current/current-but-incomplete/misaligned/obsolete,
and intentional-local-decision versus real drift, with scope, evidence, version/date,
risk and minimal proposed action. Retain local decisions until an approved change;
do not silently modernize architecture/cache/runtime or enlarge test gates. Explicit
upgrade tasks first assess breaking changes against adopted rules. Escalate actual
conflicts rather than importing an external skill as a replacement authority.

## Official links by question

- Architecture: [project structure](https://nextjs.org/docs/app/getting-started/project-structure),
  [server/client](https://nextjs.org/docs/app/getting-started/server-and-client-components).
- Reads/assets: [data and streaming](https://nextjs.org/docs/app/getting-started/fetching-data),
  [images](https://nextjs.org/docs/app/getting-started/images),
  [adopted cache model](https://nextjs.org/docs/app/guides/caching-without-cache-components).
- Env: [environment variables](https://nextjs.org/docs/app/guides/environment-variables).
- Checks: [ESLint](https://nextjs.org/docs/app/api-reference/config/eslint),
  [lint CLI migration](https://nextjs.org/docs/app/guides/upgrading/codemods#next-lint-to-eslint-cli),
  [testing](https://nextjs.org/docs/app/guides/testing),
  [Playwright](https://playwright.dev/docs/intro), [Vitest](https://vitest.dev/guide/).
- Server exports: [invalid runtime export](https://nextjs.org/docs/messages/invalid-use-server-value),
  [server directive](https://nextjs.org/docs/app/api-reference/directives/use-server),
  [TypeScript type-only erasure](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-8.html#type-only-imports-and-export),
  [module emit](https://www.typescriptlang.org/tsconfig/verbatimModuleSyntax.html).
- Binary bodies: [Fetch BodyInit](https://fetch.spec.whatwg.org/#bodyinit-unions),
  [Response](https://fetch.spec.whatwg.org/#response-class),
  [assertion erasure](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions),
  [typed-array buffer types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-7.html#typedarrays-are-now-generic-over-arraybufferlike).
- Target runtime: [OpenNext Cloudflare](https://opennext.js.org/cloudflare),
  [Workers Next.js guide](https://developers.cloudflare.com/workers/frameworks/framework-guides/nextjs/).
- Adopted next-intl: [App Router without locale routing](https://next-intl.dev/docs/getting-started/app-router/without-i18n-routing),
  [runtime](https://next-intl.dev/docs/environments/runtime),
  [locale detection](https://next-intl.dev/docs/routing#locale-detection).
- Accessibility: [web.dev](https://web.dev/accessibility),
  [WCAG quick reference](https://www.w3.org/WAI/WCAG21/quickref/).
- Broader API lookup: [Next.js documentation index](https://nextjs.org/docs/llms-full.txt).

Runtime-export/type-erasure/binary-body/OpenNext references were consulted
2026-10-21 for narrow factual constraints, not installed-version certification.
Other links are retained reading references, not freshly verified claims. Upstream
pages are mutable; inspect actual target versions for execution evidence. No example
imports, code bodies, setup instructions or external license grants are bundled.
