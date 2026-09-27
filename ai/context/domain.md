# Domain Glossary

> The project's ubiquitous language. Load this before naming anything — types,
> functions, tables, endpoints, UI copy. One concept gets exactly one name, and code
> uses the same words the business does.

## Terms

| Term | Meaning | In code |
| --- | --- | --- |
| TODO | Plain-language definition | `TodoType`, `todo_table` |

## Naming rules

- **One concept, one name.** If the business says "customer", the code never says
  "client" or "user" for the same thing.
- **No synonyms across layers.** The API field, DB column, and UI label for a concept
  share a root name.
- **New domain concept?** Add it to this table in the same change that introduces it.

## Things that look similar but aren't

Disambiguate the trap pairs that cause bugs:

- TODO — e.g. "*order* (customer intent) vs *shipment* (fulfillment); one order can
  have many shipments."
