## AUDIT-PAY-APPLY-001 — Customer payment application is logged

```yaml
id: AUDIT-PAY-APPLY-001
title: Applying a customer payment records actor, amount, and applications
goal: |
  Verify that recording and applying a customer payment against open
  invoices records actor, timestamp, payment amount, deposit account,
  and each invoice the payment was applied to with the applied amount.
roles:
  - AR Clerk
preconditions:
  - At least one posted, unpaid customer invoice exists.
prerequisite_cases:
  - AUDIT-INV-POST-001
steps:
  - n: 1
    action: |
      Record a customer payment. Apply it across one or more open
      invoices.
    expected: |
      Payment posts and the targeted invoices reflect the applied amount.
  - n: 2
    action: |
      Open the payment's audit log.
    expected: |
      Application entry shows actor, timestamp, payment total, deposit
      account, and each invoice / amount applied. A GL reference to the
      cash receipt postings is included.
expected_overall: |
  Cash application is fully attributed and traceable to invoice and GL.
pass_criteria: |
  Entry present with attribution, total, application detail, and GL
  reference.
est_minutes: 5
```
