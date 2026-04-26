## EDGE-DATE-DST-004 — Time-stamped audit log entries near a DST transition remain monotonic

```yaml
id: EDGE-DATE-DST-004
title: Audit log entries spanning a DST transition remain in chronological order
goal: |
  Verify that the audit log, which captures every state-changing
  action, presents events in true chronological order across a DST
  transition — not naive wall-clock order, which would put a fall-back
  event before its predecessor.
roles:
  - Administrator
preconditions:
  - The tenant time zone observes DST.
  - The audit log is populated with at least a handful of recent
    actions.
steps:
  - n: 1
    action: |
      Identify (or backdate-create) two audit events that bracket a
      fall-back DST transition — one at 1:30 AM tenant-local before
      the transition, one at 1:30 AM after.
    expected: |
      Both events appear in the audit log.
  - n: 2
    action: |
      Read the audit log sorted by timestamp.
    expected: |
      The earlier event appears first; the later event appears second.
      No reordering or visual ambiguity, even though both display 1:30
      AM tenant-local. The display disambiguates (e.g., shows offset:
      1:30 AM PDT vs 1:30 AM PST).
  - n: 3
    action: |
      Filter the audit log by the calendar day of the transition.
    expected: |
      Both events are returned. Order remains correct.
expected_overall: |
  Audit log preserves true chronological order across DST.
pass_criteria: |
  Events display in true time order AND the display unambiguously
  distinguishes the two 1:30 AM occurrences.
why_this_matters: |
  Audit logs are the legal record of who did what when. Out-of-order
  events on DST day undermine the entire audit story.
est_minutes: 8
```
