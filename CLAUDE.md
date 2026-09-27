# CLAUDE.md

<!-- Claude Code reads CLAUDE.md, not AGENTS.md. So we need this line-->

@AGENTS.md

## Claude Code

Everything above (via the import) is tool-agnostic. This section is Claude-specific.

- **Skills** (`.claude/skills/`) — one system for auto-triggered procedures *and*
  typed `/name` workflows (slash commands are merged into skills). Auto-triggered:
  `wire-stack` (adopt the template for a stack), `update-context` (knowledge upkeep),
  `write-adr`, `capture-lesson` (corrections → rules), `checklist` (verification
  gates). User-invoked only: `/plan <task>` (`disable-model-invocation: true`).
  Author the next one with `new-skill` from `ai/templates/skill.md`.
- **Subagents** (`.claude/agents/`) — `code-reviewer` and `test-runner`; use them
  proactively after meaningful changes to keep the main context clean (AGENTS.md §7).
- **Rules** (`.claude/rules/`, optional) — path-scoped rules (`paths:` frontmatter)
  that load only when Claude touches matching files. Keep the substance in
  `ai/context/conventions/`; a rule file is a thin pointer to it.
- **Hooks** (`hooks` in `.claude/settings.json`) — for actions that must happen every
  time with zero exceptions (e.g. format after every edit). Instructions here are
  advisory; hooks are deterministic.
- **Settings** (`.claude/settings.json`) — shared permissions pre-approve the
  `./scripts/*` wrappers and read-only git. Personal overrides go in gitignored
  `settings.local.json` (copy the `.example`).

Claude-specific workflow notes:

- Plan-mode specs go to `tasks/todo.md`, per the Task Management Workflow in AGENTS.md.
- Prefer `./scripts/*` wrappers over raw stack commands — they're pre-approved, so
  fewer permission prompts.
- Long runs follow AGENTS.md §9. A user message sent mid-run amends the current
  task — fold it in and keep going, don't restart.
- Don't reproduce your internal reasoning in replies. When asked why, explain the
  choice briefly (a few sentences).
- Auto memory is personal and machine-local. Corrections the whole team should learn
  from still go to `tasks/lessons.md` via the `capture-lesson` skill.
