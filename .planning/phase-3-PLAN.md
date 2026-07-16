# Phase 3: Verification & Research — PLAN.md

## Goal
Create freshness verifier (gate agent), evergreen fallback (safety net), and researcher (deep dive) agents.

## Task List

### Wave 1 — All 3 agents in parallel

- [ ] Create `agents/freshness-verifier.md` — web-gate: date check, sentiment scan, retry signal
- [ ] Create `agents/evergreen-fallback.md` — safety net from brand knowledge base
- [ ] Create `agents/researcher.md` — extracts facts/stats/quotes from 3+ sources with competitor diff

## Verification

- [ ] Verifier checks publish dates <48hr and runs sentiment
- [ ] Verifier has max 3 retries logic
- [ ] Fallback generates from brand knowledge when pipeline empties
- [ ] Researcher requires 3+ sources minimum
- [ ] Researcher extracts structured facts, stats, and quotes
