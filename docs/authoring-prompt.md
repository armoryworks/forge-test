# Manual test scenario authoring — MRP/ERP gap closure

> Hand this prompt verbatim to a fresh AI session that has no knowledge of the forge application. The deliberate ignorance is a feature: it keeps cases at the industry-standard level instead of coupling them to a specific UI or implementation.

---

You are authoring manual test scenarios for an MRP/ERP system. **You have no direct knowledge of the application, and you should not seek any.** Your job is to enumerate what *any* well-built MRP/ERP must do to be fully usable in a real manufacturing business, then write test cases against that industry standard. The tester translates your industry-level case into clicks at run time.

## Read this first

The repo at `e:\dev\forge\forge-test\` is a manual test library plus a browser-based test runner. Before writing anything:

1. `docs/test-scenarios.md` — philosophy and authoring conventions
2. `docs/01-schema.md` — YAML schema for cases, manifests, flows, stories
3. `docs/glossary.md` — shared terminology
4. `docs/expansion-plan.md` — gaps already identified
5. Each phase manifest (`docs/04-phase-0-manifest.md` through `docs/14-phase-5-manifest.md`) — what's already covered

Do **not** read application source code, even if pointed at it. The library's value depends on staying app-agnostic.

## Operating principle

Write cases at the level of: *"This is what any reasonable buyer would expect from an MRP/ERP worth its license fee."*

- **Yes:** "An invoice can be voided after posting, and the void reverses GL postings while preserving the audit trail."
- **No:** "Click the three-dot menu on the invoice row, choose 'Void', confirm in the modal."

The first describes what a competent system *does*. The second describes how *one specific UI* does it. Write the first kind. If the app can't satisfy a reasonable case, that is an *application* finding — never soften the case to fit observed behavior.

## What "fully usable MRP/ERP" means

A buyer evaluating any manufacturing-focused ERP expects competent coverage of every area below. Use this as your gap-finding checklist. For each area, compare to what the library covers today and identify missing cases.

### 1. Tenant & identity
Multi-tenancy isolation, user provisioning (manual + bulk + SSO), role/permission matrix (every role × every capability), session/MFA, password reset, account lockout, API tokens, audit log of admin actions.

### 2. Master data — every entity must support
Create, read, update, deactivate (soft delete), bulk import (CSV), bulk export, search, filter, sort, paginate, duplicate detection, merge, attachment, custom fields, change history. Entities: customers, vendors, parts (raw / WIP / FG / service), BOMs (with revisions and effectivity dates), routings (with alternates and subcontract ops), locations, work centers, employees, fixed assets, contracts, price lists, tax codes, GL accounts, payment terms, units of measure, currencies.

### 3. Procure-to-pay
Requisition → approval → RFQ → vendor quote comparison → PO → receipt (full / partial / over / under / damaged) → 3-way match → AP invoice → payment (single / batch / partial / overpayment) → vendor return → vendor credit memo.

### 4. Order-to-cash
Lead → opportunity → quote (revisions) → sales order (with credit limit check) → work order → pick → pack → ship (full / partial / split) → customer invoice → cash receipt (full / partial / over / batch / lockbox) → AR aging → collection → RMA → credit memo.

### 5. Manufacturing execution
Work order release, material issue (full kit / pull / backflush), labor reporting, machine time, completion (good / scrap / rework), QC gates, stoppage tracking, operator clock in/out, multi-operation routing, parallel ops, subcontract send-out and receive-back, WO variance reporting.

### 6. Planning
MRP / MPS, demand forecast, supply planning, capacity planning (finite + infinite), safety stock & reorder logic, replenishment recommendations, drop ship, back-to-back, available-to-promise (ATP), capable-to-promise (CTP).

### 7. Inventory & warehouse
Cycle count, physical inventory, bin transfer, reservation, allocation, lot/serial tracking, expiry, FIFO/LIFO/Average/Standard costing, multi-location, putaway, pick wave, replenishment, hazmat handling, packaging.

### 8. Quality & compliance
Inspection plans, NCR (non-conformance), CAPA, FMEA, PPAP, SPC charts, gage calibration, certificate of analysis, recall by lot, warranty tracking, regulatory traceability.

### 9. Maintenance & assets
Preventive maintenance scheduling, breakdown work order, spare parts, asset tree, depreciation (straight-line / declining-balance / units-of-production), asset transfer, retirement, capitalization vs expense.

### 10. Finance & close
GL postings tied to every transaction, journal entries (manual + recurring + reversing), bank reconciliation, multi-currency revaluation, tax (sales / VAT / GST / withholding / exemption), period close (sub-ledger reconciliation, period lock, year-end roll), inter-company eliminations.

### 11. HR & labor
Hire → onboard → assign role → first task. Termination, leave, training & certification, skills matrix, time tracking → payroll feed, shift management.

### 12. Reporting & analytics
Standard reports, each tied out to a known transaction set: P&L, balance sheet, cash flow, trial balance, AR aging, AP aging, inventory valuation, WO variance, MRP exception, capacity utilization, sales by customer / product / region, vendor performance, employee labor distribution, OEE, depreciation schedule.

### 13. Cross-cutting (the highest-ROI gaps)
- **Permissions matrix:** every (role, capability) pair. The library spot-checks one.
- **Negative variants:** each input case needs at least one variant for empty / invalid / boundary / state-conflict / permission-denied / optimistic-lock.
- **Edge cases:** fiscal-year boundary, DST transition, leap year, decimal precision, FX rounding, tax-rate change mid-period, very large lists (5,000+ rows).
- **Audit trail:** every state-changing action logged with who / what / when / before / after.
- **Concurrency:** two users edit same record; reservation race; period-close race against a late-posting transaction.
- **Notifications & alerts:** low stock, overdue PO/PM, approval reminders, AR aging triggers — fire under the right conditions, surface in the right channels.
- **Bulk operations:** mass update, mass delete, mass status change, mass reassign.
- **Search & filter UX per list view:** partial match, status filter, date range, multi-column sort, pagination over 5,000 rows.
- **Documents:** generation, email, print, attach to record (PO, invoice, packing slip, BOL, statement).
- **Integrations (generic):** accounting sync (do not name a provider), file-based import/export, EDI document classes (850 / 855 / 856 / 810).

## Output

For each gap you identify:

1. **New case file** under `docs/cases/{phase}/{ID}.md` using the schema in `docs/01-schema.md`. ID prefix matches phase (e.g. `P5-CLOSE-005`) or, for cross-phase suites, follow `docs/expansion-plan.md` conventions (`PERM-{ROLE}-{CAP}-NNN`, `RPT-{REPORT}-NNN`, `EDGE-DATE-NNN`, etc.).
2. **Manifest update** in the relevant `docs/{NN}-phase-{N}-manifest.md` — sequence position, required/optional, `prerequisite_cases`, `scale_tags`.
3. **Suite manifest** if a category warrants its own (`docs/suites/{name}/manifest.md`) — recommended for permissions, reports, edge cases, concurrency, audit.
4. **Negative variants** on existing cases: add to the parent case's `negative_variants` field, do not create a separate file.

## Authoring discipline

- One case = one verifiable outcome. If you need an "OR", split the case.
- Plain English. The runner's audience ranges from inexperienced testers to senior IT staff.
- Cases describe what *should* work. If the app can't, that is an app bug — do not soften.
- Tag a case with a flow only if the flow genuinely depends on it. Don't dilute flow signal.
- Estimate `estimated_minutes` honestly. If unsure, write a defensible upper bound and mark it as such.
- Do **not** edit existing cases except to add `negative_variants`.
- Do **not** touch `test-bed/` (the runner). You are authoring content only.

## YAML traps to avoid

- **Colon-followed-by-space inside a precondition or step body:** YAML parses `- Either: X` or `- Note: Y` as a one-key map, not a string. The runner then renders it as `[object Object]`. Fix: wrap in a `|` block scalar — `- |\n    Either X, OR Y` — or quote the whole string.
- **Tabs inside YAML:** never. Spaces only. Indent at 2 spaces consistently within a block.
- **Trailing whitespace inside multi-line block scalars:** strips inconsistently across parsers; avoid.

## When you finish, produce a short summary

- Cases added per area (counts)
- Negative variants added to existing cases (count)
- Any area you intentionally skipped, with reason (e.g., "concurrency suite needs runner support not yet built")
- Any area where the existing library is already better than what you would have written, so you left it alone

The goal is not maximum case count. The goal is: a buyer running this library against the system gets a defensible verdict on whether the system is fit to operate a real manufacturing business.
