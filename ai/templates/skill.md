<!-- Template for a new agent skill. Copy to .claude/skills/<skill-name>/SKILL.md.
The frontmatter `description` is the ONLY part loaded until the skill triggers —
it must say precisely WHEN to use the skill, in the words a task would use. -->

---
name: <skill-name-kebab-case>
description: >-
  Use when <specific, recognizable situation — e.g. "adding a new API endpoint
  following this project's controller/service/repository pattern">. Trigger words:
  <the words a user's request would actually contain>.
# Optional frontmatter — delete what you don't need:
# disable-model-invocation: true   # only a typed /name runs it (deploys, commits)
# user-invocable: false            # only Claude can fire it (background knowledge)
# context: fork                    # run in an isolated subagent; add `agent: Explore`
# allowed-tools: Bash(git diff *)  # pre-approve the commands the procedure needs
# argument-hint: <what to type after /name>   # $ARGUMENTS receives it in the body
---

# <Skill Name>

<!-- One sentence: what this skill produces or guarantees. -->

## Procedure

<!-- Concrete steps referencing real files and commands in this repo. Write it like
you're briefing a competent teammate who has never done this task here. -->

1.
2.
3.

## Definition of done

<!-- How the agent verifies it worked — a command to run, an output to check. -->

- [ ]

## Conventions that apply

<!-- Only the rules specific to this task. Link to ai/context/ for anything general —
don't duplicate it here, duplicated rules drift. -->

- See [ai/context/conventions/](../../../ai/context/conventions/)

## Example

<!-- A short before/after or sample invocation that makes the pattern unambiguous. -->
