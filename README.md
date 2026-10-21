# Fernway engineering standards

Organization-wide engineering rules for Fernway services. Every service repository
references these guidelines from its `.coderabbit.yaml`, so review findings can cite
the rule that applies even though it lives here and not in the service repository.

| Guideline | Applies to |
|---|---|
| [Python configuration](guidelines/python-config.md) | All Python services |
| [Money](guidelines/money.md) | Any code that computes, stores, or transmits monetary values |
| [Security](guidelines/security.md) | All application code |
| [API contracts](guidelines/api-contracts.md) | HTTP APIs and webhooks between services |
| [Data handling](guidelines/data-handling.md) | Personal and financial data |

Fernway is a fictional company. All names, people, and data in Fernway repositories
are synthetic.
