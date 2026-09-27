---
name: checklist
description: >-
  Verify the current change against a checklist from ai/checklists/. Use when the
  user runs /checklist <name>, and before declaring any change done (pre-merge),
  when a trust boundary was touched (security-review), or before shipping (release).
argument-hint: <checklist name, e.g. pre-merge>
allowed-tools: Bash(git diff *) Bash(git status *)
---

## Current change

!`git diff --stat`

## Task

Open `ai/checklists/$ARGUMENTS.md` and verify the current change (use `git diff` plus
the conversation context) against every item.

Rules:

- **Verify with evidence** — run the commands, read the code. Don't infer a pass from
  the diff looking right.
- Output the checklist with each item marked ✅ pass / ❌ fail / ➖ not applicable,
  with one line of evidence each (command + result, or file:line).
- If anything fails, propose the smallest fix and wait for my confirmation before
  applying it.
- If no checklist name was given, default to `pre-merge`. If the named file doesn't
  exist, list the available ones in `ai/checklists/`.
