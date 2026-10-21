# Data handling

## Bank account data

- Bank account and routing numbers are stored only in `payouts-service`, which is in
  scope for financial audits. No other service stores, caches, or logs them.
- Outside `payouts-service`, bank details appear only masked (last four digits).
- `payouts-service` encrypts bank account numbers at rest.

## Logging

- Never log passwords, tokens, signatures, full bank details, or complete webhook
  payloads.
- Log identifiers (expense ID, payout ID), not personal data.

## Responses

- API responses are explicit, allow-listed schemas. Never return an ORM object or a raw
  database row directly.

**Rationale:** keeping bank data in one small service keeps every other service out of
audit scope. A single leaked field pulls another repository into that scope.
