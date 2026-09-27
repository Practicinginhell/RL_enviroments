---
name: plan
description: Draft an implementation plan for a task before writing code
argument-hint: <what you want to build>
disable-model-invocation: true
---

Plan how to implement: **$ARGUMENTS**

Do NOT write code yet. Instead produce a short plan:

1. **Goal** — restate the task in one sentence, plus a "Done means: …" line with
   observable finish criteria.
2. **Affected files** — list the files you'll create or change.
3. **Approach** — the steps in order, with the key decisions called out.
4. **Risks / open questions** — anything ambiguous I should confirm first.

Keep it tight. For a non-trivial task, record the plan in `tasks/todo.md` per the
Task Management Workflow in `AGENTS.md`. Wait for my approval before implementing.
