<div align="center">

<img src="https://raw.githubusercontent.com/biswashrai04-sudo/vibetechbee-pipeline/main/.github/bee-logo.png" width="80" style="display:none" onerror="this.style.display='none'"/>

# 🐝 VibeTechBee

**14-Agent Social Media Content Pipeline**

*Research. Strategize. Write. Deliver. Daily.*

[View Architecture](architecture.html) · [opencode](https://opencode.ai)

</div>

---

## What is VibeTechBee?

A daily multi-agent content creation pipeline that generates ready-to-post social media content across **4 platforms** — Instagram, LinkedIn, X, and Facebook. 14 specialized AI agents work across 9 sequential waves to scan trends, research topics, craft strategy, write platform-optimized copy, engineer optimized prompts, generate images, and package everything into a ready-to-review checklist.

Everything runs on **opencode** as the AI runtime. Nothing auto-posts — you always have the final say.

---

## Agents & Waves

| Wave | Phase | Agents | Parallel |
|------|-------|--------|----------|
| 0 | Brand Setup | Brand Strategist | — |
| 1 | Trend Discovery | Trend Scanner, Topic Selector | ✓ |
| 2 | Verification & Research | Freshness Verifier, Evergreen Fallback, Researcher | ✓ |
| 3 | Strategy | Matrix strategist → Tactical strategist | Sequential |
| 4 | Content Writing | IG Writer, LI Writer, X Writer, FB Writer | ✓ (4x) |
| 4.5 | Prompt Engineering | Flux Prompt Optimizer | — |
| 5 | Image Generation | Flux Visual Creator | — |
| 6 | Package & Deliver | Delivery Manager | — |
| 7 | Human Approval | *You* | — |

---

## Platforms & Engagement Signals

Each writer is tuned to its platform's #1 algorithmic signal:

| Platform | #1 Signal | Tone | Format |
|----------|-----------|------|--------|
| 📸 Instagram | DM Shares | Energetic, visual-first | Carousel caption + hashtags |
| 💼 LinkedIn | Dwell Time | Authoritative, data-backed | Long-form thought leadership |
| 🐦 X/Twitter | Replies | Punchy, opinionated | Tweet or thread (≤280 chars) |
| 👥 Facebook | Meaningful Interactions | Friendly, community-driven | Discussion post |

---

## Weekly Niche Rotation

| Day | Niche | Content Pillar |
|-----|-------|---------------|
| Mon | Tech | News (30%) |
| Tue | AI for Productivity | Educational (40%) |
| Wed | Apps | Educational (40%) |
| Thu | Business | Educational (40%) |
| Fri | Gadgets / Mobile | Entertainment (20%) |
| Sat | Real Estate | Educational (40%) |
| Sun | Wildcard (Best of Week) | Entertainment (20%) |

---

## What You Get Each Day

```
D:/content/2026-07-16-ai-productivity-tools/
├── 01-TREND.md           Raw scan results from 5+ sources
├── 02-RESEARCH.md        Deep research + competitor analysis
├── 03-STRATEGY.md        Core message + platform angles
├── 04-CONTENT/
│   ├── instagram.md      Caption + hashtags + alt text
│   ├── linkedin.md        Thought leadership post
│   ├── x.md              Tweet/thread (char audited)
│   └── facebook.md        Community post (trigger-free)
├── 05-IMAGES/
│   ├── prompts-engineered.md  Engineered Flux prompts (by prompt-engineer)
│   ├── prompts.md         Flux image prompts (generation log)
│   └── *.png              Platform-sized images
└── 06-CHECKLIST.md        Previews + optimal posting order
```

---

## Stack

- **Runtime**: [opencode](https://opencode.ai)
- **Orchestration**: `task()` subagent spawning (14 agents)
- **Trend Intelligence**: `webfetch` — X, Reddit, Google Trends, Product Hunt, TechCrunch, Google News
- **Image Generation**: flux.2-max → gemini-3.1-flash-lite-image → gpt-5-image-mini → IMAGE_PROMPTS.md (OpenRouter)
- **Brand**: VibeTechBee — Navy `#2F4156` · Teal `#567C8D` · Sky Blue `#C8D9E6` · Beige `#F5EFEB`

---

## Quickstart

```bash
# 1. Symlink commands for global access
ln -s commands/* ~/.config/opencode/command/

# 2. Run in opencode
/social-post daily

# 3. Review & publish
open D:/content/YYYY-MM-DD-topic/06-CHECKLIST.md
```

---

<div align="center">

**Built for opencode · 14 agents · 9 waves · 4 platforms · max engagement**

</div>


