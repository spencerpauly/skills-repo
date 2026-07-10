---
name: write-like-a-human
description: Strip the AI-isms out of any text — em-dash overuse, "It's not just X, it's Y", inflated significance, sycophantic openers, rule-of-three padding. Use when the user says "humanize this", "make this less AI", "tighten this", or pastes obviously-AI prose and asks for a rewrite.
license: MIT
---

# Write Like a Human

Rewrite text so it stops sounding like a language model wrote it. Wraps the open-source [humanizer](https://github.com/blader/humanizer) skill, which catalogs ~30 specific tells (em-dash overuse, "stands as a testament", `-ing` analyses, rule-of-three padding, inline-bold lists, and so on).

## When to use

- The user pastes a chunk of writing and asks to "humanize", "de-AI", "tighten", or "make this sound like me".
- The user asks for editing on something they wrote with an LLM.
- A blog post / launch email / README draft has tells the user wants gone.

## Steps

1. **Load the reference list of patterns** the first time this skill activates in a session. On Spencer's machine, read the canonical local copy (newer than upstream):
   ```bash
   cat ~/.agents/skills/humanizer/SKILL.md
   ```
   Otherwise pull it from upstream:
   ```bash
   curl -fsSL https://raw.githubusercontent.com/blader/humanizer/main/SKILL.md
   ```
   There are ~30 patterns; you don't need to memorize them, just keep them visible while editing.

2. **Ask for a voice sample** if you don't already have one. One paragraph the user wrote themselves is enough. Match cadence, vocabulary, and how they handle transitions. For content written *as Spencer*, the voice layer is the `spencers-writing-style` skill in the stack repo (`.agents/skills/spencers-writing-style/`) — use it instead of asking.

3. **Do a first pass** removing the highest-signal tells in this order:
   1. Sycophantic openers ("Great question!", "Absolutely!").
   2. Em-dashes that should be commas, periods, or parens.
   3. "It's not just X, it's Y" / "Not only … but …" parallelisms.
   4. Inflated significance words: *testament, pivotal, landscape, vibrant, tapestry, underscore*.
   5. Rule-of-three lists that pad ideas into groups of three.
   6. Inline-bold vertical lists (`- **Speed:** …`).

4. **Do a second "audit" pass.** Re-read your draft and ask out loud: *"What still makes this sound AI-generated?"* Answer briefly, then revise once more. This step is the difference between "cleaned up" and "actually sounds human".

5. **Return three things:**
   - A draft rewrite.
   - A short list of remaining tells you noticed during the audit.
   - A final rewrite with those fixed.

## Don't

- Don't replace AI mush with new AI mush. If the original said "stands as a testament to" and you change it to "represents a key milestone in", you haven't fixed anything.
- Don't sand off the user's voice. Quirks, opinions, and the occasional sentence fragment are the *point*.
- Don't add em-dashes back in. If you must use a punctuation break, prefer a period.

## Reference

Patterns and examples: <https://github.com/blader/humanizer>
