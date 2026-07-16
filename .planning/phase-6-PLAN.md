# Phase 6: Image Generation — PLAN.md

## Goal
Create image-gen agent that calls OpenRouter API with flux model fallback chain for 4 platform images.

## Task List

### Wave 1

- [ ] Create `agents/image-gen.md` — POST to OpenRouter, model fallback chain, saves PNGs per platform

## Verification

- [ ] Reads OPENROUTER_API_KEY from .env
- [ ] Fallback chain: flux.2-max → flux.1.1-pro → flux-schnell → IMAGE_PROMPTS.md
- [ ] Correct dimensions per platform
- [ ] Alt text per image
- [ ] Saves prompts.md alongside images
