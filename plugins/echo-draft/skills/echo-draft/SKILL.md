---
name: echo-draft
description: Generate human-quality content with automatic AI detection scoring and self-improvement loop. Full pipeline — generate, score, fix, verify. Trigger with "echo draft", "write a post", "write content", "ghost write".
user-invocable: true
---

# Echo Draft — Full Pipeline

Generate content that reads like a human wrote it, then prove it with automated scoring.

## Flow

### Step 1: Load Creative Coaching

**ALWAYS** read `skills/echo-draft/references/creative-coaching.md` before generating anything. This is non-negotiable. The rules in that file are system-level constraints on every word you produce.

### Step 2: Load Voice Template

Read `training/voice/voice-template.md` from the workspace root. This file contains the user's voice profile — their tone, cadence, and writing style. Absorb it as the authorial identity for everything you generate.

If `training/voice/voice-template.md` does not exist, tell the user:
> No voice template found. Add your writing samples to `training/voice/voice-template.md` for better results. Proceeding with creative-coaching defaults.

### Step 3: Load Context

Read `.coworker/index.md` if it exists. Extract any relevant context — recent topics, active projects, audience notes — and carry it into generation.

### Step 4: Gather Input

Ask the user for:
- **Topic or argument** — not just a subject, but a take. "AI agents" is a topic. "Most people build AI agents backwards" is an argument. Push for the argument.
- **Target length** — short post (~150-300 words), long post (~500-800 words), or newsletter (~1000-1500 words)
- **Platform** — LinkedIn, Twitter/X, or newsletter

If the user already provided these in their request, skip the questions and generate.

Accept alternative inputs:
- A tweet or post to expand on ("echo draft from tweet: [text]")
- A rough idea to develop ("echo draft: [concept]")
- A topic seed from conversation context

### Step 5: Generate

Write the piece using every rule from creative-coaching.md as hard constraints:
- Bursty rhythm (varied sentence and paragraph lengths)
- Concrete details over abstract concepts
- Positive framing (say what things ARE, not what they aren't)
- No banned words, phrases, structures, or punctuation
- Surprising, specific, incomplete where it earns it

Match the voice and cadence from the voice template. Not similar — match it.

### Step 6: Self-Check (Pre-Eval)

Before running eval scripts, do a manual scan for obvious violations:

**Banned Structures:**
- [ ] No "Here's what/why/how" openers
- [ ] No "The truth/reality/fact is" setups
- [ ] No "Most people/founders/everyone" openers
- [ ] No negative definitions (isn't, wasn't, aren't, didn't, nobody, no one, not even, not the)
- [ ] No rule of three (three parallel short sentences in a row)

**Banned Punctuation:**
- [ ] No em dashes or en dashes
- [ ] No spaced hyphens
- [ ] No colons after setup phrases
- [ ] Max one exclamation mark in the entire piece

**Banned Words:**
- [ ] None of: framework, leverage, optimize, landscape, ecosystem, scalable, innovative, game-changer, level up, furthermore, moreover, in conclusion

**Banned Questions:**
- [ ] No "Sound familiar?", "Want to know?", "Ready to?", "Guess what?"
- [ ] No "And the wildest/craziest/best part?"
- [ ] No "Let that sink in", "Read that again"

**Rhythm Check:**
- [ ] At least one single-sentence paragraph
- [ ] At least one sentence under 6 words
- [ ] At least one sentence over 30 words
- [ ] No three consecutive sentences within 5 words of each other in length
- [ ] Paragraph lengths vary by at least 2x

Fix any violations found before proceeding to auto-eval.

### Step 7: Auto-Eval

Write the generated content to `/tmp/echo-draft-output.txt`, then run both eval scripts:

```bash
python3 eval/human-eval.py /tmp/echo-draft-output.txt
```

```bash
python3 eval/punctuation-scanner.py /tmp/echo-draft-output.txt
```

Parse both outputs to extract scores. Combined score = min(regex_score, punctuation_score).

### Step 8: Score Gate

**If combined score >= 80:** Proceed to Step 10 (Save and Present).

**If combined score < 80:** Proceed to Step 9 (Self-Improvement Loop).

### Step 9: Self-Improvement Loop

1. Read the flags/patterns from both eval outputs
2. Identify the specific sentences that triggered flags
3. Rewrite ONLY the flagged sentences. Do not touch clean sentences.
4. Write the improved version to `/tmp/echo-draft-output.txt`
5. Re-run both eval scripts
6. Check new combined score

Repeat up to 3 total cycles. Track which cycle produced the best score.

If after 3 cycles the score is still below 80, present the best-scoring version (not necessarily the last one).

### Step 10: Save Output

Save the final draft to `output/` with a timestamped filename:

```
output/YYYY-MM-DD-[slug].md
```

Where `[slug]` is a 3-5 word kebab-case summary of the topic.

After saving, update `.coworker/index.md`:
- Add a line under a "Recent Output" section noting the filename, platform, and date
- If the section doesn't exist, create it at the bottom of the file

### Step 11: Present

Show the final draft to the user with this footer:

```
---
Score: [combined_score]/100 (regex: [regex_score], punctuation: [punct_score])
Cycle: [which cycle produced this version, e.g., "1 of 1" or "2 of 3"]
Saved: output/[filename]
Patterns found: [list any remaining flags, or "None"]
```

If the score is below 80, add:
```
Note: Best score after 3 improvement cycles. Remaining flags above may benefit from manual editing.
```

## Scoring Existing Content

If the user says "score this" or "eval this" followed by content:
1. Write the content to `/tmp/echo-draft-output.txt`
2. Run both eval scripts
3. Report the combined score and any flags
4. Skip generation, improvement, and save steps

## What This Skill Does NOT Do

- Does not publish content anywhere
- Does not modify eval scripts or training data
- Does not bypass the eval step (every generation gets scored)
- Does not run more than 3 improvement cycles
