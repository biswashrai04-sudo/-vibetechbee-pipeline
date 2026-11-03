<div align="center">

<a href="https://github.com/biswashrai04-sudo/-vibetechbee-pipeline">
  <img src="https://raw.githubusercontent.com/biswashrai04-sudo/-vibetechbee-pipeline/main/.github/bee-logo.png" alt="VibeTechBee Logo" width="100" height="100" style="max-width:100%;">
</a>

# VibeTechBee

**14-Agent Daily Social Media Content Pipeline**

*Research → Strategize → Write → Generate Images → Package for Review — All in One Flow*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Built with opencode](https://img.shields.io/badge/Built%20with-opencode-6C5CE7.svg)](https://opencode.ai)
[![Agents: 14](https://img.shields.io/badge/Agents-14-FF6B6B.svg)](https://github.com/biswashrai04-sudo/-vibetechbee-pipeline/tree/main/agents)
[![Platforms: 4](https://img.shields.io/badge/Platforms-4-4ECDC4.svg)](https://github.com/biswashrai04-sudo/-vibetechbee-pipeline)
[![Waves: 9](https://img.shields.io/badge/Waves-9-45B7D1.svg)](https://github.com/biswashrai04-sudo/-vibetechbee-pipeline)
[![No Auto-Posting](https://img.shields.io/badge/Auto--Posting-None-95A5A6.svg)](https://github.com/biswashrai04-sudo/-vibetechbee-pipeline)

[Architecture](architecture.html) • [Agent Specs](agents/) • [Commands](commands/) • [Skill Definition](social-posting.skill.md) • [opencode](https://opencode.ai)

</div>

---

## What is VibeTechBee?

**VibeTechBee** is a production-ready, multi-agent content creation pipeline that generates **ready-to-review social media content daily** across **4 platforms** — Instagram, LinkedIn, X (Twitter), and Facebook.

**14 specialized AI agents** collaborate across **9 sequential waves** to:
1. **Scan** trends from 5+ sources (X, Reddit, Google Trends, Product Hunt, TechCrunch, Google News)
2. **Verify** freshness & relevance with fallback to evergreen content
3. **Research** deep-dive with competitor analysis
4. **Strategize** core messaging & platform-specific angles
5. **Write** platform-optimized copy (tuned to each algorithm's #1 signal)
6. **Engineer** optimized Flux prompts for visuals
7. **Generate** platform-sized images via multiple model fallbacks
8. **Package** everything into a human-review checklist

> **Key Principle:** Zero auto-posting. You always have final approval.

---

## Agent Architecture (14 Agents, 9 Waves)

| Wave | Phase | Agents | Execution |
|------|-------|--------|-----------|
| **0** | Brand Setup | `Brand Strategist` | Sequential |
| **1** | Trend Discovery | `Trend Scanner`, `Topic Selector` | **Parallel** |
| **2** | Verification & Research | `Freshness Verifier`, `Evergreen Fallback`, `Researcher` | **Parallel** |
| **3** | Strategy | `Matrix Strategist` → `Tactical Strategist` | Sequential |
| **4** | Content Writing | `IG Writer`, `LI Writer`, `X Writer`, `FB Writer` | **Parallel (4×)** |
| **4.5** | Prompt Engineering | `Flux Prompt Optimizer` | Sequential |
| **5** | Image Generation | `Flux Visual Creator` | Sequential |
| **6** | Package & Deliver | `Delivery Manager` | Sequential |
| **7** | Human Approval | **You** | Manual |

<details>
<summary><strong>View all 14 agent specifications</strong></summary>

| Agent | Role | Key Capability |
|-------|------|----------------|
| `brand-strategist.md` | Defines brand voice, pillars, visual identity | Brand DNA extraction |
| `trend-scanner.md` | Scans 5+ sources for trending topics | Multi-source aggregation |
| `topic-selector.md` | Picks best topic per niche rotation | Scoring & filtering |
| `freshness-verifier.md` | Validates topic recency & relevance | Anti-stale guard |
| `evergreen-fallback.md` | Provides backup evergreen topics | Zero-downtime guarantee |
| `researcher.md` | Deep research + competitor analysis | Evidence-backed insights |
| `strategist-matrix.md` | Core message + platform angle matrix | Strategic coherence |
| `strategist-tactical.md` | Tactical execution plan per platform | Actionable directives |
| `instagram-writer.md` | Carousel captions + hashtags + alt text | DM-share optimization |
| `linkedin-writer.md` | Long-form thought leadership | Dwell-time optimization |
| `x-writer.md` | Tweets/threads ≤280 chars | Reply-rate optimization |
| `facebook-writer.md` | Community discussion posts | Meaningful-interaction optimization |
| `prompt-engineer.md` | Engineers Flux prompts from copy | Visual-copy alignment |
| `image-gen.md` | Generates images via Flux fallbacks | Multi-model resilience |
| `packager.md` | Assembles final review checklist | Human-in-the-loop UX |

</details>

---

## Platform Strategy: Tuned to Algorithmic Signals

| Platform | #1 Algorithmic Signal | Tone & Style | Output Format |
|----------|----------------------|--------------|---------------|
| 📸 **Instagram** | **DM Shares** | Energetic, visual-first, story-driven | Carousel caption + 15–20 hashtags + alt text |
| 💼 **LinkedIn** | **Dwell Time** | Authoritative, data-backed, professional | Long-form (1300+ chars) with line breaks |
| 🐦 **X / Twitter** | **Replies** | Punchy, opinionated, hook-first | Single tweet or 3–5 tweet thread |
| 👥 **Facebook** | **Meaningful Interactions** | Friendly, community-driven, question-led | Discussion post (trigger-word safe) |

---

## Weekly Niche Rotation (7-Day Cycle)

| Day | Niche | Content Pillar | Educational % | Entertainment % | News % |
|-----|-------|----------------|---------------|-----------------|--------|
| **Mon** | Tech | News-heavy | 30% | 20% | **50%** |
| **Tue** | AI for Productivity | Educational | **40%** | 30% | 30% |
| **Wed** | Apps | Educational | **40%** | 30% | 30% |
| **Thu** | Business | Educational | **40%** | 30% | 30% |
| **Fri** | Gadgets / Mobile | Entertainment | 30% | **50%** | 20% |
| **Sat** | Real Estate | Educational | **40%** | 30% | 30% |
| **Sun** | Wildcard (Best of Week) | Entertainment | 20% | **60%** | 20% |

---

## Daily Output Structure

Each run produces a dated folder with complete audit trail:

```text
content/2026-07-16-ai-productivity-tools/
├── 01-TREND.md              # Raw scan results from 5+ sources
├── 02-RESEARCH.md           # Deep research + competitor analysis
├── 03-STRATEGY.md           # Core message + platform angle matrix
├── 04-CONTENT/
│   ├── instagram.md         # Caption + hashtags + alt text
│   ├── linkedin.md          # Thought leadership post
│   ├── x.md                 # Tweet/thread (character-audited)
│   └── facebook.md          # Community post (trigger-free)
├── 05-IMAGES/
│   ├── prompts-engineered.md  # Engineered Flux prompts (by prompt-engineer)
│   ├── prompts.md           # Generation log with model used
│   └── *.png                # Platform-sized images (1080×1080, 1200×628, etc.)
└── 06-CHECKLIST.md          # Previews + optimal posting order + approval
```

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| **AI Runtime** | [opencode](https://opencode.ai) — local-first, subagent orchestration |
| **Orchestration** | `task()` subagent spawning (14 parallel/sequential agents) |
| **Trend Intelligence** | `webfetch` — X, Reddit, Google Trends, Product Hunt, TechCrunch, Google News |
| **Image Generation** | **Flux.2-max** → `gemini-3.1-flash-lite-image` → `gpt-5-image-mini` (fallback chain) |
| **Image Provider** | [OpenRouter](https://openrouter.ai) unified API |
| **Brand Colors** | Navy `#2F4156` • Teal `#567C8D` • Sky Blue `#C8D9E6` • Beige `#F5EFEB` |
| **Documentation** | Markdown + interactive `architecture.html` |
| **Skills/Commands** | opencode-native `.skill.md` + `.md` command files |

---

## Quickstart

### Prerequisites
- [opencode](https://opencode.ai) installed (`npm i -g opencode` or download binary)
- [OpenRouter API key](https://openrouter.ai/keys) for image generation
- Git + Bash/Zsh

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/biswashrai04-sudo/-vibetechbee-pipeline.git
cd -vibetechbee-pipeline

# 2. Configure environment
cp .env.example .env
# Edit .env and add your OPENROUTER_API_KEY

# 3. Install opencode commands globally (one-time)
ln -sf "$PWD/commands"/* ~/.config/opencode/command/

# 4. Initialize brand (first run only)
# This creates .brain/brand-profile.json with your voice & pillars
/social-brand-setup

# 5. Run daily pipeline
/social-post daily
```

### Daily Workflow

```bash
# Generate today's content package
/social-post daily

# Review the checklist
cat content/$(date +%F)-*/06-CHECKLIST.md

# Approve & publish manually (copy-paste to platforms)
/social-approve
```

---

## Repository Structure

```text
-vibetechbee-pipeline/
├── .github/                 # GitHub configs (workflows, dependabot)
├── agents/                  # 14 agent specifications (Markdown)
├── brain/                   # Runtime state (brand-profile.json, niche-rotation.json)
├── commands/                # opencode slash commands (social-post-daily, etc.)
├── .planning/               # Local planning artifacts (gitignored)
├── architecture.html        # Interactive architecture visualization
├── social-posting.skill.md  # opencode skill definition
├── .env.example             # Environment template
├── .gitignore               # Comprehensive ignore rules
├── LICENSE                  # MIT License
└── README.md                # This file
```

---

## Configuration

### Environment Variables (`.env`)

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENROUTER_API_KEY` | **Yes** | OpenRouter key for Flux image generation |

### Brand Profile (`.brain/brand-profile.json`)

Created on first run via `/social-brand-setup`. Contains:
- Brand name, tagline, mission
- Voice attributes (tone, vocabulary, emoji usage)
- Content pillars & niche weights
- Visual identity (colors, fonts, logo usage)
- Platform-specific guidelines

### Niche Rotation (`.brain/niche-rotation.json`)

Configurable 7-day niche schedule with pillar weights.

---

## Extending the Pipeline

### Add a New Agent
1. Create `agents/your-agent.md` following the [agent template](agents/brand-strategist.md)
2. Register in `social-posting.skill.md` under `agents:`
3. Add to wave execution order in `commands/social-post-daily.md`

### Add a New Platform
1. Create writer agent: `agents/yourplatform-writer.md`
2. Add image specs to `agents/image-gen.md`
3. Update packager: `agents/packager.md`
4. Add command integration in `commands/`

### Customize Niche Rotation
Edit `.brain/niche-rotation.json` (created after brand setup) or modify the source in `commands/social-brand-setup.md`.

---

## CI / Quality Gates

| Check | Tool | Trigger |
|-------|------|---------|
| Markdown lint | `markdownlint-cli2` | PR / Push |
| Link validation | `markdown-link-check` | PR / Push / Weekly |
| Spell check | `cspell` | PR / Push |
| Shellcheck | `shellcheck` | PR / Push (for `.sh` files) |
| YAML lint | `yamllint` | PR / Push (for `.yml` files) |

Run locally:
```bash
npm i -g markdownlint-cli2 markdown-link-check cspell
markdownlint-cli2 "**/*.md"
markdown-link-check README.md
cspell "**/*.md"
```

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/amazing-feature`
3. Run lint checks locally (see [CI](#ci--quality-gates))
4. Commit with conventional commits: `feat: add amazing feature`
5. Push and open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## Security

- **No auto-posting** — human approval required for every piece
- **Secrets in `.env`** — never committed (enforced by `.gitignore`)
- **OpenRouter key** — scoped to image generation only
- **Dependabot** — enabled for GitHub Actions & npm (if added)

Report vulnerabilities via [GitHub Security Advisories](https://github.com/biswashrai04-sudo/-vibetechbee-pipeline/security/advisories).

---

## License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.

---

## Acknowledgments

- [opencode](https://opencode.ai) — the AI runtime that makes this possible
- [OpenRouter](https://openrouter.ai) — unified model access
- [Flux](https://github.com/black-forest-labs/flux) — state-of-the-art image generation
- All open-source models powering the agent intelligence

---

<div align="center">

**Built with ❤️ for opencode · 14 agents · 9 waves · 4 platforms · Zero auto-posting**

[⬆ Back to top](#vibetechbee)

</div>