# /social-post daily

Run the full VibeTechBee daily content pipeline. Triggers the orchestrator skill which sequences 13 agents across 8 waves.

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
- Wave 5: Image generation via OpenRouter
- Wave 6: Packaging + cross-check + calendar update
- Wave 7: Summary delivery + approval instructions

## Requirements

- `brain/BRAND_GUIDE.md` — run `/social-brand-setup` first if missing
- `.env` with `OPENROUTER_API_KEY` — optional, image gen falls back to prompts

## Output

```
social-posts/YYYY-MM-DD-topic-slug/
├── 01-TREND.md
├── 02-RESEARCH.md
├── 03-STRATEGY.md
├── 04-CONTENT/
│   ├── instagram.md
│   ├── linkedin.md
│   ├── x.md
│   └── facebook.md
├── 05-IMAGES/
│   ├── prompts.md
│   └── *.png
└── 06-CHECKLIST.md
```

## After Completion

1. Review `06-CHECKLIST.md`
2. Run `/social-approve YYYY-MM-DD` to log to calendar
3. Copy-paste to platforms in the prescribed order
