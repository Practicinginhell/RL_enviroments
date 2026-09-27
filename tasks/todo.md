# Task Plans

Working memory for tasks, per the workflow in `AGENTS.md`: plan here first, get the
plan confirmed, check items off while implementing, close with a review section.
Finished tasks can be pruned once their lessons/docs are captured — this file is a
workbench, not an archive.

## Current task

## Apply "Getting the most out of Opus 5.5" guidance — 2026-09-22

**Goal:** Fold the article's recommendations (claude.dev/blog/getting-the-most-out-of-opus-5-5,
2026-09-22) into the template. Done means: stopping rules, subagent verification,
file-based progress, "Needs from you" reporting, blocking-only pre-human review, and
"mark unconfirmed" research are encoded in the canon/agents/prompts; no "think hard"
or "show your reasoning" phrasing remains; destructive commands still prompt.

**Plan**

- [x] `AGENTS.md`: §4 "Done means" line, §5 mark-unconfirmed, §7 verify subagent evidence, new §9 long runs (continue/stop rules, progress file, "Needs from you" report) → verify: read-through, no § renumbering ✓
- [x] `CLAUDE.md`: mid-run follow-ups, no reasoning reproduction → verify: read-through ✓
- [x] `.claude/settings.json`: `ask` for destructive commands → verify: valid JSON ✓ (applied after user approval)
- [x] `code-reviewer` agent: blocking-only findings with file:line / why / how to show it fails → verify: read-through ✓
- [x] Prompts: drop "show your reasoning" (debug-issue), add mark-unconfirmed (explore-codebase), new `review-diff.md` + `fan-out-audit.md`, authoring rules in README → verify: grep finds the phrasing only where it's quoted as advice ✓
- [x] feature-spec, todo template, pre-merge checklist, README → verify: grep for § refs all resolve ✓ (`/plan` skill wording applied after user approval)

**Review**

- Needs from you: none.
- What changed: agent-side rules for long runs (AGENTS.md §9: continue vs stop,
  `tasks/todo.md` as the progress file, "Needs from you" report first), finish lines
  (§4), mark-unconfirmed (§5), fan-out plus subagent evidence checks (§7). Prompt
  authoring rules drop "think hard" and requests to reproduce reasoning. New prompts
  `review-diff.md` and `fan-out-audit.md`. The pre-merge checklist now requires an
  agent review before human review. README has tips for the human at the keyboard
  (fast mode, flagged-message recovery).
- How it was verified: grep for think-hard and show-your-reasoning phrasing; all §
  references resolve (no renumbering). Docs only, so there is no test suite to run.
- Also: `.claude/settings.json` `ask` += `git reset --hard`, `git clean`,
  `git branch -D`, `rm -rf`; `code-reviewer` reports blocking-only findings (file:line,
  why, how to show it fails); `/plan` asks for a "Done means" line. These needed
  explicit user approval (auto mode blocks `.claude/` self-modification).
- Follow-ups / deferred: none.

---

## Update template to current Claude Code best practices — 2026-08-22

**Goal:** Bring the template in line with current (Aug 2026) Claude Code docs: commands→skills unification, new skill frontmatter, `.claude/rules/`, auto memory, hooks guidance — verified against code.claude.com/docs.

**Plan**

- [x] Migrate `.claude/commands/{plan,checklist}.md` → `.claude/skills/{plan,checklist}/SKILL.md` → verify: files exist, commands dir removed ✓
- [x] Modernize skill-authoring guidance (`ai/templates/skill.md`, `example-skill`, `new-skill`) with current frontmatter fields → verify: no stale `.claude/commands` advice remains ✓
- [x] Update `CLAUDE.md` Claude-specific section (skills unification, rules, auto memory vs lessons.md, hooks) → verify: read-through ✓
- [x] Update `AGENTS.md` repository map + `README.md` layout/tables → verify: grep shows no stale refs ✓
- [x] Sweep remaining references to `.claude/commands` across the repo (`ai/*/README.md`, `.gitignore`) → verify: grep returns nothing ✓

**Review**

- What changed: `/plan` and `/checklist` are now skills (`/plan` is user-invoked only
  via `disable-model-invocation: true`; `checklist` stays model-invocable as a
  verification gate, grounds itself with an injected `git diff --stat`, and
  pre-approves its git commands via `allowed-tools`). Skill-authoring guidance
  (template, example-skill, new-skill) documents current frontmatter:
  `disable-model-invocation`, `user-invocable`, `context: fork` + `agent`,
  `allowed-tools`, `$ARGUMENTS`, `` !`cmd` `` injection. CLAUDE.md gained notes on
  `.claude/rules/` (path-scoped rules), hooks-vs-instructions, and auto memory vs
  the shared `tasks/lessons.md`. README/AGENTS.md/ai READMEs/.gitignore updated to
  match (incl. `CLAUDE.local.md` ignore and a plugin-packaging note). Facts verified
  against code.claude.com/docs (memory, skills, sub-agents, best-practices) on
  2026-08-22; the `@AGENTS.md` import remains the officially documented pattern.
- How it was verified: repo-wide grep for `.claude/commands` returns nothing; the
  new/edited skills were re-registered live by Claude Code during the session
  (frontmatter parses).
- Follow-ups / deferred: consider `memory: project` on `code-reviewer`/`test-runner`
  subagents (persistent agent memory — left out as too opinionated for a default);
  consider a format-after-edit PostToolUse hook once `scripts/format` is wired.

---

_Start the next non-trivial task by writing its plan below, using this shape:_

---

## <Task name> — <YYYY-MM-DD>

**Goal:** <one sentence; what "done" observably means>

**Plan**

- [ ] <Step> → verify: <command or observable check>
- [ ] <Step> → verify: <…>
- [ ] Run `ai/checklists/pre-merge.md` → verify: all items pass

**Review** *(fill in when done)*

- Needs from you: (decisions/approvals blocking progress; "none" if none)
- What changed:
- How it was verified:
- Follow-ups / deferred:
