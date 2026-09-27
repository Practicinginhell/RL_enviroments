---
name: capture-lesson
description: >-
  Use immediately after the user corrects a mistake, rejects an approach, restates an
  instruction that was missed, or points out a violated convention — before resuming
  the task. Implements the self-improvement loop from AGENTS.md §8. Trigger signals:
  "no, don't do X", "that's not how we do it", "I already told you…", "undo that",
  or any request to redo work differently.
---

# Capture a Lesson

A correction is data. Recording it as a rule is what stops the same mistake next
session — agents skim `tasks/lessons.md` at session start precisely for this.

## Procedure

1. **Name the pattern, not the incident.** Generalize one step: "used raw npm instead
   of ./scripts/test" is a pattern; "forgot the thing at 3pm" is not; "always be
   careful" is over-generalized. One correction = one lesson.
2. **Prepend an entry** to `tasks/lessons.md` (newest first), in its format:
   - **Mistake:** what actually went wrong, concretely.
   - **Rule:** imperative, checkable by a future agent — it should change behavior,
     not express regret.
3. **Check for promotion.** A lesson about a durable rule belongs in a durable home:
   - code / tests / git / security practice → the matching file in
     `ai/context/conventions/` (via the `update-context` skill)
   - universal behavior needed on every task → propose adding to `AGENTS.md`, but ask
     first — that file is the always-loaded budget.
   If promoted, put the rule in the durable home and keep only a one-line pointer in
   lessons (or drop it) — duplicated rules drift.
4. **Apply it now.** Resume the corrected task with the rule in effect; redo the
   rejected work accordingly.

## Definition of done

- [ ] Entry exists at the top of `tasks/lessons.md` with both Mistake and Rule lines
- [ ] Rule is stated so a future agent could be caught violating it
- [ ] Current task's work now complies with the rule
