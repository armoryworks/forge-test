## EDGE-UNICODE-NAMES-004 — Unicode-aware sort orders names per locale, not by byte value

```yaml
id: EDGE-UNICODE-NAMES-004
title: A list of customers with accented names sorts by locale-aware order, not by raw byte order
goal: |
  Verify that sorting a list of customers whose names mix accented
  and unaccented Latin characters produces an order a human reader
  would expect — "Ångström" near "Aalto," not at the end after "Z" —
  per a documented locale collation.
roles:
  - Administrator
preconditions:
  - At least 10 customers with names that include both accented and
    unaccented characters (e.g., "Aalto", "Ångström", "Bär", "Bärbel",
    "Cabo", "Café", "Zebra").
steps:
  - n: 1
    action: |
      Sort the customer list ascending by name.
    expected: |
      Sort applies.
  - n: 2
    action: |
      Inspect the order. Confirm "Ångström" appears near "Aalto" /
      "Bär" — not after "Z" (which would indicate naive byte-order
      sort treating Å as a high-codepoint character).
    expected: |
      Order matches a documented locale collation (e.g., en-US, where
      Å is grouped with A; or Swedish locale, where Å sorts after Z).
      The application's locale is documented somewhere accessible.
  - n: 3
    action: |
      Switch the user's locale (if supported) and re-sort.
    expected: |
      Order changes per the new locale's collation rules.
expected_overall: |
  List sorting respects Unicode collation per a documented locale.
pass_criteria: |
  Sort order matches a documented locale's collation AND no byte-order
  artifacts (Å, Ä, Ö dumped at end) appear unless that is the locale's
  documented behavior.
why_this_matters: |
  Byte-order sorting puts every accented name at the end of the list,
  which makes finding "Ångström" require scrolling past "Z." A real
  ERP gets locale collation right.
est_minutes: 8
```
