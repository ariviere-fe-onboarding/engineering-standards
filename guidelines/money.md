# Money

These rules are mandatory for any code that computes, stores, or transmits monetary values.

## Integer cents only

- Monetary amounts are integers in the currency's minor unit (for USD, cents), never
  floating-point numbers of dollars.
- Never multiply or divide a monetary amount by a float. Compute percentages with integer
  arithmetic and round once, explicitly, at the boundary.
- Parse user-entered amounts with `decimal.Decimal`, then convert to integer cents.
  Never call `float()` on a monetary string.

## Names carry the unit

- A field holding minor units ends in `_cents` (`amount_cents`, `total_cents`). A field
  without that suffix must not hold a monetary amount.
- Every amount travels with its ISO 4217 `currency` code.

## Limits are inclusive

- Approval and policy limits are inclusive: a manager limit of $500.00 means
  `amount_cents <= 50_000` is within the limit.

**Rationale:** floating-point currency arithmetic silently loses precision. An amount
whose unit is ambiguous gets misread by a downstream system as 100x too large or too small.
