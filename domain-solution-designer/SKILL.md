---
name: domain-solution-designer
description: Use when a backend feature needs domain and technical solution design before coding, especially when requirements or source materials imply entities, state transitions, storage choices, consistency rules, concurrency concerns, background jobs, caches, queues, or external integrations.
---

# Domain Solution Designer

## Overview

Shape the domain model and backend solution before implementation. Focus on core entities, lifecycle rules, storage structure, runtime responsibilities, and the tradeoffs around consistency, concurrency, and failure handling.

## Workflow

### 1. Frame the capability

Start by stating:

- the business capability being added
- the key invariants that must hold
- what failure looks like
- what must remain auditable or recoverable

If the problem statement is still vague, use `design-from-materials` or `brainstorming` first.

### 2. Identify domain concepts

List the main entities, aggregates, or records involved.

For each one, capture:

- purpose
- ownership
- lifecycle
- relationships
- fields that drive business rules

Prefer business concepts over framework objects.

### 3. Define state and transitions

Make the lifecycle explicit whenever the feature has timing, approval, retries, fulfillment, quota, or expiration behavior.

Document:

- states
- transitions
- transition triggers
- invalid transitions
- compensating or recovery behavior

### 4. Draft storage and indexing

Describe the storage shape needed to support the rules:

- tables or collections
- key fields
- uniqueness constraints
- indexes
- audit timestamps or operator fields
- archive or history needs

Keep the design technology-aware but not pinned to one database unless the project already is.

### 5. Assign runtime responsibilities

State which part of the system owns which work:

- synchronous API path
- async worker or queue
- cache
- object storage
- scheduled task
- external system boundary

This is where the high-level solution becomes buildable.

### 6. Address consistency and failure

Always call out:

- concurrency hazards
- duplicate requests
- partial failure paths
- retry behavior
- timeout boundaries
- observability needs

Do not leave these as implicit implementation details when they materially affect correctness.

## Output Shape

Use the `Domain and Solution Package` structure in `references/output-templates.md`.

The minimum output should cover:

1. Problem framing
2. Core domain concepts
3. Entity and state model
4. Data and storage design
5. Integration and runtime responsibilities
6. Consistency, concurrency, and failure concerns
7. Tradeoffs and recommended approach
8. Open questions

## Guardrails

- Do not jump straight to service or repository class layouts.
- Do not hide uncertainty behind technology jargon.
- Do not overfit the design to one stack unless the materials require it.
- Keep business invariants visible all the way through the solution.

## Quick Checklist

- Are the core entities and relationships explicit?
- Are lifecycle states and transitions visible?
- Is storage structure tied back to business rules?
- Are async and sync responsibilities separated?
- Are consistency and concurrency risks called out?
- Are the main tradeoffs and open questions visible?
