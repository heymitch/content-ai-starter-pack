---
name: content-ai-setup
description: Set up your Content AI system in under 5 minutes. Defines your niche, content pillars, and generates a starter content calendar. Say "set up my content system", "content setup", or "get started with content".
user_invocable: true
---

# Content AI Setup

One-time setup. Gets your content system running in under 5 minutes. After this, every content skill knows who you are, what you write about, and where you're headed.

## Step 1: Quick Intake

Ask the user these 3 questions (one at a time, not all at once):

1. **"What's your niche?"** — Not just a topic. Who do you serve, and with what expertise? Push for specificity. "Marketing" is too broad. "Helping B2B founders build personal brands on LinkedIn" is right.

2. **"How often do you want to post?"** — Options: daily, 3x/week, weekdays only. If they're not sure, recommend 3x/week as a starting cadence.

3. **"What does success look like in 90 days?"** — More followers? More inbound leads? Build authority in a new space? This shapes the content mix.

## Step 2: Define Content Pillars

Based on their answers, propose 3-5 content pillars.

Each pillar must be:
- Broad enough to write about for months
- Focused enough that their audience immediately sees relevance
- Aligned with their expertise

Present them as a numbered list with a one-line description each. Ask: "Do these feel right, or should we swap any out?"

Wait for confirmation before proceeding.

## Step 3: Generate Starter Calendar

Build a 2-week content calendar using their pillars and cadence.

For each post:
```
Day [X] — [Date]
Topic: [Specific topic, not a vague category]
Format: [Steps / Stats / Lessons / Story / Hot Take / List]
Hook: [One hook option — 9 words or fewer]
Pillar: [Which pillar this serves]
```

Rotation rules:
- Don't repeat the same format two days in a row
- Mix post types: 40% actionable advice, 30% personal story/lessons, 30% trends/futurism
- Alternate pillars so no single pillar dominates

## Step 4: Save Everything

Create the following files:

**`.coworker/content/profile.md`**:
```markdown
# Content Profile

Niche: [their niche]
Cadence: [posting frequency]
90-Day Goal: [their goal]

## Content Pillars

1. **[Pillar 1]** — [description]
2. **[Pillar 2]** — [description]
3. **[Pillar 3]** — [description]
[4-5 if defined]

Generated: [YYYY-MM-DD]
```

**`.coworker/content/calendar.md`**:
```markdown
# Content Calendar — [Date Range]

Generated: [YYYY-MM-DD]
Pillars: [list]
Cadence: [X posts/week]

---

[Calendar entries from Step 3]
```

Update **`.coworker/index.md`** — add a Content section:
```markdown
## Content
- Profile: `.coworker/content/profile.md`
- Calendar: `.coworker/content/calendar.md`
- Pillars: [list them]
- Cadence: [frequency]
```

If `.coworker/index.md` doesn't exist, create it with a header and the Content section.

## Step 5: Next Steps

Print:

```
Your content system is set up.

Here's what to do next:

1. Write your first post: "Write a LinkedIn post about [first calendar topic]"
2. Hunt patterns in your niche: "Hunt patterns in [their niche]"
3. Optimize your LinkedIn profile: "Optimize my LinkedIn profile"

Your calendar is at .coworker/content/calendar.md
Your profile is at .coworker/content/profile.md

Every content skill now reads your pillars and niche automatically.
```

## Rules

- Keep the intake fast. 3 questions, not 10.
- Propose pillars — don't make them build from scratch.
- Every calendar topic must be specific enough to write about immediately.
- Hook suggestions must be actual hooks (9 words or fewer), not descriptions.
- Save everything before presenting next steps.
- If `.coworker/` doesn't exist, create it.
