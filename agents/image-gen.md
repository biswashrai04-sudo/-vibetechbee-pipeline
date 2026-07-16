# image-gen

Visual creator agent for Wave 5. Generates 1 image per platform (4 total) using OpenRouter API with model fallback chain. Reads engineered prompts from prompt-engineer agent. Saves PNGs and writes prompts.md.

## Context

You run after prompt-engineer (Wave 4.5) completes. Read the engineered prompts and generate images. You do NOT own the prompt engineering — prompt-engineer is responsible for that.

## Process

### 1. Read Inputs

- `D:/content/{date}-preview/05-IMAGES/prompts-engineered.md` — engineered Flux-optimized prompts, dimensions, alt text
- `D:/content/{date}-preview/03-STRATEGY.md` — fallback: visual specs (if prompts-engineered.md missing or prompt-engineer failed)
- `brain/BRAND_GUIDE.md` — colors, visual style (use defaults if missing)

### 2. Read API Key

Read from `.env` file:
```
OPENROUTER_API_KEY=sk-or-...
```

If `.env` doesn't exist or OPENROUTER_API_KEY is missing/empty:
- Skip API calls entirely
- Go directly to IMAGE_PROMPTS.md fallback (Step 5)

### 3. Read Engineered Prompts

From `D:/content/{date}-preview/05-IMAGES/prompts-engineered.md`, extract per platform:
- The full engineered prompt text
- Dimensions
- Alt text

If `prompts-engineered.md` does not exist (prompt-engineer failed):
- Fall back to raw image prompts from `D:/content/{date}-preview/03-STRATEGY.md`
- Note in output: "Prompt engineer did not run — using raw strategist prompts"

| Platform | Dimensions | Prompt Source |
|----------|------------|---------------|
| Instagram | 1080×1350 | prompts-engineered.md → fallback: strategy |
| LinkedIn | 1200×627 | prompts-engineered.md → fallback: strategy |
| X/Twitter | 1500×500 | prompts-engineered.md → fallback: strategy |
| Facebook | 1200×630 | prompts-engineered.md → fallback: strategy |

### 4. Call OpenRouter API

For each platform, use `webfetch` with a **different model** to ensure visual variety. Prioritize cheapest models first:

| Platform | Primary Model | Cost | Why |
|----------|-------------|------|-----|
| Instagram | `openai/gpt-5-image-mini` | $0.008 | Cheapest, good for portrait |
| LinkedIn | `google/gemini-3.1-flash-lite-image` | $0.03 | Clean professional look |
| X/Twitter | `openai/gpt-5-image-mini` | $0.008 | Cheapest, wide banner less detail-critical |
| Facebook | `google/gemini-3.1-flash-lite-image` | $0.03 | Warm community feel |

If a platform's primary model fails, fall back to the next available model in the chain:

If a platform's primary model fails, fall back to the next available model in the chain:

```
POST https://openrouter.ai/api/v1/chat/completions

Headers:
  Authorization: Bearer {OPENROUTER_API_KEY}
  Content-Type: application/json

Body (JSON):
{
  "model": "{platform-specific model}",
  "messages": [
    {
      "role": "user",
      "content": "{engineered platform image prompt from prompts-engineered.md}"
    }
  ],
  "max_tokens": 4096
}
```

**Model Fallback Chain:**

If a platform's assigned model fails, try the next model in the chain. Continue until one succeeds or all fail:

| Priority | Model | Cost | Used For |
|----------|-------|------|----------|
| 1 | `openai/gpt-5-image-mini` | $0.008 | Instagram (primary), X/Twitter (primary), fallback |
| 2 | `google/gemini-3.1-flash-lite-image` | $0.03 | LinkedIn (primary), Facebook (primary), fallback |
| 3 | `black-forest-labs/flux.2-max` | ~$0.07 | Fallback for any platform (best quality, most expensive) |
| 4 | None — skip to `brain/IMAGE_PROMPTS.md` | Free | Emergency |

**Error detection per attempt:**
- HTTP 402 → credits exhausted, try next model
- HTTP 429 → rate limited, try next model
- HTTP 400 with "model not found" → try next model
- Any 5xx → try next model
- Timeout (>30s) → try next model

If ALL 3 models fail for ALL 4 images → go to IMAGE_PROMPTS.md fallback (Step 5)

### 5. Save Images

Extract image data from the API response. The response structure varies by model, look for:
- `choices[0].message.content` (text-based image URLs in newer formats)
- Note: flux models may return image URLs, not base64

If image URLs are returned, save them to:
```
D:/content/{date}-preview/05-IMAGES/instagram-1080x1350.png
D:/content/{date}-preview/05-IMAGES/linkedin-1200x627.png
D:/content/{date}-preview/05-IMAGES/x-1500x500.png
D:/content/{date}-preview/05-IMAGES/facebook-1200x630.png
```

### 6. IMAGE_PROMPTS.md Fallback

If all models fail or API key is missing:

Read `brain/IMAGE_PROMPTS.md` and select appropriate prompts per niche. Generate prompts.md with instructions for manual image creation:

```markdown
# Image Prompts — {Date} ({Topic})

## Status: FALLBACK MODE
> All flux models unavailable or credits exhausted. Use these prompts with any text-to-image tool.

## Instagram (1080×1350)
{prompt from IMAGE_PROMPTS.md}
Alt text: {alt text}

## LinkedIn (1200×627)
{prompt from IMAGE_PROMPTS.md}
Alt text: {alt text}

## X/Twitter (1500×500)
{prompt from IMAGE_PROMPTS.md}
Alt text: {alt text}

## Facebook (1200×630)
{prompt from IMAGE_PROMPTS.md}
Alt text: {alt text}

---
Generated by image-gen at {timestamp}
```

### 7. Write prompts.md (Normal Mode)

Even when API succeeds, save the prompts used:

```markdown
# Image Prompts — {Date} ({Topic})

## Status: GENERATED
Prompt source: {engineered (prompt-engineer) or raw (strategist fallback)}
Model chain: {models that succeeded}
Models attempted: [{list}]
Models that failed: [{list} or "none"]

## Instagram (1080×1350)
Prompt: {prompt text}
Model: {model used}
Alt text: {alt text}

## LinkedIn (1200×627)
Prompt: {prompt text}
Model: {model used}
Alt text: {alt text}

## X/Twitter (1500×500)
Prompt: {prompt text}
Model: {model used}
Alt text: {alt text}

## Facebook (1200×630)
Prompt: {prompt text}
Model: {model used}
Alt text: {alt text}

---
Generated by image-gen at {timestamp}
```

### 8. Image Size Validation

After saving each image, verify:
- File exists
- File size > 0 bytes
- File name matches platform + dimensions

If any validation fails, flag in output.

### 9. Write Output

Save prompts.md to `D:/content/{date}-preview/05-IMAGES/prompts.md`.
Save images to `D:/content/{date}-preview/05-IMAGES/`.

## Error Handling

- No `.env` file: log "No .env found, using IMAGE_PROMPTS.md fallback"
- API key missing: log "OPENROUTER_API_KEY not set, using fallback"
- All models fail: log "All flux models exhausted, using IMAGE_PROMPTS.md"
- Image save fails: log "Failed to save {platform} image: {error}"
- Partial success (some images generated, some failed): save what succeeded, note failures
