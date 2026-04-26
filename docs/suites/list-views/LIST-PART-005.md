## LIST-PART-005 — Part list: saved filter views

```yaml
id: LIST-PART-005
title: Part list supports named saved filter views
goal: |
  Verify the parts list lets a user save the current filter / sort /
  column configuration as a named view, return to it later, share
  it (where supported), and delete it cleanly.
roles:
  - Engineer / R&D
  - Procurement
preconditions:
  - At least 100 parts exist across multiple types and statuses.
steps:
  - n: 1
    action: |
      Configure the list: filter type = Raw material, status =
      Active, sort by part number ascending, hide cost column.
    expected: |
      List reflects the configuration.
  - n: 2
    action: |
      Save as a named view (e.g., "My active raw materials").
    expected: |
      View appears in the saved-views menu.
  - n: 3
    action: |
      Switch to a different list configuration, then re-open the
      saved view.
    expected: |
      Saved view restores the exact filter / sort / column set.
  - n: 4
    action: |
      Edit the saved view: change one filter, save in place.
    expected: |
      View updates. Re-opening loads the new config.
  - n: 5
    action: |
      Delete the saved view.
    expected: |
      View removed from menu. Default list view unaffected.
expected_overall: |
  Saved views support recurring engineering / procurement workflows.
pass_criteria: |
  Save, recall, edit, and delete all work cleanly. Saved views are
  scoped per-user (or per-team if shared, with clear ownership).
est_minutes: 6
```
