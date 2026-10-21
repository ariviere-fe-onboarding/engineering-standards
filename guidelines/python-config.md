# Python configuration

- Never call `os.environ` or `os.getenv` directly in application code. Always read
  configuration through the service's shared `get_config()` helper so values can be
  validated, defaulted, and mocked consistently in tests.
- Secrets (API keys, signing secrets, database credentials) come only from configuration.
  Never commit a secret, a default secret, or a secret in a test fixture that is reused
  outside tests.
- Configuration is validated once at startup. A missing required value stops the service
  with a clear error rather than falling back to an insecure default.

**Rationale:** one entry point for configuration makes it auditable and testable, and
prevents secrets from appearing in scattered call sites.
