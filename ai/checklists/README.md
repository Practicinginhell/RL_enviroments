# ai/checklists/ — Verification Gates

Checklists are how "done" gets proven instead of claimed. Agents (and humans) run the
relevant checklist **at the end of work, before declaring completion** — every item is
verified with evidence, not assumed from the diff.

| Checklist | Gate | Run it when |
| --- | --- | --- |
| [pre-merge.md](pre-merge.md) | Definition of done | Before every merge / before an agent reports "complete" |
| [security-review.md](security-review.md) | Trust-boundary changes | Change touches input handling, auth, secrets, or dependencies |
| [release.md](release.md) | Shipping | Before cutting any release/deploy |

In Claude Code, `/checklist <name>` (see `.claude/skills/checklist/SKILL.md`) runs one
of these against the current change. In other tools, paste the checklist and ask the
agent to verify each item with evidence.

## Authoring rules

- **Every item must be checkable** — a command to run or a thing to observe. "Code is
  clean" is not an item; "`./scripts/lint` exits 0" is.
- **Short beats complete.** A 10-item checklist gets run; a 40-item one gets skimmed.
  Split by concern (that's why security is separate) rather than growing one monster.
- **An item that always passes is dead weight** — automate it (hook, CI, lint rule)
  and remove it from the list. Checklists are for what machines can't yet check.
- When an incident or user correction reveals a missed class of problem, add exactly
  one item for it (and record the pattern in `tasks/lessons.md`).
