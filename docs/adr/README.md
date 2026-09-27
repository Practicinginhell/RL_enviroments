# Architecture Decision Records

Short documents capturing structural decisions and — the valuable part — *why* they
were made and what was rejected. They stop settled debates from being re-litigated,
by new teammates and by AI agents alike (an agent that reads "we rejected X because Y"
won't helpfully propose X next month).

## Rules

- One decision per record. Copy [ai/templates/adr.md](../../ai/templates/adr.md) to
  `NNNN-short-slug.md` with the next number.
- Write it **when the decision is made**, not retroactively.
- ADRs are immutable history: never edit a decision — supersede it with a new ADR and
  update the old one's status to `superseded by ADR-NNNN`.
- Agents: check this directory before proposing architectural changes
  (see the context-loading policy in `AGENTS.md`).

## Index

| # | Decision | Status |
| --- | --- | --- |
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions as ADRs | accepted |
