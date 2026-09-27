# Prompt: Fan-Out Audit

**Use when:** the same question has to be answered for many units (services,
packages, endpoints), such as auditing for a bug pattern or checking a migration.
**Fill in:** `{units}` — the set to cover (e.g. "every service in `services/`");
`{question}` — what to check in each (e.g. "the retry bug described in #123").

---

Audit {units} for {question}. Give each unit its own subagent. When a subagent
reports back, check its evidence (file:line, command output) before you accept it.
Re-check or re-dispatch any finding without evidence.

Track progress in `tasks/todo.md`, one checkbox per unit, and tick each unit once its
result is verified.

Finish with one table: unit, affected (yes / no / unconfirmed), and the evidence. Mark
anything you couldn't confirm, and say where you looked. Do not fix anything; list
what should be fixed after the table.
