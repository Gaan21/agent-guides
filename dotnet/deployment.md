# Security verification and deployment boundaries

Dependency: [security](security.md). Applies to deployment preparation/verification;
does not authorize deployment or impose a second factory publication pipeline.

Before first production deployment, satisfy critical/high checks. On subsequent
deployments verify all applicable critical/high/medium checks; retain monthly review
of lower-priority hardening. A project's mandatory gates remain mandatory even if
a reference labels a finding low priority. Do not claim historical findings current.

## Required applicable checks

- Explicit allowed CORS origins, appropriate methods/headers/credentials and correct
  middleware order: after routing, before authentication. Verify preflight, allowed
  origins and denial of disallowed origins. Do not use a wildcard production policy.
- Production HTTPS redirection and valid certificates; appropriate HSTS outside
  development. Subdomains, preload and preload-list submission require domain-owner
  decisions, not automatic configuration or a universal duration.
- Review security headers/CSP for the application's actual response types and current
  platform guidance. Do not reproduce obsolete header recipes as guaranteed protection.
- Authentication fallback/default protection, explicit anonymous exceptions, correct
  role/resource checks and startup secret validation.
- Input validation; salted password KDF if passwords are used; no leaked error detail.
- Rate limits on exposed sensitive/public operations, especially authentication.
  Verify allowed attempts, rejection with 429 and recovery; monitor safely. Exact
  limits/windows/partition keys are project policy, not universal constants.
- Logs/audit and least privilege; secure environment configuration and secret storage.
- Health behavior, HTTPS redirection, HSTS/security headers, CORS and authentication
  verified after authorized deployment. Check actual endpoints without embedding
  origins, credentials or product commands in shared guidance.

Record actual results and justified exceptions. Missing/failing mandatory checks
block closure/commit/push; consult owner/host rather than treating unavailable checks
as passed. Factory chooses execution/tool/publication mechanisms; manual work keeps
the agreed branch and scopes any authorized validated closeout. No automatic
environment changes, dependencies, certificates, external registration or secrets.
