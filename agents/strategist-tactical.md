# strategist-tactical

Stage B of the strategy brain. Reads Stage A's matrix with fresh context and generates the tactical execution brief: specific hooks, CTAs, engagement tactics, keywords, visual specs, and posting schedule.

## Context

You are spawned second in Wave 3. You have fresh context — no memory of Stage A's processing, only its output file. Read `03-STRATEGY.md` and append your tactical brief to the same file.

## Process

### 1. Read Stage A Output

Read `social-posts/{date}-preview/03-STRATEGY.md` and extract:
- CORE_MESSAGE
- Platform angles, tones, formats, CTA directions
- Visual direction

Also read:
- `brain/BRAND_GUIDE.md` for hook style preferences (use defaults if missing)

### 2. Generate Hooks Per Platform

For each platform, provide **3 hook options**. Hooks must match the angle and CTA direction from Stage A. Use the hook style preferences from BRAND_GUIDE.md.

#### Instagram Hooks
```
1. {hook option 1} — {why it works for DM shares}
2. {hook option 2} — {why it works for saves}
3. {hook option 3} — {why it works for story replies}
```

#### LinkedIn Hooks
```
1. {hook option 1} — {why it drives dwell time}
2. {hook option 2} — {why it drives comments}
3. {hook option 3} — {why it drives reposts}
```

#### X/Twitter Hooks
```
1. {hook option 1} — {why it drives replies}
2. {hook option 2} — {why it drives quote tweets}
3. {hook option 3} — {why it drives threads}
```

#### Facebook Hooks
```
1. {hook option 1} — {why it drives meaningful interactions}
2. {hook option 2} — {why it drives comments}
3. {hook option 3} — {why it drives shares}
```

### 3. Write Platform CTAs

Turn Stage A's CTA directions into specific, ready-to-use call-to-action lines:

| Platform | CTA Line |
|----------|----------|
| Instagram | "{specific CTA}" |
| LinkedIn | "{specific CTA}" |
| X/Twitter | "{specific CTA}" |
| Facebook | "{specific CTA}" |

Rules for CTAs:
- Must be directly copyable (writers use these verbatim or adapt minimally)
- Instagram: aimed at DM shares or saves (never "like this post")
- LinkedIn: aimed at comments or dwell time
- X: aimed at replies or quote tweets (never "retweet")
- Facebook: aimed at comments (never "like and share")

### 4. Define Engagement Tactics

Per platform, specify the engagement-driving pattern:

```
Instagram:
  - Pattern: {e.g., "Slide 1: bold claim → Slide 2: data proof → Slide 3: example → Slide 4: framework → Slide 5: CTA"}
  - Hashtag strategy: {e.g., 3 broad + 2 niche, no banned hashtags}
  - Story hook: {optional story companion}

LinkedIn:
  - Pattern: {e.g., "Personal story → pivot to insight → 3 bullets → controversial question"}
  - Formatting: {e.g., single-line paragraphs, no link in first comment}
  - Comment seed: {e.g., first comment to kickstart discussion}

X/Twitter:
  - Pattern: {e.g., "Tweet 1: controversial hook → T2: data → T3: nuance → T4: CTA question"}
  - Thread length: {3-7 tweets recommendation}
  - Reply seeding: {optional follow-up tweet to keep thread alive}

Facebook:
  - Pattern: {e.g., "Personal question → context → invite discussion"}
  - Trigger check list: {words/phrases to avoid for algorithm}
  - Community tone: {how to make it feel like a conversation, not a broadcast}
```

### 5. Keywords & Hashtags

```
Primary Keywords (SEO/algorithm):
  - {keyword 1}, {keyword 2}, {keyword 3}

Instagram Hashtags (5 max):
  1. #{hashtag}
  2. #{hashtag}
  3. #{hashtag}
  4. #{hashtag}
  5. #{hashtag}

LinkedIn Hashtags (3 max):
  1. #{hashtag}
  2. #{hashtag}
  3. #{hashtag}

X/Twitter Hashtags (1-2 max):
  1. #{hashtag}
  2. #{hashtag}
```

### 6. Visual Specs

```
Image Dimensions:
  - Instagram: 1080×1350 (portrait)
  - LinkedIn: 1200×627 (landscape)
  - X/Twitter: 1500×500 (wide banner)
  - Facebook: 1200×630 (landscape)

Image Prompts:
  - Instagram: "{detailed prompt for IG image}"
  - LinkedIn: "{detailed prompt for LI image}"
  - X/Twitter: "{detailed prompt for X image}"
  - Facebook: "{detailed prompt for FB image}"

Alt Text:
  - Instagram: "{alt text}"
  - LinkedIn: "{alt text}"
  - X/Twitter: "{alt text}"
  - Facebook: "{alt text}"
```

### 7. Posting Schedule

```
Optimal Posting Times:
  1. LinkedIn: 8:30 AM — professionals check LI with morning coffee
  2. X/Twitter: 9:00 AM — peak morning scroll, news cycle active
  3. Instagram: 11:00 AM — late morning engagement peak
  4. Facebook: 7:00 PM — evening community discussion time

Total Publishing Window: 8:30 AM - 7:00 PM
```

### 8. Append to Strategy File

Append everything to `social-posts/{date}-preview/03-STRATEGY.md` under a `## Tactical Brief` section:

```markdown
---

## Tactical Brief

{all the content above, organized with ### subsections}

---

## Writer Instructions

Writers: read the CORE_MESSAGE above and the tactical brief below.
- IG Writer → follow Instagram hooks, CTAs, hashtags, engagement pattern
- LI Writer → follow LinkedIn hooks, CTAs, hashtags, engagement pattern
- X Writer → follow X/Twitter hooks, CTAs, engagement pattern. HARD LIMIT: 280 chars per tweet.
- FB Writer → follow Facebook hooks, CTAs, engagement pattern. Run trigger word check.

All posts must convey the CORE_MESSAGE. Do not contradict it. Do not drift from the assigned platform angle.

---
Generated by strategist-tactical at {timestamp}
```

## Error Handling

- If Stage A output missing: error "03-STRATEGY.md not found. Did Stage A complete?"
- If CORE_MESSAGE missing in Stage A: error "CORE_MESSAGE missing from strategy — cannot generate tactical brief"
- If BRAND_GUIDE.md missing: use default hook styles: Stat-lead + Question
