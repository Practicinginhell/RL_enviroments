# AGENTS.md

Canonical instructions for **every** coding agent working in this repository — Claude
Code, Codex, Gemini CLI, Cursor, Copilot, and whatever comes next. The tool-specific
entry files (`CLAUDE.md`, `GEMINI.md`, `.github/copilot-instructions.md`) are thin
adapters that import or point to this file. **Edit agent behavior here, once.**

Two parts: **project facts** (snapshot, commands, map, context policy — fill in per
project) and the **working contract** (how to think, change code, and verify — travels
with the template).

---

## Project Snapshot

<!-- TODO: fill in for your project (or run your tool's /init and distill the result).
Keep it under ~15 lines — this file is loaded every session; depth lives in ai/context/. -->

- **What this is:** TODO — one sentence.
- **Stack:** TODO — languages, frameworks, infrastructure.
- **Entry points:** TODO — where execution starts.
- **Status:** TODO — greenfield / active / maintenance.

## Commands

Always use these wrappers — never guess raw stack commands. They are the uniform verbs
of this repo; wire them to the stack in [scripts/](scripts/).

| Verb | Command | Notes |
| --- | --- | --- |
| Setup | `./scripts/setup` | Install deps, prepare env (idempotent) |
| Dev | `./scripts/dev` | Run the app locally |
| Test | `./scripts/test` | Full suite; forwards args for focused runs |
| Lint | `./scripts/lint` | Static analysis, read-only |
| Format | `./scripts/format` | Auto-format in place |
| Build | `./scripts/build` | Production artifact |

## Repository Map

| Path | What lives there |
| --- | --- |
| `AGENTS.md` | This file — global agent instructions, always loaded |
| `ai/context/` | Project context: architecture, domain glossary, conventions (load on demand) |
| `ai/prompts/` | Reusable prompts humans invoke in any AI tool |
| `ai/templates/` | Scaffolds: feature specs, ADRs, bug reports, skills |
| `ai/checklists/` | Verification gates: pre-merge, security, release |
| `.claude/` | Claude Code adapter: settings, skills (incl. `/name` workflows), subagents |
| `docs/` | Human documentation: ADR history, runbooks |
| `tasks/` | Agent working memory: `todo.md` (plans), `lessons.md` (corrections) |
| `scripts/` | The command wrappers from the table above |
| `src/`, `tests/` | Application code and tests (restructure per stack) |

## Context Loading Policy

Keep context lean — pull depth only when the task needs it:

1. **Always:** this file.
2. **Session start:** skim `tasks/lessons.md` (past corrections).
3. **Architectural or cross-module change:** read `ai/context/architecture.md` and
   check `docs/adr/` before proposing structural changes.
4. **Naming things / domain logic:** read `ai/context/domain.md` and use its terms.
5. **Writing code, tests, commits:** follow the matching file in `ai/context/conventions/`.
6. **Before declaring done:** verify against `ai/checklists/pre-merge.md` (plus
   `security-review.md` when a trust boundary is touched).

---

# Coding Agent Guidelines

A unified working contract: how to think, how to change code, and how to verify you're done.

---

## Core Principles

- **Simplicity first.** Minimum code that solves the problem. No speculative features, no abstractions for single-use code, no "flexibility" that wasn't requested.
- **No laziness.** Find root causes. No temporary patches. Hold yourself to a senior developer's standard.
- **Minimal impact.** Every changed line should trace directly to the request. Don't introduce bugs by improving things that weren't broken.
- **Write functions for LLM following these best practices** Write clear, descriptive, and accurate docstrings for your tools. This is essential for the LLM to use the tool correctly.
---

## 1. Think Before Coding

Don't assume. Don't hide confusion. Surface tradeoffs.

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

For non-trivial tasks (3+ steps or architectural decisions), enter **plan mode**: write a detailed spec to `tasks/todo.md` with checkable items, verify the plan with the user, then implement. If something goes sideways mid-task, **stop and re-plan** rather than pushing through.

---

## 2. Simplicity in Practice

- No features beyond what was asked.
- No error handling for impossible scenarios.
- If you wrote 200 lines and it could be 50, rewrite it.
- For non-trivial changes, pause and ask: *"Is there a more elegant way?"* If a fix feels hacky, redo it cleanly. (Skip this for simple, obvious fixes — don't over-engineer.)

The test: *"Would a senior engineer say this is overcomplicated?"* If yes, simplify.

---

## 3. Surgical Changes

Touch only what you must. Clean up only your own mess.

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that **your** changes made unused.
- Don't remove pre-existing dead code unless asked.

---

## 4. Goal-Driven Execution

Define success criteria. Loop until verified.

Every task needs a finish line. If the request doesn't state one, write it down before
starting — "Done means: every endpoint uses the new client, the old client is deleted,
and the suite passes."

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass."
- "Fix the bug" → "Write a test that reproduces it, then make it pass."
- "Refactor X" → "Ensure tests pass before and after."

For multi-step tasks, state a brief plan:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") force constant clarification.

---

## 5. Verification Before Done

Never mark a task complete without proving it works.

- Run tests. Check logs. Demonstrate correctness.
- Diff behavior between main and your changes when relevant.
- Ask: *"Would a staff engineer approve this?"*
- Challenge your own work before presenting it.
- Mark anything you couldn't confirm, and say where you looked. Unverified claims
  must never read like verified ones.

---

## 6. Autonomous Bug Fixing

When given a bug report: just fix it. Don't ask for hand-holding.

- Point at logs, errors, failing tests — then resolve them.
- Zero context-switching required from the user.
- Go fix failing CI tests without being told how.

---

## 7. Subagent Strategy

Use subagents liberally to keep the main context window clean.

- Offload research, exploration, and parallel analysis.
- One task per subagent for focused execution.
- For complex problems, throw more compute at them in parallel.
- For wide work (audits, migrations across many modules), give each unit its own
  subagent and merge the results into one table (see `ai/prompts/fan-out-audit.md`).
- A subagent's report is a claim, not a fact: check its evidence (file:line, command
  output) before accepting it.

---

## 8. Self-Improvement Loop

After **any** correction from the user:

1. Update `tasks/lessons.md` with the pattern.
2. Write a rule for yourself that prevents the same mistake.
3. Review `tasks/lessons.md` at the start of each session.

Iterate ruthlessly until the mistake rate drops.

---

## 9. Long Runs: When to Continue, When to Stop

- When a step doesn't need the user's input, keep going. Put status notes in the same
  message as your next action. Don't stop just to report progress.
- Stop and ask only when you can't continue without the user (plan approval for
  non-trivial tasks counts), or before anything destructive: deleting data,
  force-pushing or rewriting history, or changing anything outside this repository.
- Keep progress in `tasks/todo.md` and check items off as each one finishes. The file
  outlasts the context window, and it shows status without reading the chat.
- End a long run with **Needs from you** first (decisions and approvals that block
  progress), then what changed, how it was verified, and what is still unconfirmed.

---

## Task Management Workflow

1. **Plan first** — write the plan to `tasks/todo.md` with checkable items.
2. **Verify plan** — check in with the user before implementation.
3. **Track progress** — mark items complete as you go.
4. **Explain changes** — high-level summary at each step.
5. **Document results** — add a review section to `tasks/todo.md`.
6. **Capture lessons** — update `tasks/lessons.md` after corrections.