---
name: write-adr
description: >-
  Use when a structural or technology decision has just been made (or explicitly
  rejected): choosing a framework/database/dependency, an API shape, a cross-cutting
  pattern, or reversing a previous decision. Trigger phrases: "record this decision",
  "write an ADR", "let's go with X" after weighing alternatives. Also use when
  update-context routes a decision here.
---

# Write an ADR

Capture the decision **now**, while the rejected alternatives and real reasons are
fresh. The payload of an ADR is the *why* and the *what lost* — that's what stops the
debate from being re-litigated by future humans and agents.

## Procedure

1. **Claim the next number**: highest `NNNN` in `docs/adr/` plus one, zero-padded.
2. **Copy the template**: `ai/templates/adr.md` → `docs/adr/NNNN-short-slug.md`
   (slug = the decision, e.g. `0002-use-postgres-for-persistence`).
3. **Fill it in**, one page maximum:
   - *Context*: the forces and constraints — understandable to a stranger.
   - *Decision*: active voice, one paragraph. "We will…"
   - *Consequences*: honest costs included; ADRs that admit trade-offs get trusted.
   - *Alternatives considered*: each rejected option with the one real reason it lost.
4. **Set status**: `accepted` if decided, `proposed` if awaiting sign-off. If this
   reverses an earlier ADR, mark the old one `superseded by ADR-NNNN` — never edit
   the old decision's content.
5. **Update the index** table in `docs/adr/README.md`.
6. **Link it** from `ai/context/architecture.md` if the decision changes the system map.

## Definition of done

- [ ] `docs/adr/NNNN-slug.md` exists, ≤ 1 page, all four sections substantive
- [ ] Index in `docs/adr/README.md` has the new row
- [ ] Superseded ADR (if any) has its status updated
