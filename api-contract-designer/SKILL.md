---
name: api-contract-designer
description: Use when backend or integration work needs endpoint contract design from requirements, PDFs, spreadsheets, sample payloads, or existing APIs, including request and response schemas, status codes, auth behavior, pagination, validation, and error semantics.
---

# API Contract Designer

## Overview

Turn business rules and source examples into explicit API contracts. Make endpoint boundaries, request and response structures, validation rules, and error semantics unambiguous before implementation starts.

## Workflow

### 1. Start from existing patterns

Look for project-level conventions before inventing new ones:

- response envelope
- field naming style
- status code usage
- auth model
- pagination shape
- filtering and sorting patterns

If the source materials already establish a pattern, preserve it unless there is a concrete reason to change it.

### 2. Define endpoint boundaries

State:

- the business capability each endpoint serves
- the owning module or resource boundary
- the caller assumptions
- whether the endpoint is read, write, or asynchronous trigger

Avoid mixing unrelated responsibilities into one contract.

### 3. Specify each contract explicitly

For every endpoint, define:

- method and path
- purpose
- auth or caller constraints
- request parameters
- request body shape
- response shape
- status and error outcomes
- edge-case behavior

Mark fields as required, optional, derived, or server-controlled.

### 4. Standardize the shared contract layer

Describe the shared rules once:

- response envelope
- error envelope
- pagination structure
- idempotency behavior
- validation failure behavior
- trace or request identifiers when relevant

Do not leave these as implied conventions if multiple endpoints depend on them.

### 5. Surface weak points

Call out places where the contract is still underdefined, such as:

- unclear ownership of a field
- missing business validation rules
- conflicting source examples
- uncertain status code semantics
- missing async or retry behavior

## Output Shape

Use the `API Contract Package` structure in `references/output-templates.md`.

The minimum output should cover:

1. API purpose and assumptions
2. Existing patterns or source references
3. Endpoint list
4. Per-endpoint contract details
5. Shared response and error model
6. Validation and edge cases
7. Open questions

## Guardrails

- Do not reduce the work to curl or fetch snippets.
- Do not output OpenAPI unless the user asks for it.
- Do not assume REST purity matters more than project consistency.
- Keep the main artifact contract-first, not client-example-first.
- Keep long contract documents easy to scan in Markdown readers:
  - add a short overview or endpoint map before detailed sections
  - group endpoints by resource or workflow, not by arbitrary numbering alone
  - use short explanatory lead-ins before dense tables
  - keep paragraphs short and avoid large uninterrupted walls of field definitions
  - add quick-locate hints for common caller paths such as auth, learner flow, admin flow, or internal APIs
  - when many shared structures exist, include a compact "most important updates" summary near the top

## Quick Checklist

- Is module ownership clear?
- Are request and response shapes explicit?
- Are required versus optional fields marked?
- Are auth and validation rules visible?
- Are pagination, filtering, and sorting conventions covered where relevant?
- Are error semantics and edge cases spelled out?
