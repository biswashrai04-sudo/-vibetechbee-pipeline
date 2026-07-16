# Phase 8: Orchestrator — PLAN.md

## Goal
Create the master skill file and daily trigger command that ties all 14 agents together.

## Task List

### Wave 1

- [ ] Create `social-posting.skill.md` — master orchestrator with wave sequencing, error handling, retry logic
- [ ] Create `commands/social-post-daily.md` — trigger that loads the skill and runs the pipeline

## Verification

- [ ] Skill sequences all 9 waves properly
- [ ] Parallel spawns for Wave 1, 2, 4 agents
- [ ] Sequential flow between waves
- [ ] Retry loop for freshness verifier (max 3)
- [ ] Fallback trigger for evergreen-fallback
- [ ] Error handling for missing prerequisites
- [ ] Command correctly loads the skill
