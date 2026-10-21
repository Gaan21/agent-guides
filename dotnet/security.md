# Security: input, identity, secrets and errors

Dependencies: [architecture](architecture.md), [controllers](controllers.md) for API
work. Before deployment also read [deployment](deployment.md).

## Input and access

- Validate every input DTO with required/bounded/format/range constraints appropriate
  to its contract; sanitize free text where required. Test valid, invalid, missing
  and excessive input. Do not change an identifier into an email without authority.
- Require authentication by default, explicitly allow public operations and enforce
  resource/role authorization. Preserve 401 versus 403 semantics.
- Apply least privilege to database users and sensitive operations.
- Protect refresh tokens with the project's short-expiration/rotation policy; do not
  invent a lifetime or claim a specific implementation exists.

## Secrets and startup

- No real keys, passwords, tokens or connection-string secrets in source or
  appsettings. Development uses User Secrets; production uses environment variables
  or an approved secret manager. Keep setup instructions free of real values.
- Validate required configuration at startup and fail clearly on missing/invalid
  values. Signing keys must meet algorithm-specific strength/encoding requirements;
  a character count alone is not a universal cryptographic guarantee.
- Password hashing must use an appropriate salted password KDF, not direct unsalted
  SHA-256. Distinguish password protection from non-password identifier hashing;
  inspect actual usage before changing anything. Existing-password migration needs
  an explicit plan. Evaluate Identity when complete user management is required.
- Verify password hashes with constant-time comparison. Do not import an old work
  factor or implementation as a current security default; verify official guidance.

## Error and audit boundary

- Production errors are generic, without exception messages, stack traces, paths or
  database details. Development-only detail must be environment-gated.
- Include safe trace correlation, log diagnostics server-side and test Development
  and Production behavior. A 404 response is not proof of exception handling.
- Use structured logging/auditing for sensitive operations and access denials;
  do not log tokens, passwords, secrets or PII. A correlation identifier must not
  expose personal identifiers/IP addresses by default. Respect local privacy policy.
- Appropriate response caching needs explicit cache profiles and authorization/data
  sensitivity review; never treat performance caching as permission to expose data.
