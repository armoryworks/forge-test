## LIST-SO-005 — Sales order list: multi-column sort + saved view

```yaml
id: LIST-SO-005
title: SO list supports multi-column sort and named saved views
goal: |
  Verify the SO list supports stable multi-column sort and the
  ability to save the current filter / sort / column set as a named
  view that persists per-user.
roles:
  - Sales / Account Manager
  - Customer Service
preconditions:
  - At least 50 SOs exist across customers, statuses, and dates.
steps:
  - n: 1
    action: |
      Sort by promised ship date (ascending) primary, then by
      customer (ascending) secondary, then by total amount
      (descending) tertiary.
    expected: |
      Sort precedence reflected; sort indicator shows three-level
      precedence; ties break correctly.
  - n: 2
    action: |
      Apply filter: status = Open. Hide one column.
    expected: |
      List reflects all settings.
  - n: 3
    action: |
      Save as named view (e.g., "Open SOs by ship date").
    expected: |
      Saved view appears in menu.
  - n: 4
    action: |
      Switch to default view, then re-open the saved view.
    expected: |
      Saved view restores filter / sort / column set exactly.
  - n: 5
    action: |
      Delete the saved view.
    expected: |
      Saved view removed.
expected_overall: |
  Multi-column sort and saved views together support recurring
  customer-service / sales workflows.
pass_criteria: |
  Sort precedence and saved-view save / recall / delete all work
  cleanly.
est_minutes: 6
```
