# Prompt: Refactor Safely

**Use when:** restructuring code without changing behavior.
**Fill in:** `{target}` — the code to refactor; `{goal}` — what better looks like
(e.g. "extract the retry logic so it's reusable").

---

Refactor {target}. Goal: {goal}. Behavior must not change.

Rules of engagement:

1. **Baseline first.** Run `./scripts/test` before touching anything. If relevant
   tests are missing, write characterization tests that pin down current behavior —
   including its quirks — before refactoring.
2. **Small reversible steps.** One structural change at a time (rename, extract, move,
   inline), keeping the suite green after each. No drive-by behavior "fixes" — if you
   find a real bug, report it separately; don't fold it into the refactor.
3. **Respect the blast radius.** Update every caller/import your change touches;
   remove code your change orphans; touch nothing else.
4. **Finish clean.** `./scripts/test`, `./scripts/lint`, and `./scripts/format` all
   pass. Summarize what moved where and why the new shape is better, then confirm:
   same inputs, same outputs, fewer places for bugs to hide.

If mid-way you discover the refactor requires a behavior change after all, stop and
say so — that's a different task needing a decision, not something to push through.
