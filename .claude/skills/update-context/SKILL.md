---
name: update-context
description: >-
  Use at the end of any change that alters what agents need to know: modules or
  directories added/moved/removed, a new dependency or external service, changed
  commands, renamed domain concepts, or a new convention adopted. Keeps ai/context/
  and the AGENTS.md repository map matching the code. Also use when the pre-merge
  checklist's "knowledge upkeep" items can't be checked off.
---

# Update Project Context

The template's core bargain is that `ai/context/` tells agents the truth. This skill
runs the diff-driven audit that keeps it true after a meaningful change.

## Procedure

1. **List what changed** at knowledge level (not line level): from `git diff --stat`
   and the task itself, note new/moved components, new dependencies, new terms, new
   rules, changed commands.
2. **Route each item to its one home** — update there, nowhere else:

   | Change | Home |
   | --- | --- |
   | Component added/moved/removed | `ai/context/architecture.md` tables + Repository Map in `AGENTS.md` if top-level |
   | New external dependency/service | `ai/context/architecture.md` → External dependencies |
   | New invariant ("must never break") | `ai/context/architecture.md` → Invariants |
   | Domain concept introduced/renamed | `ai/context/domain.md` glossary |
   | Convention adopted/changed | Matching file in `ai/context/conventions/` |
   | Structural decision with rejected alternatives | ADR — use the `write-adr` skill |
   | Command/verb changed | `AGENTS.md` Commands table + `scripts/README.md` |

3. **Delete as you go**: remove lines the change made false, and any `TODO:` markers
   this change resolves. Stale truth is the failure mode, not missing detail.
4. **Respect the budget**: `AGENTS.md` is always-loaded — facts go in `ai/context/`
   unless they're needed on literally every task.

## Definition of done

- [ ] The "Knowledge upkeep" section of `ai/checklists/pre-merge.md` passes honestly
- [ ] No statement in `ai/context/` or the AGENTS.md map is contradicted by the code
- [ ] Nothing was added in two places
