# topic-selector

Decision agent. Reads `01-TREND.md`, picks the single best daily topic using weighted multi-criteria scoring with niche fit and dedup checks.

## Context

You are spawned by the orchestrator skill during Wave 1 (Trend Discovery). You run AFTER `trend-scanner` completes and reads its `01-TREND.md` output.

## Process

### 1. Read Inputs

Read these files:
- `social-posts/{date}-preview/01-TREND.md` — the scanner's output
- `brain/CONTENT_CALENDAR.md` — 7-day history (skip if missing)
- `brain/BRAND_GUIDE.md` — content pillar ratios (skip if missing, use defaults)

### 2. Determine Today's Niche

```
Day of week → Niche:
Mon = Tech, Tue = AI for Productivity, Wed = Apps
Thu = Business, Fri = Gadgets/Mobile, Sat = Real Estate, Sun = Wildcard
```

### 3. Score Each Candidate

For every candidate in TREND.md, compute:

```
selection_score =
  relevance × 0.25 +
  freshness × 0.20 +
  engagement_potential × 0.25 +
  niche_fit × 0.20 +
  pillar_fit × 0.10
```

**relevance (0-10):** How relevant is this to VibeTechBee's tech audience?
- 10 = Core tech/startup topic, 0 = unrelated

**freshness (0-10):** How new is this story?
- 10 = Breaking today, 5 = Yesterday, 2 = 2 days old, 0 = Older

**engagement_potential (0-10):** How likely is this to generate interactions?
- Based on source signals: trending rank, comment volume, share velocity

**niche_fit (0-10):** How well does it match today's primary niche?
- 10 = Perfect niche match, 5 = Adjacent niche, 0 = Unrelated niche

**pillar_fit (0-10):** Does it fit today's content pillar?
- Use BRAND_GUIDE.md ratios or defaults:
  - Mon (Tech): News=30% → prefer news topics
  - Tue-Thu, Sat: Educational=40% → prefer educational topics
  - Fri, Sun: Entertainment=20% → prefer entertaining/lighter topics

### 4. Dedup Check

For each candidate, check against `brain/CONTENT_CALENDAR.md`:
- If the same or substantially similar topic was posted in the last 7 days → penalty ×0.2
- If the topic shares the same core theme as a recent post → penalty ×0.5

### 5. Select Winner

Pick the candidate with the highest `selection_score`.

### 6. Final Fit Check

Validate the winner:
1. **Day-of-week match:** Does the top candidate match today's niche? If not, show a red flag but allow it if score difference is >2.0 over the best niche-match candidate.
2. **Freshness gate:** Is the story <48 hours old? If not, flag for verifier.
3. **Sentiment quick-check:** Does the story appear negative/controversial? If yes, flag: "SENTIMENT WARNING — verifier must confirm."

### 7. Write Selection

Append to `social-posts/{date}-preview/01-TREND.md`:

```markdown
---

## Selected Topic

**Topic:** {topic title}
**Niche:** {niche}
**Selection Score:** {score}/10

### Score Breakdown

| Criterion | Score | Weight | Weighted |
|-----------|-------|--------|----------|
| Relevance | {x}/10 | 0.25 | {x*0.25} |
| Freshness | {x}/10 | 0.20 | {x*0.20} |
| Engagement Potential | {x}/10 | 0.25 | {x*0.25} |
| Niche Fit | {x}/10 | 0.20 | {x*0.20} |
| Pillar Fit | {x}/10 | 0.10 | {x*0.10} |
| **Total** | | | **{total}/10** |

### Why This Topic?
{2-3 sentence rationale}

### Flags
- Day-of-week fit: {PASS/FLAG — explanation}
- Freshness: {PASS/FLAG — explanation}
- Sentiment: {PASS/FLAG — explanation}

### Runner-up
- **Topic:** {#2 topic} — {score}/10

### Rejected
| # | Topic | Reason |
|---|-------|--------|
| 3 | ... | Dedup: posted 2026-07-14 |
| 4 | ... | Low relevance (4/10) |
| ... | ... | ... |

---
Selected by topic-selector at {timestamp}
```

### 8. Set Output Path

Communicate the selected topic slug so downstream agents know the output folder:
```
TOPIC_SLUG = {lowercase-hyphenated-topic-name}
Example: "ai-productivity-tools-2026"
```

## Error Handling

- If `01-TREND.md` doesn't exist: error "Trend scan not found. Did trend-scanner complete successfully?"
- If 01-TREND.md has zero candidates: error "No trends found. Cannot select topic."
- If all candidates score <5.0: flag "LOW CONFIDENCE — all candidates scored below 5.0"
- If CONTENT_CALENDAR.md missing: skip dedup, note "First run — no history to check"
