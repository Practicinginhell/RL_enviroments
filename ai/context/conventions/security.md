# Convention: Security

> Load when handling input, auth, secrets, dependencies, or anything that crosses a
> trust boundary. The hard rules below are non-negotiable for agents.

## Hard rules for agents

- **Never** read, print, or commit secret values (`.env`, `secrets/`, keys, tokens).
  Reference them by variable name only. `.env.example` documents names, never values.
- **Never** disable or bypass auth, validation, or TLS "temporarily" to make a test
  pass or a demo work.
- **Never** log credentials, session tokens, or personal data.
- **Never** add a new dependency without stating what it's for and why an existing
  one can't do the job.

## Defaults for all code

- **Validate at trust boundaries.** All external input (HTTP, CLI args, file uploads,
  model outputs) is validated before use.
- **Parameterize, don't concatenate** — SQL, shell commands, HTML. Injection is the
  perennial top bug class, for agents too.
- **Least privilege.** New tokens, roles, and DB users get the minimum scope that works.
- **Fail closed.** On auth or validation errors, deny and log — don't fall through to
  the happy path.

## Project specifics

TODO once the stack is chosen:

- Where secrets actually live (vault, cloud secret manager, CI secrets)
- AuthN/AuthZ model and the one true middleware/guard to use
- Data classification: what counts as sensitive here, retention rules
- Dependency policy: allowed licenses, update cadence, audit command

Before merging security-relevant changes, run
[ai/checklists/security-review.md](../../checklists/security-review.md).
