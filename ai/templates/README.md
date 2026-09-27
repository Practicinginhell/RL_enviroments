# ai/templates/ — Artifact Scaffolds

Fill-in-the-blank shapes for the documents this project produces. When a human or
agent needs to create one of these artifacts, they copy the template and fill it in —
so every spec, ADR, and bug report has the same bones, and agents can parse older ones
reliably.

| Template | Produces | Final artifact lives in |
| --- | --- | --- |
| [feature-spec.md](feature-spec.md) | A lightweight spec for a feature before building it | `tasks/` or your tracker |
| [adr.md](adr.md) | An Architecture Decision Record | `docs/adr/NNNN-slug.md` |
| [bug-report.md](bug-report.md) | A bug report an agent can act on without follow-up questions | your tracker / `tasks/` |
| [skill.md](skill.md) | A new agent skill | `.claude/skills/<name>/SKILL.md` |

Templates vs the other shelves: a **template** is a *shape to fill in*; a **prompt**
is an *instruction to execute*; a **checklist** is a *gate to pass*. If your file has
blanks, it's a template.

## Authoring rules

- Every section header earns its place — if authors routinely delete a section, remove
  it from the template.
- Include one line of guidance under each heading (as an HTML comment or quote) saying
  what good looks like; it's the difference between a form and a formality.
- Keep templates short enough that filling one in is faster than arguing about format.
