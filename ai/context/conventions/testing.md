# Convention: Testing

> Load when writing tests or verifying a change. The test suite is the agent's main
> feedback loop — these rules keep that loop trustworthy.

## Principles

- **A change isn't done until `./scripts/test` proves it.** "It should work" is not
  evidence.
- **Bug fixes start with a failing test** that reproduces the bug, then make it pass.
- **Never weaken a test to make it pass.** If a test is genuinely wrong, explain why
  before changing it (see `.claude/agents/test-runner.md` — same rule for humans).
- **Test behavior, not implementation.** Tests should survive a refactor that
  preserves behavior.
- **Deterministic or deleted.** Flaky tests get fixed or removed, never retried into
  submission.

## What to test where

| Layer | What it covers | Speed budget |
| --- | --- | --- |
| Unit | Pure logic, edge cases, error paths | milliseconds |
| Integration | Component boundaries (DB, API contracts) | seconds |
| End-to-end | Critical user journeys only | minutes, few of them |

## Project specifics

TODO once the stack is chosen:

- Test framework and how `./scripts/test` invokes it
- Where tests live and how files are named (e.g. `tests/` mirrors `src/`)
- How to run one test fast (agents iterate much faster with a focused runner)
- Fixtures/factories: where shared test data lives
- Coverage expectations, if enforced
