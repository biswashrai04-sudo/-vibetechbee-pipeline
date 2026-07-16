# VibeTechBee — Roadmap

## Milestone: v1.0 — Complete Pipeline

**Goal:** Build all 13 agents, 3 commands, 1 orchestrator skill, and supporting files.

**Success Criteria:** Run `/social-post daily` and get a complete `social-posts/YYYY-MM-DD-topic/` output folder with 4 ready-to-post platform messages and images.

---

## Phase 0: Foundation

**Goal:** Create directory scaffolding, `.env.example`, seed files for fallback and calendar.

**Deliverables:**
- `agents/` directory
- `commands/` directory
- `brain/` directory with `IMAGE_PROMPTS.md` (seed fallback prompts)
- `brain/CONTENT_CALENDAR.md` (empty template)
- `social-posts/` directory
- `.env.example` with `OPENROUTER_API_KEY=your_key_here`

**Dependencies:** None

**Mode:** Setup

---

## Phase 1: Brand Setup

**Goal:** Create `/social-brand-setup` command that interactively captures brand identity.

**Deliverables:**
- `commands/social-brand-setup.md`

**Requirements:** SETUP-01, SETUP-02, SETUP-03

**Dependencies:** Phase 0

**Mode:** Setup

---

## Phase 2: Trend Discovery

**Goal:** Create trend scanner and topic selector agents for daily topic discovery.

**Deliverables:**
- `agents/trend-scanner.md`
- `agents/topic-selector.md`

**Requirements:** TREND-01, TREND-02, TREND-03, TREND-04

**Dependencies:** Phase 0

**Mode:** Build

---

## Phase 3: Verification & Research

**Goal:** Create freshness verifier, evergreen fallback, and researcher agents.

**Deliverables:**
- `agents/freshness-verifier.md`
- `agents/evergreen-fallback.md`
- `agents/researcher.md`

**Requirements:** VERIFY-01, VERIFY-02, VERIFY-03, VERIFY-04, VERIFY-05, VERIFY-06

**Dependencies:** Phase 2 (reads TREND.md to verify)

**Mode:** Build

---

## Phase 4: Strategy

**Goal:** Create two-stage strategy agent (Matrix + Tactical) for daily content strategy.

**Deliverables:**
- `agents/strategist-matrix.md`
- `agents/strategist-tactical.md`

**Requirements:** STRAT-01, STRAT-02, STRAT-03

**Dependencies:** Phase 3 (reads RESEARCH.md for strategy inputs)

**Mode:** Build

---

## Phase 5: Content Writing

**Goal:** Create all 4 platform-specific writer agents.

**Deliverables:**
- `agents/instagram-writer.md`
- `agents/linkedin-writer.md`
- `agents/x-writer.md`
- `agents/facebook-writer.md`

**Requirements:** WRITE-01, WRITE-02, WRITE-03, WRITE-04, WRITE-05, WRITE-06

**Dependencies:** Phase 4 (reads STRATEGY_TACTICAL.md)

**Mode:** Build

---

## Phase 6: Image Generation

**Goal:** Create image generation agent using OpenRouter API with model fallback chain.

**Deliverables:**
- `agents/image-gen.md`

**Requirements:** IMAGE-01, IMAGE-02, IMAGE-03, IMAGE-04, IMAGE-05

**Dependencies:** Phase 5 (reads content for visual prompts)

**Mode:** Build

---

## Phase 7: Packaging & Approval

**Goal:** Create packager agent and approval command for final delivery.

**Deliverables:**
- `agents/packager.md`
- `commands/social-approve.md`

**Requirements:** PACK-01, PACK-02, PACK-03, PACK-04, APPROVE-01

**Dependencies:** Phase 6 (packages all prior output)

**Mode:** Build

---

## Phase 8: Orchestrator

**Goal:** Create the master skill file and daily trigger command that ties everything together.

**Deliverables:**
- `social-posting.skill.md`
- `commands/social-post-daily.md`

**Requirements:** ORCH-01, ORCH-02, ORCH-03

**Dependencies:** Phases 0-7 (orchestrates all agents)

**Mode:** Glue

---

## Phase Execution Order

```
Phase 0 → Phase 1 → Phase 2 → Phase 3 → Phase 4 → Phase 5 → Phase 6 → Phase 7 → Phase 8
  │         │         │         │         │         │         │         │         │
  └─Foundation         └─reads TREND.md    └─reads RESEARCH.md  └─reads STRATEGY    └─reads content       └─orchestrates
                                                                  │                  │                     all agents
                                                                  └─reads STRATEGY   └─reads content
```

## Coverage

| Phase | Requirements Covered |
|-------|---------------------|
| 0 | (Infrastructure) |
| 1 | SETUP-01, SETUP-02, SETUP-03 |
| 2 | TREND-01, TREND-02, TREND-03, TREND-04 |
| 3 | VERIFY-01, VERIFY-02, VERIFY-03, VERIFY-04, VERIFY-05, VERIFY-06 |
| 4 | STRAT-01, STRAT-02, STRAT-03 |
| 5 | WRITE-01, WRITE-02, WRITE-03, WRITE-04, WRITE-05, WRITE-06 |
| 6 | IMAGE-01, IMAGE-02, IMAGE-03, IMAGE-04, IMAGE-05 |
| 7 | PACK-01, PACK-02, PACK-03, PACK-04, APPROVE-01 |
| 8 | ORCH-01, ORCH-02, ORCH-03 |

---
*Last updated: 2026-07-16 after initialization*
