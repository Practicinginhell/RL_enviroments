# Prompt: Review a Diff Before Human Review

**Use when:** a branch is ready for a human reviewer and you want the agent to catch
merge-blocking problems first.
**Fill in:** `{base}` — the branch to diff against (usually `main`).

---

Review the diff on this branch against {base}. List only problems you'd block the
merge for. For each one, give:

- the file and line,
- why it's wrong,
- how to show it fails (an input, a test, or a command that shows the failure).

Judge against `AGENTS.md` and `ai/context/conventions/`. Skip style nits that
`./scripts/lint` and `./scripts/format` already handle. If you suspect a problem but
couldn't confirm it, mark it unconfirmed and say what you checked. If nothing blocks
the merge, say so in one line.
