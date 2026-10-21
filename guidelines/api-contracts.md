# API contracts

These rules apply to HTTP APIs and webhooks consumed by another Fernway service.

- Every webhook payload carries an integer `version`. Changes within a version are
  additive only. Removing, renaming, or retyping a field requires a new version and a
  migration window in which both versions are sent.
- The producer documents the contract in its repository, and the consumer's tests pin
  the contract it relies on.
- Webhooks are signed with HMAC-SHA256 over the raw request body using a shared secret.
  Consumers reject unsigned or incorrectly signed requests.
- Every webhook carries an idempotency key. Consumers must process each key at most
  once, including on retries.
- Outbound calls to another service use a timeout and handle failure explicitly.

**Rationale:** producers and consumers deploy independently. An unannounced contract
change breaks a consumer in production, usually in a different team's repository.
