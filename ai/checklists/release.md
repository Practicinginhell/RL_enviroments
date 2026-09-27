# Checklist: Release

Run before cutting any release or production deploy. TODO: adapt the mechanics
(version scheme, changelog location, deploy command) to your project once they exist.

## Ready

- [ ] `main` is green in CI — build, lint, and tests all pass
- [ ] `pre-merge.md` was completed for every change in this release (spot-check the log)
- [ ] Version bumped per the project's scheme; changelog entry written for humans

## Data & compatibility

- [ ] Migrations run cleanly on a copy of production-like data
- [ ] Rollback path exists and is written down — including for migrations
- [ ] Public API / config / CLI flag changes are backward compatible, or the break is
      documented loudly

## Ship

- [ ] Release artifact built via `./scripts/build` (not from someone's laptop state)
- [ ] Deployed to staging (or closest equivalent) and the critical user journey
      exercised by hand once
- [ ] Monitoring/alerts in place for the parts this release changes

## After

- [ ] Watch error rates/logs for the first minutes post-deploy — don't ship and leave
- [ ] Tag the release in git; announce per team convention
- [ ] Anything learned the hard way → `tasks/lessons.md` and, if a step was missing,
      add it to this checklist
