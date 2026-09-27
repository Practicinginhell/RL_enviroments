---
name: new-skill
description: >-
  Use when creating, authoring, or extracting an agent skill — the user says "create
  a skill", "turn this into a skill", "make the agent always do this", or the same
  multi-step procedure has now been performed twice and should be captured. Covers
  placement, naming, and the craft of trigger descriptions.
---

# Author a New Skill

Skills are how this template grows its own automation. This skill exists because the
hard part — writing a `description` that fires at the right moments and only those —
is a craft with rules.

## Procedure

1. **Confirm it should be a skill.** A skill is a *procedure applied when the task
   matches* — auto-triggered by Claude, typed as `/name`, or both (slash commands are
   skills now). If it's tool-agnostic human-invoked guidance → `ai/prompts/`; a
   verification gate → `ai/checklists/`; always-on behavior → `AGENTS.md`. One skill
   = one capability — split anything with "and also" in its purpose.
2. **Create the folder**: `.claude/skills/<kebab-name>/` — name it after the outcome
   (verb-noun: `write-adr`, `wire-stack`). Copy `ai/templates/skill.md` to `SKILL.md`
   inside it.
3. **Write the `description` first** — it is the only part loaded until the skill
   fires, so it carries the entire triggering decision:
   - state WHEN to use it, not what it is ("Use when…", not "A skill for…")
   - include the literal words a matching request would contain
   - name the negative space if confusable with another skill ("for X; for Y use Z")
4. **Pick the invocation control** (frontmatter, all optional):
   - side effects or timing the human should own (deploy, commit, release) →
     `disable-model-invocation: true` — only a typed `/name` runs it
   - background knowledge that isn't an action → `user-invocable: false`
   - heavy research or verification that would fill the main context →
     `context: fork` (add `agent: Explore` for read-only exploration)
   - commands the procedure always needs → `allowed-tools` (e.g.
     `Bash(git diff *)`) so they run without prompts; a `` !`cmd` `` line injects
     the command's live output before Claude reads the body; `$ARGUMENTS` receives
     what was typed after `/name`.
5. **Write the body** as a briefing to a competent stranger: numbered steps with real
   repo paths and commands, a checkable definition of done, links to `ai/context/`
   instead of restating conventions (duplicated rules drift).
6. **Add supporting files** (scripts, reference docs) in the same folder and link
   them — they're only read when the skill fires, so they're context-cheap.
7. **Test the trigger.** Write 2–3 realistic requests that *should* fire it and one
   nearby request that *shouldn't*; check the description alone decides all of them
   correctly. Fix the description, not the requests. For a `/name`-only skill,
   confirm `disable-model-invocation: true` is set instead.

## Definition of done

- [ ] `SKILL.md` exists with frontmatter `name` matching the folder
- [ ] Description passes the fire / don't-fire test from step 6
- [ ] Body references real paths; no conventions duplicated from `ai/context/`
