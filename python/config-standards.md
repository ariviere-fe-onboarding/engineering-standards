# Python Configuration Standards

- Never call `os.environ` directly in application code. Always read configuration through the shared `get_config()` helper so values can be validated, defaulted, and mocked consistently in tests.
