# ai/ — Tool-Agnostic AI Knowledge Base

Everything in this directory is **plain Markdown that any coding agent can read** —
Claude Code, Codex, Gemini CLI, Cursor, Copilot, or a tool that doesn't exist yet.
Nothing here depends on a specific vendor's config format; the vendor-specific layers
(`.claude/`, `GEMINI.md`, …) are thin adapters that *point into* this directory.

## The four shelves

| Shelf | Contains | Loaded when | Question it answers |
| --- | --- | --- | --- |
| [`context/`](context/) | Architecture, domain glossary, conventions | On demand, per the policy in `AGENTS.md` | *"What do I need to know about this project?"* |
| [`prompts/`](prompts/) | Reusable prompts a human invokes | When you paste/invoke one | *"How do I ask an agent to do X well?"* |
| [`templates/`](templates/) | Scaffolds for artifacts (specs, ADRs, bug reports, skills) | When creating that artifact | *"What shape should this document take?"* |
| [`checklists/`](checklists/) | Verification gates (pre-merge, security, release) | At the end of work, before "done" | *"How do I prove this is finished?"* |

How this differs from its neighbors:

- **`AGENTS.md`** (repo root) is *always* loaded — it holds only the rules every task
  needs. Content here in `ai/` is loaded *on demand* to keep context lean.
- **`docs/`** is written for humans first (onboarding, runbooks, ADR history). Agents
  may read it, but nothing in `docs/` is required to complete a task.
- **`tasks/`** is per-task working memory (plans, lessons), not durable knowledge.
- **`.claude/skills|agents/`** are executable *bindings*: they wire an agent tool to
  the knowledge in here (e.g. the `checklist` skill's `/checklist pre-merge` reads
  `ai/checklists/pre-merge.md`).

## Authoring rules

1. **One topic per file.** Agents load files whole; small files = cheap context.
2. **Truth over aspiration.** Describe the project as it is. A stale architecture doc
   is worse than none — updating `ai/context/` is part of the definition of done.
3. **No secrets, ever.** These files are prime agent-context; assume every line ends
   up in a model prompt.
4. **Write for a capable stranger.** The reader knows software, not your project.
   Spell out names, paths, and reasons.
5. **Keep `TODO:` markers honest.** They tell agents "this is unfilled template", not
   "this is true". Delete them as you fill things in.
