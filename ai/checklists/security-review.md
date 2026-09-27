# Checklist: Security Review

Run in addition to `pre-merge.md` when a change touches input handling, auth,
secrets, data storage, or dependencies. Rules of the road live in
`ai/context/conventions/security.md`; this list verifies this specific diff.

## Input & injection

- [ ] All new external input (HTTP, CLI, files, env, model output) is validated before use
- [ ] No string-built SQL/shell/HTML — parameterized queries, arg arrays, escaping/templating
- [ ] File paths derived from input are constrained (no traversal to arbitrary paths)

## AuthN / AuthZ

- [ ] New endpoints/operations declare who may call them — nothing is open "for now"
- [ ] Authorization is checked server-side per request, not only in the UI
- [ ] Nothing bypasses the project's standard auth guard/middleware

## Secrets & data

- [ ] No secrets in code, config, tests, fixtures, or logs — env var names only
- [ ] New credentials/tokens/roles have the minimum scope that works
- [ ] Sensitive data isn't newly logged, cached, or sent to third parties
- [ ] Error messages shown to users don't leak internals (stack traces, queries, paths)

## Dependencies

- [ ] Each new dependency: actively maintained, license compatible, name spelled
      exactly (typosquatting check)
- [ ] Lockfile updated and committed alongside the manifest

## Failure behavior

- [ ] Auth/validation failures fail **closed** (deny + log), not open
- [ ] Rate limiting / abuse considered for anything newly reachable from outside
