# VibeTechBee — Multi-Agent Content Pipeline

A daily multi-agent content creation pipeline for social media (Instagram, LinkedIn, X, Facebook) built on **opencode** as the AI runtime. 11 specialized agents orchestrated across 7 waves to research, strategize, write, and deliver platform-optimized posts branded as **VibeTechBee**.

## Architecture

```
opencode (AI Runtime)
  │  task() — spawn subagents
  ├─ Wave 1: Trend Discovery  (scanner + selector)
  ├─ Wave 2: Verification     (verifier → fallback → researcher)
  ├─ Wave 3: Strategy         (matrix → tactical)
  ├─ Wave 4: Content Writing  (4 parallel writers)
  ├─ Wave 5: Image Generation (Flux via OpenRouter)
  ├─ Wave 6: Package & Deliver (checklist → calendar)
  └─ Wave 7: Human Approval Gate
       └─ ./social-posts/YYYY-MM-DD-topic/
```

## Project Structure

```
vibetechbee-pipeline/
├── social-posting.skill.md       ← orchestrator
├── commands/                     ← /social-post daily & friends
├── agents/                       ← 11 agent definitions
├── brain/BRAND_GUIDE.md          ← brand identity
├── social-posts/                 ← daily output
├── architecture.html             ← this page
└── blueprint.html                ← visual pipeline blueprint
```

## Usage

1. Symlink `commands/` to `~/.config/opencode/command/`
2. Run `/social-post daily` in opencode
3. Review `06-CHECKLIST.md`
4. Copy-paste to platforms

## Stack

- **Runtime**: opencode
- **Orchestration**: task() subagent spawning
- **Trends**: webfetch (X, Reddit, Google Trends, Product Hunt, TechCrunch)
- **Images**: Flux 1.1 Pro via OpenRouter
- **Brand**: VibeTechBee — Navy Blue · Champagne Gold · Dark Mode

---

Built for opencode · 11 agents · 7 waves · 4 platforms · max engagement
