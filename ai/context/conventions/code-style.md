# Convention: Code Style

> Load when writing or reviewing code. Formatting is a machine's job —
> `./scripts/format` owns whitespace; this file covers what formatters can't.

## Universal rules (any language)

- **Clarity over cleverness.** Optimize for the next reader, who has no context.
- **Small units.** A function does one thing; if you need "and" to describe it, split it.
- **Names carry meaning.** Use glossary terms from [domain.md](../domain.md); avoid
  abbreviations that aren't in the glossary.
- **Errors are handled or propagated, never swallowed.** No empty catch blocks; no
  logging-and-continuing past a broken invariant.
- **Comments explain *why*, not *what*.** If the code needs a "what" comment, rewrite
  the code.
- **Docstrings on public surfaces.** Every exported function/class states what it
  does, its inputs/outputs, and failure modes — agents rely on these to call code
  correctly.

## Stack-specific rules

TODO: replace with your language's rules once the stack is chosen. Examples of the
kind of rule that belongs here:

- "TypeScript: no `any`; prefer discriminated unions over enums."
- "Python: type hints required; dataclasses over dicts for structured data."
- "Go: accept interfaces, return structs."

## Tooling

| Concern | Owner |
| --- | --- |
| Formatting | `./scripts/format` (never hand-format) |
| Static checks | `./scripts/lint` |
