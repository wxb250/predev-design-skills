---
name: design-from-materials
description: Use when a project starts from source materials such as PRDs, PDFs, spreadsheets, API examples, schema notes, or prototype descriptions and those materials need to be turned into a build-ready backend or API design draft before implementation planning.
---

# Design From Materials

## Overview

Turn mixed project materials into a stable pre-development design package for backend, platform, admin, workflow, or API-heavy work. Extract facts first, label inferences clearly, and keep the result implementation-aware without locking it to a framework unless the materials require that.

## Workflow

### 1. Check fit

Use this skill when the request is driven by source materials and the user needs structured design output before coding.

Do not use this skill as the primary path for:

- pure visual UI exploration
- implementation planning
- codebase orientation without design work

If the request is still fuzzy and the user has not settled the goal, use `brainstorming` first. If the design is already approved and the next step is execution planning, hand off to `writing-plans`.

### 2. Inventory the materials

List the materials before drawing conclusions.

Capture:

- source type
- what it appears to contain
- confidence level
- obvious gaps

Typical source types and reading heuristics are in `references/source-material-patterns.md`.

### 3. Extract facts, then inferences

Separate the output into three buckets while reading:

- `Facts`: explicitly stated by the materials
- `Inferences`: strongly implied but not directly stated
- `Open questions`: required details that are still missing or conflicting

Do not silently upgrade an example into a rule. Repeated patterns are stronger than isolated samples.

### 4. Reconcile conflicting sources

When sources disagree:

- prefer explicit written rules over screenshots or one-off examples
- preserve existing project terminology
- show the conflict instead of hiding it

The goal is a usable design draft, not false certainty.

### 5. Produce the normalized design package

Use the `Full Design Package` structure in `references/output-templates.md`.

The minimum output should cover:

1. Background and goal
2. Source materials used
3. Scope and non-scope
4. Main workflows or use cases
5. Module or responsibility boundaries
6. Interface design needs
7. Domain, data, or solution design needs
8. Risks and unresolved questions
9. Recommended next step

### 6. Route follow-on design work

After producing the normalized draft:

- use `api-contract-designer` when endpoint contracts need depth
- use `domain-solution-designer` when entities, storage, lifecycle, or runtime concerns need depth
- use `writing-plans` only after the design has been reviewed and accepted

## Output Rules

- Prefer concise developer-facing language.
- Keep known facts separate from assumptions.
- Preserve the naming already established by the project materials.
- Stay framework-neutral unless the user or sources require a specific stack.
- Call out missing information early.
- For long Markdown artifacts, optimize for readability before completeness:
  - start with a short `How to Read This Document` section when the file is longer than a few screens
  - add a `Summary` or `Design Overview` section before dense detail
  - group dense facts into short bullet lists or compact tables instead of long paragraphs
  - keep paragraphs short, usually 2 to 4 lines in common desktop Markdown readers
  - add quick navigation cues such as recommended reading order or section purpose
  - avoid opening with only metadata; tell the reader what changed and why it matters first
  - use tables selectively; if a table becomes hard to scan, split it into bullets by theme

## Quick Checklist

- Are the source materials inventoried?
- Are facts and inferences separated?
- Is scope clear?
- Are workflows and module boundaries explicit?
- Are API and domain follow-up areas called out separately?
- Are unresolved questions visible?
