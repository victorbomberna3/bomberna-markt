# CLAUDE.md

Operating instructions for Claude Code sessions on this project. Read this first.

## What this is
A two-function tool for the Bomberna family business to use at the weekly farmers
market (Wednesday and Saturday, one fixed location in Belgium, Knokke-Heist):

1. **Market tracker** - log each market day (date, revenue, staff count, note) and
   see season trends.
2. **Invoice request** - capture B2B customer details at the stall and send a clean,
   structured email to the administration office (bomberna@info.be), who raise the formal invoice.

## Architecture (decided)
A split, not a single app. Do not try to merge these.

- **Frontend** (`frontend/`): a static, dependency-free web app that runs in a phone
  browser at the stall. Must work offline and one-handed. No build step. No framework
  that needs compilation unless explicitly decided in DECISIONS.md. This is the
  stall-facing tool. Python does NOT run here.
- **Analysis / backend** (`analysis/`): Python. Scope depends on OPEN QUESTION 1 in
  DECISIONS.md (offline CSV analysis vs live FastAPI backend). Do not build beyond the
  decided scope.

## Hard conventions
- **No em dashes anywhere.** Not in code comments, not in copy, not in docs. Use commas,
  colons, or full stops.
- **Customer-facing copy is Dutch, formal `u` register.** Warm but not flowery. The only
  customer-facing surface right now is the invoice email body and the UI labels.
- **Code, comments, commit messages, and these docs are English.**
- **Mobile-first.** Large tap targets, single column, works without signal.
- **Small, reviewable commits.** Prefer many small diffs over one large one. When a change
  is large, describe the plan and wait for confirmation before writing it.
- **Be honest about trade-offs.** Flag when a request is unrealistic or adds disproportionate
  complexity. Do not gold-plate.

## File layout
```
bomberna-markt/
  CLAUDE.md            this file
  README.md            how to run
  docs/
    PROBLEM.md         business context and problem statement
    REQUIREMENTS.md    functional requirements and field definitions
    ARCHITECTURE.md    the split, rationale, the two Python paths
    DECISIONS.md       decisions made + OPEN QUESTIONS (answer these first)
    PROGRESS.md        status and next steps
  frontend/
    index.html         working prototype v0 (single self-contained file)
  analysis/            Python layer (scope pending OPEN QUESTION 1)
```

## Before starting work
Check `docs/DECISIONS.md`. There are open questions that fork the architecture. Do not
build the Python layer or change the invoice end-to-end flow until they are answered.
