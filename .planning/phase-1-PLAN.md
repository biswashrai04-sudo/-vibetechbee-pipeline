# Phase 1: Brand Setup — PLAN.md

## Goal
Create `/social-brand-setup` command that interactively captures brand identity via 3-questions-at-a-time Q&A, outputting `brain/BRAND_GUIDE.md`.

## Task List

### Wave 1 — Command File

- [ ] Create `commands/social-brand-setup.md`
  - Use `question` tool with 3-questions-at-a-time batches
  - Capture: brand voice, platform tone, visual style, content pillar ratios, competitors
  - Follows the interactive questioning pattern from GSD question.md reference
  - Outputs structured `brain/BRAND_GUIDE.md`
  - Includes graceful degradation note: agents use built-in defaults if BRAND_GUIDE.md missing

## Verification

- [ ] File exists at `commands/social-brand-setup.md`
- [ ] References `question` tool correctly
- [ ] 3-questions-at-a-time batching
- [ ] Outputs to `brain/BRAND_GUIDE.md`
- [ ] Mentions degradation fallback
