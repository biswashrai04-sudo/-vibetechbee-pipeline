# Phase 2: Trend Discovery — PLAN.md

## Goal
Create trend-scanner and topic-selector agents that discover and select the best daily topic from 7 niches across 5+ sources.

## Task List

### Wave 1 — Trend Scanner

- [ ] Create `agents/trend-scanner.md`
  - Scans 7 niches using `webfetch` across X trending, Reddit, Google Trends, Product Hunt, TechCrunch, Google News
  - Scores each candidate by velocity × reach × engagement
  - Deduplicates against 7-day history from CONTENT_CALENDAR.md
  - Outputs `01-TREND.md` with scored candidates

### Wave 2 — Topic Selector

- [ ] Create `agents/topic-selector.md`
  - Reads `01-TREND.md`
  - Applies weighted scoring: relevance × freshness × engagement potential × niche fit
  - Checks day-of-week niche match
  - Deduplicates against CONTENT_CALENDAR.md
  - Returns single selected topic with rationale

## Verification

- [ ] `agents/trend-scanner.md` exists and references webfetch correctly
- [ ] `agents/topic-selector.md` exists and reads 01-TREND.md
- [ ] Scanner covers all 7 niches and 5+ sources
- [ ] Selector uses weighted scoring with documented weights
- [ ] Both agents handle CONTENT_CALENDAR.md absent case gracefully
