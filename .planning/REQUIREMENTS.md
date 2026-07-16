# VibeTechBee — Requirements

## v1 Requirements

### Brand Setup

- [ ] SETUP-01: Interactive Q&A flow (3 questions at a time via `question` tool) to capture brand voice, platform tone per channel, visual style preferences, content pillar ratios, competitor references
- [ ] SETUP-02: Outputs `brain/BRAND_GUIDE.md` with structured brand identity consumed by all agents
- [ ] SETUP-03: Graceful degradation — if BRAND_GUIDE.md missing, agents use built-in VibeTechBee defaults

### Trend Discovery

- [ ] TREND-01: Scanner fetches trends from X trending, Reddit, Google Trends, Product Hunt, TechCrunch, Google News for all 7 niches
- [ ] TREND-02: Scanner scores by velocity × reach × engagement, deduplicates against 7-day history
- [ ] TREND-03: Selector picks best candidate using weighted scoring, dedup against calendar, day-of-week niche fit check
- [ ] TREND-04: Outputs `01-TREND.md` with raw scan results from 5+ sources

### Verification & Research

- [ ] VERIFY-01: Freshness gate checks publish dates are within 48 hours
- [ ] VERIFY-02: Sentiment gate auto-rejects negative topics and signals retry loop
- [ ] VERIFY-03: Max 3 retries — if all fail, triggers evergreen fallback
- [ ] VERIFY-04: Fallback generates safe, brand-compatible topic from brand knowledge base
- [ ] VERIFY-05: Researcher extracts facts, statistics, and quotes from 3+ sources with competitor differentiation
- [ ] VERIFY-06: Outputs `02-RESEARCH.md` with deep research + competitor analysis

### Strategy

- [ ] STRAT-01: Stage A reads research + brand guide + last 3 calendar entries, assigns platform angles, tone, format, writes core message
- [ ] STRAT-02: Stage B reads Stage A output with fresh context, generates hooks, CTAs, engagement tactics, keywords, visual direction, timing
- [ ] STRAT-03: Outputs `03-STRATEGY.md` with platform-specific tactical briefs

### Content Writing

- [ ] WRITE-01: IG Writer produces carousel caption (125-150 words), 5 hashtags, slide text, story hook — optimized for DM shares
- [ ] WRITE-02: LI Writer produces thought leadership (800-1200 chars) with Hook → Context → Insight bullets → CTA structure — optimized for dwell time
- [ ] WRITE-03: X Writer produces tweet or thread (3-7 tweets) with ## Character Audit appendix counting chars per tweet — 280 hard limit — optimized for replies
- [ ] WRITE-04: FB Writer produces community discussion post (~300 chars) with trigger word check — optimized for meaningful interactions
- [ ] WRITE-05: All 4 writers obey CORE_MESSAGE from strategy
- [ ] WRITE-06: Outputs `04-CONTENT/{instagram,linkedin,x,facebook}.md`

### Image Generation

- [ ] IMAGE-01: Reads OPENROUTER_API_KEY from `.env`, POSTs to `https://openrouter.ai/api/v1/chat/completions`
- [ ] IMAGE-02: Generates 1 image per platform at correct dimensions: IG 1080×1350, LI 1200×627, X 1500×500, FB 1200×630
- [ ] IMAGE-03: Model fallback chain: black-forest-labs/flux.2-max → flux.1.1-pro → flux-schnell → IMAGE_PROMPTS.md
- [ ] IMAGE-04: Brand style applied from BRAND_GUIDE.md with alt text per image
- [ ] IMAGE-05: Outputs `05-IMAGES/{prompts.md, *.png}`

### Packaging & Approval

- [ ] PACK-01: Organizes all outputs into date-topic folder
- [ ] PACK-02: Cross-checks all 4 posts against CORE_MESSAGE for contradictions
- [ ] PACK-03: Creates `06-CHECKLIST.md` with 1-line previews + optimal posting order: LI 8:30AM → X 9AM → IG 11AM → FB 7PM
- [ ] PACK-04: Updates `brain/CONTENT_CALENDAR.md` with new entry
- [ ] APPROVE-01: `/social-approve` command logs approved posts and marks calendar entry as published

### Orchestrator

- [ ] ORCH-01: `social-posting.skill.md` sequences all 8 waves with proper error handling
- [ ] ORCH-02: `/social-post daily` triggers the full pipeline
- [ ] ORCH-03: Parallel agents within waves (Wave 1, 2, 4), sequential between waves

## v2 Requirements (Deferred)

- [ ] Feedback loop agent — analyzes engagement data, adjusts strategy
- [ ] Direct posting to platforms via API
- [ ] Video/reel generation
- [ ] Multi-language support

## Out of Scope

- Auto-posting without human approval — explicit design decision
- Real-time social listening / monitoring
- Analytics dashboard
- User authentication system

## Traceability

| REQ-ID | Phase | Plan | Verified |
|--------|-------|------|----------|
| SETUP-01 | 1 | — | — |
| SETUP-02 | 1 | — | — |
| SETUP-03 | 1 | — | — |
| TREND-01 | 2 | — | — |
| TREND-02 | 2 | — | — |
| TREND-03 | 2 | — | — |
| TREND-04 | 2 | — | — |
| VERIFY-01 | 3 | — | — |
| VERIFY-02 | 3 | — | — |
| VERIFY-03 | 3 | — | — |
| VERIFY-04 | 3 | — | — |
| VERIFY-05 | 3 | — | — |
| VERIFY-06 | 3 | — | — |
| STRAT-01 | 4 | — | — |
| STRAT-02 | 4 | — | — |
| STRAT-03 | 4 | — | — |
| WRITE-01 | 5 | — | — |
| WRITE-02 | 5 | — | — |
| WRITE-03 | 5 | — | — |
| WRITE-04 | 5 | — | — |
| WRITE-05 | 5 | — | — |
| WRITE-06 | 5 | — | — |
| IMAGE-01 | 6 | — | — |
| IMAGE-02 | 6 | — | — |
| IMAGE-03 | 6 | — | — |
| IMAGE-04 | 6 | — | — |
| IMAGE-05 | 6 | — | — |
| PACK-01 | 7 | — | — |
| PACK-02 | 7 | — | — |
| PACK-03 | 7 | — | — |
| PACK-04 | 7 | — | — |
| APPROVE-01 | 7 | — | — |
| ORCH-01 | 8 | — | — |
| ORCH-02 | 8 | — | — |
| ORCH-03 | 8 | — | — |

---
*Last updated: 2026-07-16 after initialization*
