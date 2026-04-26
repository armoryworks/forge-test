# Edge Cases Suite

The category of bugs that surface only at month-end, only on a leap year, only when an FX rate moves a few decimals, only when a list crosses a few thousand rows. None of these are exotic — they happen every quarter in any real shop. This suite covers the canonical date, currency, decimal-precision, scale, unicode, time-zone, signed-quantity, null-vs-empty, and zero-boundary permission edge cases that ERPs routinely get wrong.

## ID convention

`EDGE-{CATEGORY}-{SCENARIO}-NNN` where category is `DATE`, `FX`, `DECIMAL`, `TAX`, `SCALE`, `UNICODE`, `NEGQTY`, `ZEROQTY`, `NULLEMPTY`, or `PERMZERO`.

## Sequence

Cases are independent. Each can be run against the post-Phase-5 state with the listed scenario state established.

```yaml
suite: edge-cases
title: Date, currency, decimal, tax, scale, unicode, signed-quantity, null/empty, and zero-boundary edge cases
description: |
  Bugs that surface only at boundaries: fiscal year end, DST, leap
  year, decimal-precision rounding, FX rate movement, tax-rate change
  mid-period, list views over five thousand rows, non-ASCII names,
  time-zone-spanning shifts, negative and zero quantities, empty vs
  null values, and permission boundaries at exactly zero. The bar is
  that the application handles each cleanly without silent corruption.
estimated_total_minutes: 360

cases:
  - id: EDGE-DATE-FYBOUNDARY-001
  - id: EDGE-DATE-FYBOUNDARY-002
  - id: EDGE-DATE-FYBOUNDARY-003
  - id: EDGE-DATE-FYBOUNDARY-004
  - id: EDGE-DATE-DST-001
  - id: EDGE-DATE-DST-002
  - id: EDGE-DATE-DST-003
  - id: EDGE-DATE-DST-004
  - id: EDGE-DATE-LEAP-001
  - id: EDGE-DATE-LEAP-002
  - id: EDGE-DATE-LEAP-003
  - id: EDGE-DATE-LEAP-004
  - id: EDGE-DATE-TZBOUNDARY-001
  - id: EDGE-DATE-TZSHIFT-001
  - id: EDGE-DATE-TZSHIFT-002
  - id: EDGE-DATE-TZSHIFT-003
  - id: EDGE-FX-ROUNDING-001
  - id: EDGE-FX-ROUNDING-002
  - id: EDGE-FX-ROUNDING-003
  - id: EDGE-FX-RATEMOVE-001
  - id: EDGE-DECIMAL-PRECISION-001
  - id: EDGE-DECIMAL-PRECISION-002
  - id: EDGE-DECIMAL-PRECISION-003
  - id: EDGE-DECIMAL-PRECISION-004
  - id: EDGE-TAX-RATECHANGE-001
  - id: EDGE-TAX-RATECHANGE-002
  - id: EDGE-TAX-RATECHANGE-003
  - id: EDGE-TAX-RATECHANGE-004
  - id: EDGE-SCALE-LARGELIST-001
  - id: EDGE-SCALE-LARGELIST-002
  - id: EDGE-SCALE-LARGELIST-003
  - id: EDGE-SCALE-LARGEEXPORT-001
  - id: EDGE-SCALE-LARGEEXPORT-002
  - id: EDGE-UNICODE-NAMES-001
  - id: EDGE-UNICODE-NAMES-002
  - id: EDGE-UNICODE-NAMES-003
  - id: EDGE-UNICODE-NAMES-004
  - id: EDGE-NEGQTY-001
  - id: EDGE-NEGQTY-002
  - id: EDGE-NEGQTY-003
  - id: EDGE-ZEROQTY-001
  - id: EDGE-ZEROQTY-002
  - id: EDGE-ZEROQTY-003
  - id: EDGE-NULLEMPTY-001
  - id: EDGE-NULLEMPTY-002
  - id: EDGE-NULLEMPTY-003
  - id: EDGE-PERMZERO-001
  - id: EDGE-PERMZERO-002
  - id: EDGE-PERMZERO-003
  - id: EDGE-PERMZERO-004

completion_criteria:
  - Every case in the suite has a recorded pass/fail.
  - No silent data corruption occurred in any case.
```
