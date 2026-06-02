# Source Material Patterns

Use these heuristics when reading mixed project materials.

## PRD or Feature Brief

Extract:

- business goal
- actors and permissions
- success criteria
- scope and exclusions
- explicit rules and edge cases

## PDF Design or Development Docs

Extract:

- module boundaries
- workflows
- state transitions
- non-functional constraints
- technical assumptions

Treat screenshots or diagrams as supporting evidence, not as the only source of rules.

## Spreadsheet Materials

Look for:

- endpoint inventories
- status code tables
- sample payloads
- field naming conventions
- data dictionary patterns

Prefer stable patterns repeated across rows over one-off examples.

## API Examples

Extract:

- request and response envelope
- auth model
- pagination shape
- field naming conventions
- error semantics

Mark fields as inferred if they appear only in examples and are not described elsewhere.

## Schema Notes or Table Drafts

Extract:

- core entities
- relationships
- uniqueness and indexing needs
- lifecycle states
- audit fields

## Cross-Source Reconciliation

- Prefer explicit written rules over screenshots or isolated examples.
- Prefer repeated patterns over singular samples.
- When sources conflict, preserve both and flag the conflict instead of silently choosing one.
- When a source is incomplete, keep the gap visible in the final output.
