# Bulk Operations Suite

Mass updates, mass deletes, mass status changes, mass reassigns. Real shops use these constantly: terms changes for a vendor list, closing a batch of completed WOs, reassigning a region's customers. Bulk operations are also where the worst data corruption happens — partial failures that leave records in inconsistent states.

## ID convention

`BULK-{ENTITY-OP}-NNN`.

```yaml
suite: bulk-ops
title: Bulk operations beyond import
description: |
  Mass update, mass status change, mass reassign, mass deactivate.
  Each operation must report which records succeeded, which failed,
  and why — never silent partial outcomes.
estimated_total_minutes: 40

cases:
  - id: BULK-VENDOR-TERMS-001
  - id: BULK-WO-CLOSE-001
  - id: BULK-CUST-REASSIGN-001
  - id: BULK-CUST-DEACT-001
  - id: BULK-PART-PRICE-001
  - id: BULK-PART-LEAD-001
  - id: BULK-CUST-TERMS-001
  - id: BULK-PART-COST-001
  - id: BULK-BOM-EFFDATE-001
  - id: BULK-PART-DEACT-001
  - id: BULK-EMP-DEACT-001
  - id: BULK-CONTRACT-EXPIRE-001
  - id: BULK-PART-OBSOLETE-001
  - id: BULK-QUOTE-DELETE-001
  - id: BULK-PO-DRAFT-DELETE-001
  - id: BULK-ATTACH-PURGE-001
  - id: BULK-FORECAST-DELETE-001
  - id: BULK-WO-WORKCENTER-001
  - id: BULK-PO-BUYER-001
  - id: BULK-INV-LOCATION-001
  - id: BULK-OPP-SALESREP-001
  - id: BULK-ASSET-CUSTODIAN-001
  - id: BULK-IMPORT-CUST-ERR-001
  - id: BULK-IMPORT-PART-DUP-001
  - id: BULK-IMPORT-VENDOR-VAL-001
  - id: BULK-IMPORT-PARTIAL-001
  - id: BULK-EXPORT-AR-FILTER-001
  - id: BULK-EXPORT-INV-LOC-001
  - id: BULK-EXPORT-WO-DATE-001
  - id: BULK-EXPORT-PII-001

completion_criteria:
  - Every bulk operation reports success / failure per row.
  - No partial-state corruption in any case.
```
