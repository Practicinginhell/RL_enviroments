# scripts/ — Uniform Command Verbs

One wrapper per verb, whatever the stack underneath. This is the
["scripts to rule them all"](https://github.blog/engineering/scripts-to-rule-them-all/)
pattern, and it matters twice as much with AI agents: `AGENTS.md` tells every agent to
run `./scripts/test`, so no agent ever has to guess (or hallucinate) your package
manager, test runner, or flags. CI calls the same wrappers, so agents and CI can never
drift apart.

| Script | Verb | Contract |
| --- | --- | --- |
| `setup` | Install deps, prepare env | Idempotent, non-interactive |
| `dev` | Run the app locally | Foreground, logs to stdout |
| `test` | Run the test suite | Forwards args for focused runs; exit 0 = green |
| `lint` | Static analysis | Read-only; exit 0 = clean |
| `format` | Auto-format in place | Idempotent |
| `build` | Produce a production artifact | Exit 0 = artifact exists |

## Rules

- Every script is runnable from anywhere (they `cd` to the repo root themselves).
- Never interactive — no prompts, no watch modes (put watch modes behind a flag if needed).
- Exit codes are the API: `0` success, non-zero failure. Agents branch on them.
- The stubs `exit 1` with a `TODO` message until you wire them — so nothing can
  silently "pass" before the template is configured.
- Adding a new verb (e.g. `migrate`, `deploy`)? Add the wrapper here **and** add a row
  to the Commands table in `AGENTS.md`.
