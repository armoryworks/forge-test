## AUDIT-INV-POST-001 — Customer invoice posting is logged with GL effect

```yaml
id: AUDIT-INV-POST-001
title: Posting a customer invoice records actor, amount, and GL postings
goal: |
  Verify that posting a customer invoice records actor, timestamp,
  invoice number, customer, total amount, and a reference to the GL
  postings produced.
roles:
  - AR Clerk
  - Controller
preconditions:
  - A draft customer invoice tied to a shipment or SO exists.
prerequisite_cases:
  - AUDIT-SO-CREATE-001
steps:
  - n: 1
    action: |
      Post the invoice.
    expected: |
      Invoice posts and is no longer in draft.
  - n: 2
    action: |
      Open the invoice's audit log.
    expected: |
      Posting entry shows actor, timestamp, invoice number, customer,
      total amount, and a link or reference to the GL journal lines
      produced.
expected_overall: |
  Invoice posting is fully attributed and tied to the resulting GL
  effect.
pass_criteria: |
  Posting entry present AND captures attribution, amount, and GL
  reference.
est_minutes: 5
```
