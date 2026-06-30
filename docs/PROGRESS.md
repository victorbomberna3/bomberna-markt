# PROGRESS

## Status: v0 prototype, scoping the Python layer

### Done
- v0 frontend prototype: `frontend/index.html`. Self-contained, mobile-first.
  - Market tab: date (with weekday), revenue, staff, note; running totals; simple bar
    chart (Saturdays distinguished); CSV export; email-overview stopgap.
  - Invoice tab: full B2B field set incl. order description and amount; builds a structured
    Dutch email to admin via mailto; copy-to-clipboard; editable admin email in settings.
  - Storage: localStorage with in-memory fallback.

### Next (blocked on DECISIONS Q1 to Q3)
1. Answer the three open questions in DECISIONS.md.
2. If Path A: scaffold the Python analysis project (pandas + charts) that reads the
   exported CSV. Define the report it produces.
3. If Path B: scaffold FastAPI + SQLite, define the sync contract, add offline queue +
   sync to the frontend.
4. Resolve invoice end-state (Q2) and accounting integration (Q3) before building anything
   invoice-related beyond the current email flow.

### Cleanup
- Dead `.row` and `.row .field` CSS rules to remove on next CSS pass (columns removed, rules left in place).

### Later
- Durable season storage (Google Sheet via Apps Script, or the Path B database).
- Optional product shortlist for faster invoice entry.
- Tidy the frontend styling once the flow is settled (it is intentionally minimal now).
