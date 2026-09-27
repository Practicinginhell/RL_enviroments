# Prompt: Debug an Issue

**Use when:** something is broken and you want root-cause diagnosis, not patch
roulette.
**Fill in:** `{symptom}` — the error, failing test, or wrong behavior, with any
logs/output you have.

---

Debug this issue:

{symptom}

Work in this order, and after each step state what you found in a sentence or two:

1. **Reproduce.** Find the smallest reliable way to trigger it (a focused
   `./scripts/test` run if possible). If you can't reproduce it, stop and report what
   you'd need.
2. **Localize.** Trace from symptom to cause — read the code, add temporary
   instrumentation if needed. Name the exact file:line where behavior diverges from
   intent.
3. **Explain.** State the root cause in two sentences, and why it produces exactly
   this symptom. If your explanation doesn't account for every observed detail, keep
   digging.
4. **Fix.** The smallest change that removes the root cause — not a guard that hides
   the symptom. Remove any temporary instrumentation you added.
5. **Prove.** A test that failed before the fix and passes after. Run the full
   `./scripts/test` to check for regressions.

If you find yourself proposing a second fix because the first didn't work, stop —
return to step 2, the localization was wrong.
