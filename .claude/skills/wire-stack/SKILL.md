---
name: wire-stack
description: >-
  Use when adopting this template for a real project: wiring the scripts/ command
  wrappers (setup, dev, test, lint, format, build) to a chosen stack, or whenever a
  script still exits with its TODO stub. Trigger phrases: "set up this template",
  "wire the scripts", "initialize this repo for <stack>", "scripts/test says TODO".
---

# Wire the Stack

Turn the template's deliberately-failing script stubs into working uniform verbs.
This is step one of template adoption — agents, CI, and half the checklist items
depend on these six scripts working.

## Procedure

1. **Confirm the stack** — language, package manager, test runner, linter, formatter,
   build tool. Infer from existing manifests (`package.json`, `pyproject.toml`,
   `go.mod`, `Cargo.toml`, …) if present; if nothing is stated or inferable, ask —
   don't guess a stack.
2. **Wire each script** in `scripts/`. Replace the stub's `echo`/`exit 1` lines with
   real commands, keeping the contract from [scripts/README.md](../../../scripts/README.md):
   - keeps `set -euo pipefail` and the `cd "$(dirname "$0")/.."` preamble
   - non-interactive, no watch modes
   - `test` forwards `"$@"` so focused runs work
   - exit code is the API: 0 = success
3. **Verify each verb** by running it:
   - `setup` twice — second run must succeed too (idempotent)
   - `test`, `lint`, `format`, `build` — run and confirm real tool output, not the TODO message
   - `dev` — starts, then stop it
4. **Enable CI**: in `.github/workflows/ci.yml`, add the toolchain setup step and
   switch `workflow_dispatch` to the commented `push`/`pull_request` triggers.
5. **Update the always-on facts**: fill the Stack line of the Project Snapshot in
   `AGENTS.md`; if you added a new verb (e.g. `migrate`), add its row to the AGENTS.md
   Commands table and `scripts/README.md`.

## Definition of done

- [ ] All six scripts run their real commands — `grep -rl "TODO(scripts" scripts/` returns nothing
- [ ] `./scripts/test` executes the actual runner (fine if 0 tests yet)
- [ ] `./scripts/setup` ran twice cleanly
- [ ] CI workflow has toolchain setup and push/PR triggers enabled
- [ ] AGENTS.md Snapshot/Commands reflect reality
