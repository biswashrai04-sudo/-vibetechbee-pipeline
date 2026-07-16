# Phase 6: Image Generation — PLAN.md

## Goal
Create image-gen agent that calls OpenRouter API with Gemini image model fallback chain for 4 platform images.

## Task List

### Wave 1

- [ ] Create `agents/image-gen.md` — POST to OpenRouter, model fallback chain, saves PNGs per platform

## Verification

- [ ] Reads OPENROUTER_API_KEY from .env
- [ ] Fallback chain: gemini-2.5-flash-image → gemini-3.1-flash-lite → gemini-3.1-flash → IMAGE_PROMPTS.md
- [ ] Correct dimensions per platform
- [ ] Alt text per image
- [ ] Saves prompts.md alongside images
