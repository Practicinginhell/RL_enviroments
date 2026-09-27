# ai/prompts/ — Reusable Prompts

Battle-tested prompts a **human invokes on purpose**, in any AI tool — paste one into
Claude Code, Codex, Gemini CLI, or a chat UI. Each file is self-contained: a header
saying when to use it, then the prompt itself with `{placeholders}` to fill in.

How prompts differ from the other reusable pieces:

| Piece | Triggered by | Lives in |
| --- | --- | --- |
| **Prompt** | A human, explicitly, in any tool | `ai/prompts/` |
| **Skill** | The agent when the task matches, a human typing `/name`, or both | `.claude/skills/` |

(In Claude Code, slash commands are skills — a skill with
`disable-model-invocation: true` is the "human-typed `/name` only" case.)

A good pattern: keep the substance here (tool-agnostic), and make tool skills thin
wrappers around these files — see `.claude/skills/checklist/SKILL.md` for the shape.

## Included prompts

| Prompt | Use when |
| --- | --- |
| [explore-codebase.md](explore-codebase.md) | Onboarding an agent (or yourself) to unfamiliar code |
| [debug-issue.md](debug-issue.md) | Something is broken and you want a disciplined diagnosis |
| [refactor-safely.md](refactor-safely.md) | Restructuring code without changing behavior |
| [write-tests.md](write-tests.md) | Backfilling or extending test coverage |
| [review-diff.md](review-diff.md) | A branch is about to go to human review |
| [fan-out-audit.md](fan-out-audit.md) | Asking the same question of many services/packages at once |

## Authoring rules

- One prompt per file; name the file after the outcome.
- Give the **whole task in one prompt** and state the **success criteria inside it**
  ("Done means: …") so the agent can run to the finish line and self-verify.
- No "think hard" / "think step by step" lines. Current models already reason before
  answering, and these lines only slow them down.
- Don't ask the agent to reproduce its internal reasoning in the reply. Ask for a
  short explanation of the choice instead ("explain why in three sentences").
- For UI/design work, list the concrete styles to exclude ("no cream backgrounds, no
  pill-shaped buttons"). A vague "avoid a generic look" doesn't work.
- For research or analysis, require "mark anything you couldn't confirm, and say
  where you looked."
- Use `{placeholders}` for the parts that vary; list them in the header.
- If a prompt encodes project knowledge, link to `ai/context/` instead of duplicating it.
