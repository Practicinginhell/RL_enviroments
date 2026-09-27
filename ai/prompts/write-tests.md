# Prompt: Write Tests

**Use when:** backfilling coverage for existing code or specifying behavior for new
code.
**Fill in:** `{target}` — the module/function/feature to cover.

---

Write tests for {target}, following `ai/context/conventions/testing.md`.

1. **Understand before testing.** Read the code and its callers. State the contract
   you believe it has — inputs, outputs, side effects, failure modes. If the contract
   is ambiguous, ask before enshrining a guess in tests.
2. **Cover in this priority order:**
   - the happy path a real caller takes,
   - each documented failure mode / error path,
   - boundaries (empty, zero, one, many, max, malformed),
   - any bug this code has had before (check git log / comments).
3. **Each test asserts one behavior** and is named for it — a failure message alone
   should tell you what broke.
4. **Test through the public surface**, not private internals; no mocking the thing
   under test.
5. **Prove the tests can fail.** For at least the key ones, mutate the code (or
   revert the fix) and confirm the test catches it — a test that can't fail is
   documentation fraud.

Finish with `./scripts/test` green and a one-paragraph summary: what's now covered,
and what you deliberately left uncovered and why.
