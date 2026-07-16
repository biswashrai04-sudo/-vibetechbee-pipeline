# social-posting

VibeTechBee's multi-agent social media content pipeline orchestrator. Sequences 14 agents across 9 waves. Handles retry logic, fallback triggers, and output delivery.

## Overview

This skill is loaded by `/social-post daily`. It acts as the conductor — it does NOT write content itself. It spawns subagents via `task()` and manages the pipeline flow.

## Architecture

```
Wave 0: Brand Setup         ── run once (separate command, prerequisite)
  │
Wave 1: Trend Discovery     ── scanner + selector (parallel)
  │
Wave 2: Verification        ── verifier + fallback + researcher (parallel, retry loop)
  │
Wave 3: Strategy            ── matrix → tactical (sequential, fresh context)
  │
Wave 4: Content Writing     ── IG + LI + X + FB (parallel 4x)
  │
Wave 4.5: Prompt Engineering ── flux prompt optimizer (solo)
  │
Wave 5: Image Generation    ── flux visual creator (solo)
  │
Wave 6: Package & Deliver   ── packager (solo)
  │
Wave 7: Human Approval      ── open CHECKLIST.md, user approves
```

## Prerequisites Check

Before starting any wave, verify:
1. `brain/BRAND_GUIDE.md` exists — if not, warn: "Run /social-brand-setup first for best results. Proceeding with defaults."
2. `.env` has `OPENROUTER_API_KEY` — if not, note: "No API key — image gen will use fallback prompts."

## Today's Date & Niche

Determine today's date and niche:
```
Date: {YYYY-MM-DD} (auto-detected)
Day: {day of week}
Niche: Mon=Tech, Tue=AI Productivity, Wed=Apps, Thu=Business, Fri=Gadgets/Mobile, Sat=Real Estate, Sun=Wildcard
```

Create output directory:
```
D:/content/{date}-preview/
```

---

## Wave 1: Trend Discovery

### 1a. Spawn Trend Scanner — Input: Nothing. Output: 01-TREND.md

Spawn `trend-scanner` subagent:

```
task(
  subagent_type: "general",
  description: "Scan trends across 7 niches",
  prompt: """
Read agents/trend-scanner.md and execute it.
Today's date: {date}
Today's niche: {niche} (weight this niche 2x)
Output path: D:/content/{date}-preview/01-TREND.md
"""
)
```

Wait for completion.

### 1b. Spawn Topic Selector — Input: 01-TREND.md. Output: appends to 01-TREND.md

```
task(
  subagent_type: "general",
  description: "Select best daily topic",
  prompt: """
Read agents/topic-selector.md and execute it.
Read D:/content/{date}-preview/01-TREND.md
Today's niche: {niche}
Append selection to the same file.
"""
)
```

Wait for completion. Extract TOPIC_SLUG from the selector's output for folder naming.

---

## Wave 2: Verification & Research

### 2a. Spawn Freshness Verifier — Input: 01-TREND.md. Output: append verdict

```
task(
  subagent_type: "general",
  description: "Verify topic freshness",
  prompt: """
Read agents/freshness-verifier.md and execute it.
Read D:/content/{date}-preview/01-TREND.md
Append verification verdict to the same file.
"""
)
```

Wait for completion. Read the verdict.

### 2b. Retry Loop (max 3 attempts)

If verifier returns REJECT:
- Increment retry counter
- If retry count < 3:
  - Re-spawn `topic-selector` with exclusion list (rejected topic)
  - Re-spawn `freshness-verifier`
  - Check verdict again
- If retry count = 3:
  - Break loop
  - Trigger **Evergreen Fallback** (Step 2d)

### 2c. Spawn Researcher — Input: 01-TREND.md (verified topic). Output: 02-RESEARCH.md

Only IF verification passed:

```
task(
  subagent_type: "general",
  description: "Deep research on selected topic",
  prompt: """
Read agents/researcher.md and execute it.
Read D:/content/{date}-preview/01-TREND.md for the selected topic.
Write to D:/content/{date}-preview/02-RESEARCH.md
Require minimum 3 sources, 3 stats, 2 quotes.
"""
)
```

Spawn in parallel with verifier retry loop (they're independent).

### 2d. Trigger Evergreen Fallback (only if retry loop exhausted)

```
task(
  subagent_type: "general",
  description: "Generate evergreen fallback topic",
  prompt: """
Read agents/evergreen-fallback.md and execute it.
Today's niche: {niche}
Today's date: {date}
Write to D:/content/{date}-preview/01-TREND.md (overwrite).
"""
)
```

After fallback completes, re-spawn researcher with the fallback topic.

---

## Wave 3: Strategy

### 3a. Spawn Strategist Matrix — Input: RESEARCH.md, BRAND_GUIDE.md, calendar. Output: 03-STRATEGY.md

```
task(
  subagent_type: "general",
  description: "Strategy matrix — platform angles and core message",
  prompt: """
Read agents/strategist-matrix.md and execute it.
Read D:/content/{date}-preview/02-RESEARCH.md
Write to D:/content/{date}-preview/03-STRATEGY.md
Check last 3 calendar entries for yesterday-awareness.
Define CORE_MESSAGE and 4 platform angles.
"""
)
```

Wait for completion. **Critical:** This must complete before Stage B.

### 3b. Spawn Strategist Tactical — Input: 03-STRATEGY.md. Output: appends to 03-STRATEGY.md

```
task(
  subagent_type: "general",
  description: "Tactical brief — hooks, CTAs, engagement tactics",
  prompt: """
Read agents/strategist-tactical.md and execute it.
Read D:/content/{date}-preview/03-STRATEGY.md (only this file, no other context).
Append tactical brief to the same file.
Generate hooks, CTAs, keywords, visual direction, posting schedule.
"""
)
```

Wait for completion.

---

## Wave 4: Content Writing

Spawn ALL 4 writers in parallel:

```
task(agent, "IG writer", "Read agents/instagram-writer.md. Read D:/content/{date}-preview/03-STRATEGY.md. Write to D:/content/{date}-preview/04-CONTENT/instagram.md")
task(agent, "LI writer", "Read agents/linkedin-writer.md. Read D:/content/{date}-preview/03-STRATEGY.md. Write to D:/content/{date}-preview/04-CONTENT/linkedin.md")
task(agent, "X writer", "Read agents/x-writer.md. Read D:/content/{date}-preview/03-STRATEGY.md. Write to D:/content/{date}-preview/04-CONTENT/x.md")
task(agent, "FB writer", "Read agents/facebook-writer.md. Read D:/content/{date}-preview/03-STRATEGY.md. Write to D:/content/{date}-preview/04-CONTENT/facebook.md")
```

Wait for ALL 4 to complete.

---

## Wave 4.5: Prompt Engineering

```
task(
  subagent_type: "general",
  description: "Engineer Flux-optimized image prompts",
  prompt: """
Read agents/prompt-engineer.md and execute it.
Read D:/content/{date}-preview/03-STRATEGY.md for visual specs.
Read all 4 content files in D:/content/{date}-preview/04-CONTENT/
Read brain/BRAND_GUIDE.md for visual tone (use defaults if missing).
Engineer photorealistic prompts optimized for Flux model.
Write to D:/content/{date}-preview/05-IMAGES/prompts-engineered.md
"""
)
```

Wait for completion.

---

## Wave 5: Image Generation

```
task(
  subagent_type: "general",
  description: "Generate 4 platform images via OpenRouter",
  prompt: """
Read agents/image-gen.md and execute it.
Read D:/content/{date}-preview/05-IMAGES/prompts-engineered.md for prompts.
Read .env for OPENROUTER_API_KEY
Generate images and save to D:/content/{date}-preview/05-IMAGES/
Write prompts.md to same directory.
"""
)
```

Wait for completion.

---

## Wave 6: Package & Deliver

```
task(
  subagent_type: "general",
  description: "Package output, create CHECKLIST, update calendar",
  prompt: """
Read agents/packager.md and execute it.
Read all files in D:/content/{date}-preview/
Cross-check CORE_MESSAGE across all 4 posts.
Write D:/content/{date}-preview/06-CHECKLIST.md
Update brain/CONTENT_CALENDAR.md
"""
)
```

Wait for completion. Rename folder: `D:/content/{date}-preview/` → `D:/content/{date}-{topic-slug}/`

---

## Wave 7: Deliver to User

Display summary:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 🐝 Content Ready for {Date} ({Niche})
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Topic: {topic}
CORE_MESSAGE: "{message}"

Posts:
  📸 Instagram — {1-line preview}
  💼 LinkedIn  — {1-line preview}
  🐦 X/Twitter — {1-line preview}
  👥 Facebook  — {1-line preview}

Publish in order:
  1. LinkedIn — 8:30 AM
  2. X/Twitter — 9:00 AM
  3. Instagram — 11:00 AM
  4. Facebook — 7:00 PM

Output: D:/content/{date}-{topic}/
Check: D:/content/{date}-{topic}/06-CHECKLIST.md
Approve: /social-approve {date}
```

---

## Error Recovery Matrix

| Failure | Recovery |
|---------|----------|
| Trend scanner fails | Retry once; if still fails, go to Wave 2d (evergreen fallback) |
| Topic selector fails | Retry with next candidate; after 2 failures, go to fallback |
| Freshness verifier rejects | Retry selector + verifier (max 3 loops), then fallback |
| Researcher fails (no sources) | Continue with note — strategist can work with limited data |
| Strategist Stage A fails | Fatal — cannot proceed without CORE_MESSAGE. Abort. |
| Strategist Stage B fails | Continue with Stage A only — writers use basic hooks/CTAs |
| Any 1 writer fails | Continue with remaining writers. Flag in packager. |
| All 4 writers fail | Fatal — no content to deliver. Abort. |
| Prompt engineer fails | Continue — image-gen falls back to raw strategist prompts |
| Image gen fails (all models) | Continue — packager notes missing images, CHECKLIST.md has prompts for manual gen |
| Packager fails | Manual: create CHECKLIST.md from existing files. Do not abort. |

## State Cleanup

After completion (success or partial):
- Log results to STATE.md
- Remove `-preview` suffix from output folder
- Commit checkpoint (if git_tracking enabled)
