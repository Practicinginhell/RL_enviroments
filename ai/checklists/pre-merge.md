# Checklist: Pre-Merge (Definition of Done)

Run before declaring any change complete. Verify each item with evidence — run the
command, read the output. An unchecked item means the work isn't done.

## Correctness

- [ ] `./scripts/test` passes, run locally just now (paste the summary line)
- [ ] New behavior has tests; a fixed bug has a test that reproduces it
- [ ] Edge cases considered: empty, zero/one/many, malformed input, failure paths
- [ ] Agent review ran before human review (`code-reviewer` subagent or
      `ai/prompts/review-diff.md`); every blocking finding is resolved

## Scope (surgical-change rules from AGENTS.md)

- [ ] Every changed line traces to the request — no drive-by refactors or reformatting
- [ ] Imports/variables/functions orphaned **by this change** are removed
- [ ] No new dependencies — or each one is justified in the PR description

## Quality

- [ ] `./scripts/lint` exits 0
- [ ] `./scripts/format` produces no further changes
- [ ] Names match the glossary in `ai/context/domain.md`
- [ ] Public functions/classes added or changed have accurate docstrings

## Safety

- [ ] No secrets, tokens, or real `.env` values anywhere in the diff
- [ ] If the change touches a trust boundary → `security-review.md` also completed

## Knowledge upkeep

- [ ] `AGENTS.md` / `ai/context/` updated if commands, architecture, or conventions changed
- [ ] ADR written (`ai/templates/adr.md` → `docs/adr/`) if a structural decision was made
- [ ] `tasks/todo.md` review section filled in for this task
