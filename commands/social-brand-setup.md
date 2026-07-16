# /social-brand-setup

Run VibeTechBee's interactive brand setup. Asks 3 questions at a time via the `question` tool, gathering brand identity for all agents to reference. Outputs `brain/BRAND_GUIDE.md`.

## Process

### Step 1: Welcome & Context

Tell the user: "Let's set up your brand identity. I'll ask a few questions — 3 at a time — to build your BRAND_GUIDE.md. Your answers will influence every post the pipeline generates."

### Step 2: Brand Voice (Batch 1)

Use `question` tool:

```
question([
  {
    header: "Tone",
    question: "What's your brand's default tone of voice?",
    options: [
      { label: "Bold & Punchy", description: "Short, opinionated, attention-grabbing" },
      { label: "Authoritative & Expert", description: "Data-backed, confident, thought leadership" },
      { label: "Friendly & Conversational", description: "Warm, approachable, community-focused" },
      { label: "Write my own", description: "Describe your tone in your own words" }
    ]
  },
  {
    header: "Personality",
    question: "If your brand were a person at a party, how would they behave?",
    options: [
      { label: "The Expert", description: "Dropping knowledge, people gather around to listen" },
      { label: "The Connector", description: "Making introductions, keeping conversations flowing" },
      { label: "The Provocateur", description: "Challenging norms, making people think" },
      { label: "Describe it myself", description: "Tell me in your own words" }
    ]
  },
  {
    header: "Language",
    question: "What language rules should the brand follow?",
    multiSelect: true,
    options: [
      { label: "No jargon", description: "Plain English, no buzzwords" },
      { label: "Use emojis", description: "Emojis are part of the brand voice" },
      { label: "Data-backed", description: "Every claim needs a stat or source" },
      { label: "Layperson-friendly", description: "Explain tech concepts simply" }
    ]
  }
])
```

If user picked any custom option, follow up with freeform question to capture their description.

### Step 3: Platform-Specific Tone (Batch 2)

Use `question` tool:

```
question([
  {
    header: "Instagram Tone",
    question: "How should the brand sound on Instagram?",
    options: [
      { label: "Energetic & Visual", description: "Short captions, high energy, emoji-heavy" },
      { label: "Curated & Aesthetic", description: "Polished, minimal, aspirational" },
      { label: "Behind-the-scenes", description: "Casual, authentic, day-in-the-life" },
      { label: "Same as default", description: "Use the default brand voice" }
    ]
  },
  {
    header: "LinkedIn Tone",
    question: "How should the brand sound on LinkedIn?",
    options: [
      { label: "Thought Leader", description: "Long-form insights, data, contrarian takes" },
      { label: "Career Coach", description: "Tips, frameworks, professional development" },
      { label: "Industry Analyst", description: "Trends, predictions, market commentary" },
      { label: "Same as default", description: "Use the default brand voice" }
    ]
  },
  {
    header: "X/Twitter Tone",
    question: "How should the brand sound on X?",
    options: [
      { label: "Hot Takes", description: "Punchy, opinionated, designed for replies" },
      { label: "Curator", description: "Curating others' work, adding one insight per share" },
      { label: "Threader", description: "Long-form educational threads" },
      { label: "Same as default", description: "Use the default brand voice" }
    ]
  }
])
```

### Step 4: Visual & Content Strategy (Batch 3)

Use `question` tool:

```
question([
  {
    header: "Visual Style",
    question: "What visual style should images follow?",
    options: [
      { label: "Minimal & Clean", description: "White space, simple graphics, navy/teal palette" },
      { label: "Bold & Graphic", description: "Strong typography, gradient backgrounds, big visuals" },
      { label: "Photo-forward", description: "High-quality photography with overlay text" },
      { label: "Illustrated", description: "Custom illustrations, icons, vector art" }
    ]
  },
  {
    header: "Pillar Mix",
    question: "Content pillar emphasis? (Educational content is the backbone)",
    options: [
      { label: "Standard Mix", description: "Educational 40%, News 30%, Entertainment 20%, Promotional 10%" },
      { label: "Education Heavy", description: "Educational 50%, News 20%, Entertainment 20%, Promotional 10%" },
      { label: "News Forward", description: "News 40%, Educational 30%, Entertainment 20%, Promotional 10%" },
      { label: "Custom ratios", description: "I'll specify my own split" }
    ]
  },
  {
    header: "Hooks Style",
    question: "What type of hooks work best for your audience?",
    multiSelect: true,
    options: [
      { label: "Contrarian", description: "'Most people think X. Here's the truth.'" },
      { label: "Stat-lead", description: "'73% of developers...'" },
      { label: "Question", description: "'What if you could...?'" },
      { label: "Rule-break", description: "'Stop doing X. Do Y instead.'" }
    ]
  }
])
```

### Step 5: Competitors & References (Batch 4)

Use `question` tool:

```
question([
  {
    header: "Competitors",
    question: "Who are your main competitors or reference accounts?",
    options: [
      { label: "I'll list them", description: "Share account names/handles" },
      { label: "None in mind", description: "Skip competitor context" }
    ]
  },
  {
    header: "Inspiration",
    question: "Any creators or brands you want to emulate?",
    options: [
      { label: "I'll share", description: "Tell me who inspires your style" },
      { label: "Skip", description: "No reference accounts" }
    ]
  },
  {
    header: "Taboo",
    question: "Topics or tones to AVOID at all costs?",
    options: [
      { label: "I'll specify", description: "List topics/tones that are off-limits" },
      { label: "Nothing specific", description: "No hard restrictions" }
    ]
  }
])
```

If any custom choices, follow up with freeform question. Keep these short.

### Step 6: Generate BRAND_GUIDE.md

After all questions answered, read `brain/BRAND_GUIDE.md` if it exists (update mode), otherwise create it fresh.

Write the file with:

```markdown
# VibeTechBee — Brand Guide

> Generated by /social-brand-setup on {today's date}

## Brand Voice

**Tone:** [tone answer]
**Personality:** [personality answer]
**Language Rules:** [language rules]

## Platform-Specific Tone

| Platform | Tone | Notes |
|----------|------|-------|
| Instagram | [IG tone] | |
| LinkedIn | [LI tone] | |
| X/Twitter | [X tone] | |
| Facebook | [FB tone — same as default unless specified] | |

## Visual Identity

**Colors:** Navy `#2F4156` · Teal `#567C8D` · Sky Blue `#C8D9E6` · Beige `#F5EFEB` · White `#FFFFFF`
**Style:** [visual style answer]
**Image Notes:** [any additional visual direction]

## Content Strategy

**Pillar Mix:** [pillar mix answer]
**Hook Style:** [hook styles]
**Weekly Niche Rotation:** Mon=Tech, Tue=AI Productivity, Wed=Apps, Thu=Business, Fri=Gadgets/Mobile, Sat=Real Estate, Sun=Wildcard

## Competitor Landscape

**Competitors:** [list or "None specified"]
**Inspiration:** [list or "None specified"]

## Guardrails

**Off-limits:** [taboo topics or "None specified"]

---

## Usage by Agents

All agents read this file for:
- **Strategist:** Core message tone, hook style selection
- **Writers:** Platform-specific voice adaptation
- **Image Gen:** Visual style and color palette
- **Fallback:** Evergreen topic generation

**Fallback behavior:** If this file is missing or incomplete, agents use built-in VibeTechBee defaults:
- Tone: Authoritative & Expert (default brand voice)
- Visual: Minimal & Clean with navy/teal palette
- Pillars: Standard Mix (40/30/20/10)
```

### Step 7: Confirm

Tell the user: "Brand guide saved to `brain/BRAND_GUIDE.md`. All 13 agents will now reference this for tone, style, and guardrails. Run `/social-brand-setup` anytime to update it."

## Error Handling

- If the user picks custom options, follow up with short freeform questions
- If BRAND_GUIDE.md already exists, update in place (preserve existing structure)
- Never lose user data on update — append changes, don't overwrite unrecognized sections
