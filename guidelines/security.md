# Security

## Authentication and authorization

- Every route requires an authenticated user unless it is explicitly listed as public
  in the service README. New routers include the authentication dependency.
- Authorization is checked on the server for every object access: confirm the current
  user may act on *this* record, not just that they are logged in.
- Nobody approves their own request. Approval actions check the approver against the
  submitter.

## Secrets and tokens

- Tokens are generated with the `secrets` module. Never derive a token from user data,
  timestamps, or `random`.
- Compare secrets, signatures, and tokens with `hmac.compare_digest`, never `==`.
- Store only a hash of a reset or session token at rest.

## Untrusted input

- Use the ORM or bound parameters for every query. Never build SQL with f-strings or
  string concatenation.
- Never mark user-supplied or model-generated content `|safe` in templates.
- Uploaded file names are never used as filesystem paths. Store files under generated
  names inside the configured upload directory.
- Outbound HTTP requests use a timeout and an allow-list of hosts. Never fetch a URL
  supplied by a user without validating it.

## AI features

- Treat model output as untrusted input: validate it against a schema before use.
- Model output may suggest values to a human; it never changes approval state,
  permissions, or money movement on its own.
- Content from users (receipts, notes, documents) is passed to a model as data, clearly
  separated from instructions.
