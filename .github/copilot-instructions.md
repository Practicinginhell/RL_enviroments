# GitHub Copilot instructions

Canonical agent instructions live in [AGENTS.md](../AGENTS.md) at the repository
root — read and follow that file. Keep behavior rules there, not here. The load-bearing
points:

- Use the `./scripts/*` wrappers (setup, dev, test, lint, format, build) — never guess
  raw stack commands.
- Pull deeper context from `ai/context/` (architecture, domain glossary, conventions)
  per the loading policy in AGENTS.md.
- Before declaring work done, verify it against `ai/checklists/pre-merge.md`.
