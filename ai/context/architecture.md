# Architecture

> Agent-facing map of how the system fits together. Load this when a change spans
> modules, adds a dependency, or touches infrastructure. Keep it current — updating
> this file is part of the definition of done for architectural changes.

## System overview

TODO: One paragraph — what the system is, its main runtime shape (monolith, services,
CLI, mobile app + API, training pipeline, …), and how a request/run flows through it.
An ASCII diagram earns its keep here:

```
[client] → [entry point] → [core logic] → [storage]
```

## Components

| Component | Path | Responsibility | Talks to |
| --- | --- | --- | --- |
| TODO | `src/…` | | |

## External dependencies

| Dependency | Used for | If it's down |
| --- | --- | --- |
| TODO (DB, queue, third-party API, model provider, …) | | |

## Invariants

Things that must never break, no matter the change:

- TODO — e.g. "all writes go through the repository layer, never raw SQL in handlers"
- TODO — e.g. "user data never leaves region X"

## Why it's this way

Architectural decisions and their reasoning live in [docs/adr/](../../docs/adr/).
Before proposing a structural change, check whether an ADR already decided against it.
