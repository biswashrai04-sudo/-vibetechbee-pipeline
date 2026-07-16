# /social-approve

Approve a generated content batch and log it to the calendar.

## Usage

```
/social-approve {date}
```

Example: `/social-approve 2026-07-16`

## Process

### 1. Parse Date

Extract date from the argument (YYYY-MM-DD format). If no date provided, error:
```
Usage: /social-approve {date}
Example: /social-approve 2026-07-16
```

### 2. Find Content Folder

Glob for `social-posts/{date}-*/06-CHECKLIST.md`. If multiple folders exist for the same date (unlikely), list them and ask which to approve.

If no folder found: error "No content found for {date}. Run /social-post daily first."

### 3. Read CHECKLIST.md

Display a summary to the user:
```
Approving content for {date}:

Topic: {topic}
Niche: {niche}

Posts:
  1. Instagram — {1-line preview}
  2. LinkedIn — {1-line preview}
  3. X/Twitter — {1-line preview}
  4. Facebook — {1-line preview}

Publish in order: LI → X → IG → FB
```

### 4. Confirm Approval

Use `question` tool:
```
question([
  {
    header: "Approve",
    question: "Approve this content batch? This logs it to CONTENT_CALENDAR.md.",
    options: [
      { label: "Approve all 4 posts", description: "Mark as approved in calendar" },
      { label: "Review individually", description: "I want to check each post first" },
      { label: "Cancel", description: "Don't approve yet" }
    ]
  }
])
```

**If "Review individually":**
```
question([
  {
    header: "Select",
    question: "Which platforms to approve?",
    multiSelect: true,
    options: [
      { label: "Instagram", description: "{1-line preview}" },
      { label: "LinkedIn", description: "{1-line preview}" },
      { label: "X/Twitter", description: "{1-line preview}" },
      { label: "Facebook", description: "{1-line preview}" }
    ]
  }
])
```

### 5. Update Calendar

Read `brain/CONTENT_CALENDAR.md` and update the row for this date:

Change status columns from `⏳` to `✅` for approved platforms:

```markdown
| {date} | {topic} | {niche} | {day} | ✅ | ✅ | ✅ | ✅ | {today} |
```

(The row was created by the packager with `⏳` status)

### 6. Confirmation

```
✓ Approved: {N} posts logged to CONTENT_CALENDAR.md

Publish in this order:
  1. LinkedIn — 8:30 AM
  2. X/Twitter — 9:00 AM
  3. Instagram — 11:00 AM
  4. Facebook — 7:00 PM

Posts are in: social-posts/{date}-{topic}/
```

## Error Handling

- No date argument: show usage
- Invalid date format: "Invalid date format. Use YYYY-MM-DD."
- Date in the future: "Cannot approve future content. Use today's date or a past date."
- Folder not found: "No content found for {date}."
- Calendar entry not found: "Calendar entry missing for {date}. Was the packager run?"
