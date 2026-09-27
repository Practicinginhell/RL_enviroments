---
name: example-skill
description: >-
  A template skill. Replace this with a clear, specific trigger description so
  Claude knows WHEN to use it — e.g. "Use when generating a new API endpoint
  following this project's controller/service/repository pattern." The description
  is the only part loaded until the skill fires, so make it precise.
---

# Example Skill

A **skill** is a reusable, self-contained capability you teach Claude once and it
applies automatically whenever the `description` above matches the task. Unlike
`CLAUDE.md` (always loaded), a skill's body is only pulled in when triggered — so skills
keep context lean.

## When this runs

Claude reads the `description` in the frontmatter and decides whether the current task
matches. Keep that description action-oriented and specific.

## Instructions

Write the actual procedure here, as if briefing a teammate:

1. Step one — be concrete.
2. Step two — reference real files/commands in this repo.
3. Step three — state the definition of done.

## Conventions to follow

- Bullet the rules that matter for this task.
- Link to a reference doc if the detail is long: see [reference.md](reference.md).

## Example

Show a short before/after or a sample invocation so the pattern is unambiguous.

---

### Notes on authoring skills

- **One skill = one capability.** Split unrelated tasks into separate skills.
- **Supporting files:** drop scripts, templates, or `reference.md` in this folder and
  link to them. Claude reads them only when needed.
- **Scope:** project skills live in `.claude/skills/` (shared via git). Personal skills
  live in `~/.claude/skills/` (available across all your projects).
- **Invocation:** every skill is also a slash command (`/example-skill`) — commands
  and skills are one system. Control who fires it with frontmatter:
  `disable-model-invocation: true` (human only — deploys, commits),
  `user-invocable: false` (Claude only — background knowledge), or the default (both).
- **Useful extras:** `$ARGUMENTS` receives what's typed after `/name`; a
  `` !`cmd` `` line injects live command output before Claude reads the body
  (pre-approve it via `allowed-tools`); `context: fork` runs the skill in an
  isolated subagent.
- Delete this example once you've authored your own.
