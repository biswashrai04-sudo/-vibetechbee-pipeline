# VibeTechBee — Project Context

## What This Is

A daily multi-agent content creation pipeline that generates ready-to-post social media content across **4 platforms** — Instagram, LinkedIn, X, and Facebook. 13 specialized AI agents work across 8 sequential waves to scan trends, research topics, craft strategy, write platform-optimized copy, generate images, and package everything into a ready-to-review checklist.

**Runtime:** opencode (AI runtime) — uses `task()` subagent spawning  
**Output:** `social-posts/YYYY-MM-DD-topic/` — human approval gate, no auto-posting  
**Standalone:** Portable project folder, git-tracked, opencode as runtime only

## Core Value

Generating platform-optimized, engagement-maximized social media content across 4 platforms daily, with zero manual drafting — each platform's #1 algorithmic signal drives the writing.

## Constraints

- **No auto-posting** — human must approve via `/social-approve`
- **Image gen via OpenRouter** — requires `OPENROUTER_API_KEY` in `.env`
- **opencode runtime only** — no external servers, no databases, no build step
- **Must handle credit exhaustion** — fallback to IMAGE_PROMPTS.md when OpenRouter credits gone
- **Freshness requirement** — topics must be <48hr old, negative topics auto-rejected
- **Char limits** — X/Twitter 280 chars hard limit, Facebook trigger-word check

## Target Audience

Social media managers and content creators in the tech niche running VibeTechBee brand.

## Brand Identity

- **Colors:** Navy `#2F4156` · Teal `#567C8D` · Sky Blue `#C8D9E6` · Beige `#F5EFEB` · White `#FFFFFF`
- **Voice:** Varies by platform (energetic IG, authoritative LI, punchy X, friendly FB)
- **Niche rotation (7-day):** Mon=Tech, Tue=AI Productivity, Wed=Apps, Thu=Business, Fri=Gadgets/Mobile, Sat=Real Estate, Sun=Wildcard

## Architecture

**13 agents across 8 waves:**

| Wave | Phase | Agents | Mode |
|------|-------|--------|------|
| 0 | Brand Setup | Brand Strategist | Run once |
| 1 | Trend Discovery | Trend Scanner, Topic Selector | Parallel |
| 2 | Verification & Research | Freshness Verifier, Evergreen Fallback, Researcher | Parallel |
| 3 | Strategy | Matrix Strategist → Tactical Strategist | Sequential |
| 4 | Content Writing | IG Writer, LI Writer, X Writer, FB Writer | Parallel (4x) |
| 5 | Image Generation | Gemini Visual Creator | Solo |
| 6 | Package & Deliver | Delivery Manager | Solo |
| 7 | Human Approval | User | Manual gate |

**3 Custom Commands:** `/social-post daily`, `/social-brand-setup`, `/social-approve`

**1 Orchestrator Skill:** `social-posting.skill.md` — wave sequencing, agent spawning, retry logic

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Split strategist into Stage A+B | Prevent context overload in a single agent | Two-stage with fresh context per stage |
| Wave 2 includes retry loop | Fresh topics that fail freshness check should retry, not fail immediately | Max 3 retries before evergreen fallback |
| Image gen fallback chain | No free image models on OpenRouter, so models escalate | gemini-2.5-flash-image → gemini-3.1-flash-lite → gemini-3.1-flash → IMAGE_PROMPTS.md |
| Brand setup as Wave 0 (separate command) | Setup runs once, not daily | `/social-brand-setup` outputs BRAND_GUIDE.md |
| Packager does cross-writer consistency | Writers run parallel, need final check | Packager cross-checks all posts against CORE_MESSAGE |
| GitHub Pages for architecture docs | architecture.html is a static asset | Hosted at biswashrai04-sudo.github.io/-vibetechbee-pipeline/ |

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] PIPELINE-01: Brand setup command collects brand voice, platform tone, visual style, pillar ratios
- [ ] PIPELINE-02: Trend scanner fetches from 5+ sources across 7 niches
- [ ] PIPELINE-03: Topic selector picks best candidate by weighted scoring
- [ ] PIPELINE-04: Freshness verifier checks publish dates <48hr and runs sentiment analysis
- [ ] PIPELINE-05: Evergreen fallback generates from brand knowledge when pipeline empties
- [ ] PIPELINE-06: Researcher extracts facts/stats/quotes from 3+ sources
- [ ] PIPELINE-07: Strategist Matrix assigns angles/tone/format per platform with yesterday-awareness
- [ ] PIPELINE-08: Strategist Tactical generates hooks, CTAs, keywords, visual direction
- [ ] PIPELINE-09: IG Writer produces carousel caption (125-150 words) + hashtags + alt text
- [ ] PIPELINE-10: LI Writer produces thought leadership (800-1200 chars, hook/insight/CTA structure)
- [ ] PIPELINE-11: X Writer produces tweet/thread with ## Character Audit (≤280 per tweet)
- [ ] PIPELINE-12: FB Writer produces community post ~300 chars with trigger word check
- [ ] PIPELINE-13: Image gen calls OpenRouter API with model chain, saves PNGs per platform
- [ ] PIPELINE-14: Packager organizes output, creates CHECKLIST.md, updates CONTENT_CALENDAR.md
- [ ] PIPELINE-15: Approval command logs approved posts to calendar
- [ ] PIPELINE-16: Orchestrator skill sequences all 8 waves with proper error handling

### Out of Scope

- Auto-posting to social platforms — must remain manual
- Feedback loop / performance analytics (V2)
- Multi-day batch generation
- Video/reel generation

## Evolution

This document evolves at phase transitions and milestone boundaries.

**After each phase transition** (via `/gsd-transition`):
1. Requirements invalidated? → Move to Out of Scope with reason
2. Requirements validated? → Move to Validated with phase reference
3. New requirements emerged? → Add to Active
4. Decisions to log? → Add to Key Decisions
5. "What This Is" still accurate? → Update if drifted

**After each milestone** (via `/gsd-complete-milestone`):
1. Full review of all sections
2. Core Value check — still the right priority?
3. Audit Out of Scope — reasons still valid?
4. Update Context with current state

---
*Last updated: 2026-07-16 after initialization*
