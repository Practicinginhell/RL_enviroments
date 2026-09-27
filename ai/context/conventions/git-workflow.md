# Convention: Git Workflow

> Load when committing, branching, or opening a PR. These rules apply to humans and
> agents alike; the "Agents specifically" section adds the extra guardrails for
> automated actors.

## Branches

- `main` is always releasable. Work happens on short-lived branches.
- Naming: `feat/<slug>`, `fix/<slug>`, `chore/<slug>` — TODO: adjust to taste.

## Commits

- Small, atomic commits; each message explains **why**, not just what.
- Format: TODO — e.g. [Conventional Commits](https://www.conventionalcommits.org/)
  (`feat: …`, `fix: …`) if you want changelog automation.
- Never commit secrets, `.env` files, or generated artifacts.

## Pull requests

- Fill in the template at `.github/PULL_REQUEST_TEMPLATE.md` — including how the
  change was verified.
- Complete [ai/checklists/pre-merge.md](../../checklists/pre-merge.md) before
  requesting review.

## Agents specifically

- **Commit or push only when the user asks.** Never assume.
- Never push directly to `main`; never force-push; never rewrite published history.
- Never amend or revert commits you didn't create.
- Disclose agent involvement per the PR template's "AI assistance" section.
