# /social-post daily

Run the full VibeTechBee daily content pipeline. Triggers the orchestrator skill which sequences 14 agents across 9 waves.

## Execution

Load the skill:
```
skill: social-posting
```

The skill handles:
- Today's date + niche detection
- Wave 1: Trend scanning + topic selection
- Wave 2: Freshness verification + research (with retry loop + evergreen fallback)
- Wave 3: Two-stage strategy (matrix → tactical)
- Wave 4: 4 parallel platform writers
- Wave 4.5: Prompt engineering for Flux-optimized image prompts
- Wave 5: Image generation via OpenRouter
- Wave 6: Packaging + cross-check + calendar update
- Wave 7: Summary delivery + approval instructions

## Requirements

- `brain/BRAND_GUIDE.md` — run `/social-brand-setup` first if missing
- `.env` with `OPENROUTER_API_KEY` — optional, image gen falls back to prompts

## Output

```
D:/content/YYYY-MM-DD-topic-slug/
├── 01-TREND.md
├── 02-RESEARCH.md
├── 03-STRATEGY.md
├── 04-CONTENT/
│   ├── instagram.md
│   ├── linkedin.md
│   ├── x.md
│   └── facebook.md
├── 05-IMAGES/
│   ├── prompts-engineered.md  Engineered Flux prompts (by prompt-engineer)
│   ├── prompts.md         Flux image prompts (generation log)
│   └── *.png
└── 06-CHECKLIST.md
```

## After Completion

1. Review `06-CHECKLIST.md`
2. Run `/social-approve YYYY-MM-DD` to log to calendar
3. Copy-paste to platforms in the prescribed order
