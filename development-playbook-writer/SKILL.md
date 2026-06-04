---
name: development-playbook-writer
description: Use when a team needs a task-oriented development handbook from PDFs, spreadsheets, requirements docs, design docs, demos, or mixed source materials, including environment setup, task sequencing, execution checkpoints, acceptance evidence, and reference links before detailed implementation planning.
---

# Development Playbook Writer

## Overview

Turn source materials into a practical development handbook that someone can follow task by task before formal implementation planning starts. Favor staged execution, observable acceptance checks, required evidence, and prerequisite references over code-level task breakdowns.

## Workflow

### 1. Check fit

Use this skill when the target artifact is a handbook, runbook, onboarding guide, staged execution guide, or development workbook.

Do not use this skill as the primary path for:

- pure architecture extraction without task sequencing
- deep API contract design
- deep domain or backend solution design
- code-level implementation plans with file-by-file steps

If the materials are still messy, use `design-from-materials` first. If endpoint or domain depth is missing, use `api-contract-designer` or `domain-solution-designer` first. If the handbook is approved and the next step is coding, hand off to `writing-plans`.

### 2. Identify the handbook audience

State who will execute the handbook:

- junior developer or trainee
- feature delivery team
- QA or demo runner
- operator or deployer

The audience determines how much prerequisite explanation, operational caution, and evidence capture the handbook needs.

### 3. Derive the staged path

Group the work into phases such as:

- environment and prerequisites
- project startup or baseline verification
- module-by-module execution tasks
- integration or end-to-end checks
- optional extension or production deployment

Prefer a sequence that can be executed and verified incrementally. Keep optional or advanced paths separate from the minimum delivery path.

### 4. Shape each task as a task card

For each task, capture:

- task title
- goal
- prerequisite state
- concrete actions
- acceptance checks
- required evidence or deliverables
- references or learning materials
- difficulty or effort band
- pitfalls or special notes

If the source materials call for screenshots, logs, exported files, mind maps, diagrams, or links, keep them as explicit evidence requirements rather than burying them in prose.

### 5. Separate playbook work from design work

A playbook may reference architecture or API decisions, but it should not try to replace those artifacts.

Use:

- `design-from-materials` for the normalized design baseline
- `api-contract-designer` for endpoint contract packages
- `domain-solution-designer` for domain, state, storage, and runtime design

Use this skill to turn those results into an execution-ready handbook for humans.

### 6. Produce the playbook package

Use the `Development Playbook Package` structure in `references/playbook-template.md`.

The minimum output should cover:

1. Purpose and audience
2. Source materials used
3. Scope and expected outcome
4. Global prerequisites and environment
5. Phase map or delivery sequence
6. Task catalog
7. Acceptance and evidence expectations
8. Optional extension or production path
9. Risks, missing materials, and open questions

## Output Rules

- Preserve the project terminology, tool names, and artifact names found in the materials.
- Make every acceptance check observable.
- Keep task order explicit when sequencing matters.
- Distinguish required references from optional learning links.
- Keep the handbook technology-aware but not stack-locked unless the materials require it.
- Leave missing assets, contradictions, or hidden assumptions visible.
- Stop short of file-by-file coding steps unless the user explicitly asks for a full implementation plan.
- For long Markdown handbooks, design for fast reading:
  - begin with `How to Read`, `Quick Start`, or `Playbook Summary` before detailed phases
  - provide recommended reading order for different audiences when the document serves multiple roles
  - keep paragraphs short and convert dense procedure blocks into bullets or numbered steps
  - add quick-reference sections for common commands, paths, accounts, or decision points
  - avoid front-loading the file with metadata only; explain the practical value of the document first
  - prefer multiple compact sections over a few oversized sections

## Quick Checklist

- Is the intended audience explicit?
- Is environment setup separated from feature execution tasks?
- Does each task include goal, actions, acceptance, and evidence?
- Are required versus optional references marked clearly?
- Are stretch tasks or production tasks separated from the must-do path?
- Does the output remain a handbook rather than a code-level plan?
