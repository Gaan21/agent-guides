# Controllers and DTO boundaries

Dependencies: [architecture](architecture.md), [services/data](services-data.md),
[security](security.md). Applies to endpoint/input/response changes.

- Use API controller/routing conventions, constructor-injected service interfaces,
  explicit input binding as appropriate and semantic IActionResult responses.
- Validate request DTOs with appropriate required, length, range and format rules.
  ApiController supports automatic invalid-model responses; manual ModelState checks
  are for cases that actually require them, not duplicated validation everywhere.
- Authentication is required by default; mark genuinely public operations explicitly
  anonymous. Check resource ownership/permissions as well as authentication.
- Pass cancellation through asynchronous service/data operations.
- Services return mapped DTOs/outcomes; controllers translate the actual result
  kind to HTTP semantics. Do not map every unsuccessful result to one status code.
- Use 200 for successful data, 201 for creation with correct resource location,
  204 for successful no-content operations, 400 for invalid input, 401 for missing
  or invalid authentication, 403 for denied access and 404 for absent resources.
  Preserve the product's actual contract, including its deliberate exceptions.
- No business logic, DAO/DbContext access or raw technical exceptions in controllers.
  Secure middleware handles unexpected faults; do not invent runnable API types.

Test validation, authentication, authorization, error and happy behavior where
applicable; see [test quality](test-quality.md). An unauthenticated protected request
does not establish input-validation behavior. A missing route does not exercise
exception sanitization. Verify each intended boundary with the appropriate context.
