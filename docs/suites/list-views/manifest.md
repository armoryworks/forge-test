# List View UX Suite

List views are where everyday users live. A list view that's fine at 100 records and unusable at 5,000 silently destroys productivity. This suite covers the canonical search / filter / sort / paginate behaviors per major list view, in addition to the dedicated EDGE-SCALE cases that probe behavior at scale.

## ID convention

`LIST-{ENTITY}-NNN`.

```yaml
suite: list-views
title: Per-entity list view UX (search, filter, sort, paginate)
description: |
  For each major list view, verify partial search, status filter,
  date range filter, multi-column sort, pagination at scale, and
  saved-view persistence.
estimated_total_minutes: 35

cases:
  - id: LIST-CUST-001
  - id: LIST-CUST-002
  - id: LIST-CUST-003
  - id: LIST-CUST-004
  - id: LIST-CUST-005
  - id: LIST-VENDOR-001
  - id: LIST-VENDOR-002
  - id: LIST-VENDOR-003
  - id: LIST-VENDOR-004
  - id: LIST-VENDOR-005
  - id: LIST-PART-001
  - id: LIST-PART-002
  - id: LIST-PART-003
  - id: LIST-PART-004
  - id: LIST-PART-005
  - id: LIST-BOM-001
  - id: LIST-BOM-002
  - id: LIST-BOM-003
  - id: LIST-BOM-004
  - id: LIST-BOM-005
  - id: LIST-PO-001
  - id: LIST-PO-002
  - id: LIST-PO-003
  - id: LIST-PO-004
  - id: LIST-PO-005
  - id: LIST-SO-001
  - id: LIST-SO-002
  - id: LIST-SO-003
  - id: LIST-SO-004
  - id: LIST-SO-005
  - id: LIST-WO-001
  - id: LIST-WO-002
  - id: LIST-WO-003
  - id: LIST-WO-004
  - id: LIST-WO-005
  - id: LIST-INV-001
  - id: LIST-INV-002
  - id: LIST-INV-003
  - id: LIST-INV-004
  - id: LIST-INV-005
  - id: LIST-PAY-001
  - id: LIST-PAY-002
  - id: LIST-PAY-003
  - id: LIST-PAY-004
  - id: LIST-PAY-005
  - id: LIST-EMP-001
  - id: LIST-EMP-002
  - id: LIST-EMP-003
  - id: LIST-EMP-004
  - id: LIST-EMP-005

completion_criteria:
  - Every list view supports partial search, sort, filter, and pagination.
  - No silent truncation or missing records.
```
