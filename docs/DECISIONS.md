# DECISIONS

## Decided
- One tool, two functions (market tracker + invoice request), shared foundation.
- Frontend stays a static, offline-capable phone web app. Python does not replace it.
- Invoice capture must include order description and amount incl. btw (admin cannot
  invoice without them). Customer email added as optional but recommended.
- Storage in the frontend: localStorage with in-memory fallback.
- Dutch UI and email copy, formal `u` register. No em dashes anywhere.
- Belgian ondernemingsnummer captured with a format hint, no hard validation (must not
  block entry at the stall).

## OPEN QUESTIONS (answer before building the Python layer)

### Q1. What is the Python layer for?
- [ ] **Path A** - offline analysis on the Mac, ingests exported CSV. (Recommended start.)
- [ ] **Path B** - live FastAPI backend with database and phone sync.
- Notes / answer:

### Q2. Where does the invoice flow end?
- [ ] **Feed admin** - keep emailing structured details; admin's system makes the invoice.
- [ ] **Generate here** - the tool produces the formal invoice (PDF, numbering, btw, archive).
- Notes / answer:

### Q3. What does the admin office invoice with?
- Software in use (Octopus / Yuki / Exact / WinBooks / Billit / other / none):
- Does it have an import format or API we should target?
- Notes / answer:

## Smaller open points (do not block)
- Should the invoice email also CC the customer, or only admin?
- Do we want a tappable shortlist of common products instead of typing the description?
- Durable backup for the season data: weekly CSV email is the stopgap; a Google Sheet via
  a small Apps Script endpoint is the likely low-effort durable option if Path A is chosen.
