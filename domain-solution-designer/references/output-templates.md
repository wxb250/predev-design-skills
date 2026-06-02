# Domain and Solution Package

1. Problem framing
2. Core domain concepts
3. Entity and state model
4. Data and storage design
5. Integration and runtime responsibilities
6. Consistency, concurrency, and failure concerns
7. Tradeoffs and recommended approach
8. Open questions

## Solution Rules

- Tie storage and runtime choices back to business invariants.
- Keep sync and async responsibilities distinct.
- Make lifecycle and failure behavior explicit.
- Stay technology-aware without forcing a stack unless required.
