# docs/ — Human Documentation

Documentation written for **people first**: onboarding, operations, decision history.
Agents may read it, but nothing here is required context for completing a task — the
agent-facing knowledge lives in [ai/](../ai/) (and the always-on rules in
[AGENTS.md](../AGENTS.md)).

| Section | Contains |
| --- | --- |
| [adr/](adr/) | Architecture Decision Records — the *why* behind structural choices |
| [runbooks/](runbooks/) | Step-by-step operational procedures (deploy, restore, rotate keys) |
| *(add as needed)* | Onboarding guide, API reference, user docs — whatever your project warrants |

## Where a new document belongs

- Explains **how the system works** for agents making changes → `ai/context/`
- Records **a decision and its reasoning** → `adr/` (copy `ai/templates/adr.md`)
- Tells a human **how to operate something in an emergency** → `runbooks/`
- Teaches a **new teammate** the project → here, e.g. `docs/onboarding.md`

Rule of thumb: if an agent needs it *to write correct code*, it's `ai/context/`; if a
human needs it *to understand or operate the project*, it's `docs/`. When one document
serves both, put it here and link to it from `ai/context/`.
