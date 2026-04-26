## LIST-WO-004 — WO list: saved filter views

```yaml
id: LIST-WO-004
title: WO list supports named saved filter views
goal: |
  Verify the WO list supports saved views for recurring queries
  (e.g., "My active WOs", "Late WOs", "Press Shop today") and that
  saved views persist per-user.
roles:
  - Production Manager
  - Production Planner
preconditions:
  - At least 50 WOs exist across statuses, work centers, and due
    dates.
steps:
  - n: 1
    action: |
      Configure: filter to status = In-progress + work center =
      Press Shop, sort by due date ascending.
    expected: |
      List reflects the configuration.
  - n: 2
    action: |
      Save as a named view (e.g., "Press Shop active").
    expected: |
      Saved view appears in the menu.
  - n: 3
    action: |
      Switch to a default list view, then re-open the saved view.
    expected: |
      Saved view restores the exact filter / sort.
  - n: 4
    action: |
      Edit the saved view: change one filter and save in place.
    expected: |
      Saved view updates.
  - n: 5
    action: |
      Delete the saved view.
    expected: |
      View removed. Default list unaffected.
expected_overall: |
  Saved views support recurring production-floor workflows.
pass_criteria: |
  Save, recall, edit, and delete all work cleanly.
est_minutes: 5
```
