# Output Templates

Use these section templates to keep design outputs stable across projects.

## Full Design Package

1. Background and goal
2. Source materials used
3. Scope and non-scope
4. Main workflows or use cases
5. Module or responsibility boundaries
6. Interface design needs
7. Domain, data, or solution design needs
8. Risks and unresolved questions
9. Recommended next step

## API Contract Package

1. API purpose and assumptions
2. Existing patterns or source references
3. Endpoint list
4. Per-endpoint contract details
5. Shared response and error model
6. Validation and edge cases
7. Open questions

## Domain and Solution Package

1. Problem framing
2. Core domain concepts
3. Entity and state model
4. Data and storage design
5. Integration and runtime responsibilities
6. Consistency, concurrency, and failure concerns
7. Tradeoffs and recommended approach
8. Open questions

## Output Rules

- Separate facts from inferences.
- Preserve project terminology when the source material establishes it.
- Call out missing information instead of inventing it.
- Keep the output implementation-aware but framework-neutral unless the user asks otherwise.
