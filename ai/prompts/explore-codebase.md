# Prompt: Explore the Codebase

**Use when:** you (or a fresh agent session) need an accurate mental model of an
unfamiliar area before changing it.
**Fill in:** `{area}` — a directory, feature, or "the whole repo".

---

Explore {area} and build me an accurate map. Do not change anything.

1. **Entry points** — where execution starts and how control flows from there.
2. **Key modules** — for each: path, responsibility in one sentence, and what it
   depends on.
3. **Data** — the core types/tables/schemas and where they're defined.
4. **Conventions in use** — patterns I should imitate when adding code here
   (error handling, naming, layering). Quote real examples with file:line.
5. **Surprises** — anything inconsistent, dead, or risky you noticed. Flag it;
   don't fix it.

Ground every claim in specific files — no guessing from names. Mark anything you
couldn't confirm, and say where you looked. If `ai/context/architecture.md`
disagrees with the code, say so explicitly: the code is the truth and the doc needs
updating. Finish with the three files most worth reading in full before making changes.
