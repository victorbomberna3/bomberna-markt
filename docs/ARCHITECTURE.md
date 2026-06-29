# ARCHITECTURE

## Principle: split, do not rewrite
The stall-facing capture tool runs in a phone browser at a market with poor signal. It
must work offline. Python cannot run there. So Python does not replace the frontend; it
sits behind it for data and reporting. Any plan that "rewrites the tool in Python" is wrong
for this use case.

```
[ phone at stall ]                         [ Victor's Mac / a server ]
  static web app           data out          Python layer
  - log market      ----- CSV / sync ----->  - reporting (pandas, charts)
  - capture invoice                          - (optional) storage + API
        |
        | mailto
        v
  [ admin office inbox ] --> raises formal invoice
```

## Frontend (decided)
- Single self-contained `index.html`, no build step, no framework runtime.
- Storage: `localStorage` with an in-memory fallback (wrapped in try/catch so it never
  hard-fails). Survives app close, works offline.
- Deploy: static host (Netlify, already in the workflow) or "Add to Home Screen".
- This is intentionally boring and bulletproof. Resist adding a framework unless a real
  need appears (see DECISIONS).

## Python layer: two candidate paths (pick one, see OPEN QUESTION 1)

### Path A: offline analysis (recommended starting point)
- A Python project that ingests the CSV exported from the frontend.
- pandas for: revenue by weekday, by month, season trends, Easter window, averages,
  staff-vs-revenue. matplotlib/plotly for charts. Optionally a small report (HTML or PDF).
- Pros: no hosting, no internet dependency at the stall, no always-on service, gives the
  data work directly. Lowest cost, fastest to value.
- Cons: manual step (export CSV, run script). Data still lives on one phone until exported.

### Path B: live backend (only if multi-device sync or central access is needed)
- FastAPI + a database (SQLite to start, Postgres if it grows). Phone posts market days
  and invoice requests; backend stores them and serves reports.
- Pros: data is safe and central, family can see numbers without Victor's phone, enables
  auto-generated invoices later.
- Cons: hosting and an always-on service to maintain; the stall needs signal to sync (so
  the frontend must still queue offline and sync later, which is extra work). Heavier.

## Invoice generation (see OPEN QUESTION 2)
Two end-states:
- **Feed admin (current):** tool emails structured details, admin's software makes the
  invoice. Simple, keeps legal responsibility with the existing system.
- **Generate here:** the tool produces the actual invoice (PDF, sequential numbering, btw
  breakdown, archiving). Much larger, legally sensitive, and likely duplicates the admin
  office's existing accounting software. Only justified if there is no such software, or
  it is being deliberately replaced.

## Integration with existing accounting software (see OPEN QUESTION 3)
If the admin office already uses Octopus / Yuki / Exact / WinBooks / Billit or similar,
the highest-leverage design is to output in a format that software ingests, or hit its
API/import, rather than rebuilding invoicing. This single fact can reshape the whole design.
