---
name: multi-session-project-coordinator
description: Use when coordinating multiple existing Codex threads or sessions, or when evaluating a completed development plan to decide whether workload, domain boundaries, risk, or duration justify multi-session division of labor; also use when planning, creating, supervising, polling, or integrating long-lived Codex worker sessions across project worktrees, rounds, approvals, blockers, and safety boundaries.
---

# Multi-Session Project Coordinator

## Overview

Use this skill to act as the coordinator for several Codex sessions that share one project but own different scopes. The coordinator does not replace workers; it verifies their isolation, reads their state, checks outputs, manages round boundaries, and decides whether to dispatch, pause, integrate, or escalate.

This skill complements `dispatching-parallel-agents`: use that skill to create independent workers; use this one to supervise long-lived worker threads across rounds.

## When To Use

Use when the user provides or implies:

- Multiple Codex thread/session IDs or a request to create them.
- Role boundaries such as A/B/C ownership.
- Independent worktrees or a need for data isolation.
- A shared output root, dispatch documents, or round-based delivery.
- Heartbeats, recurring polling, blockers, or cross-checks.

Do not use for a single-thread task, one-off code review, or ordinary subagent execution inside the current session.

## Plan Mode Decision Gate

When in Plan mode, invoke this skill before finalizing a detailed plan if the work may have two or more independent domains. Do not create worker threads or dispatch documents before the development plan exists and the user confirms the collaboration mode.

After the development plan is drafted, evaluate whether multi-session division of labor is warranted:

- Prefer single-session execution when the plan is small, linear, low risk, or dominated by one module.
- Recommend multi-session coordination when the plan has separable domains, long-running work, parallelizable research and implementation, separate frontend/backend/infrastructure tracks, independent worktrees, or review/integration risk.
- State the recommendation and the reason in one short paragraph.
- Ask the user to confirm whether to proceed with multi-session coordination before creating workers, dispatch files, automations, or worktrees.

Use this confirmation prompt, adapting only the first sentence to the project:

```text
我评估这个开发计划后，认为它可以拆成多个长期会话协同推进。是否启用多会话协同模式？
```

If the user accepts, proceed with Worker Creation Preflight and dispatch according to the user's chosen division of labor. If the user declines, proceed with single-session execution and do not create workers.

## Worker Creation Preflight

Before creating or forking workers, verify the project target. Do not trust a saved project name alone.

1. Resolve the intended repository root from the user's path, the current thread cwd, or an existing known-good project thread.
2. Run non-destructive checks in that exact directory: `git -C <path> rev-parse --show-toplevel` and `git -C <path> status --short`.
3. If a saved project points at a non-git directory or the wrong repository, do not create workers from it. Fork a known-good thread that is already attached to the real repository, or ask the user for the correct project target.
4. Prefer detached worktrees for concurrent code work unless the user explicitly requests shared-local execution.
5. If worktree creation returns only a pending id, wait until the actual child thread exists before dispatching.
6. After creation, read each worker thread and verify its cwd and git status before sending scoped work.

Never put two workers in the same checkout for overlapping code changes.

## Required Setup

Before coordinating, identify:

- Worker sessions: ID, label, role, worktree/path, expected output files.
- Shared output root: all coordinator and worker artifacts must go there.
- Round number and current dispatch document.
- Hard boundaries: actions that stop automation and require user confirmation.
- Resume condition: what evidence is required before dispatching the next round.
- Approval posture: whether the user granted automatic non-destructive execution, and which operations still require human confirmation.

If any of these are missing, infer conservatively from local files and thread history; ask the user only when a wrong assumption could cause unsafe work.

## Approval Handling

Thread tools may not expose approval or sandbox settings. When `create_thread` or `fork_thread` has no approval-policy field, do not claim tool-level auto-approval was configured.

Instead, put the user's approval posture in every worker dispatch:

```text
Approval posture: The user authorized automatic execution for routine, non-destructive reads, edits, builds, tests, and local worktree writes in this delegated thread. Do not ask for confirmation for those normal actions. Stop and ask only for destructive git/filesystem operations, production deployment, real secrets or paid external calls, cross-worker scope changes, or changes outside the assigned worktree.
```

If the app or tool schema later exposes an explicit approval-policy parameter, prefer the real tool setting and still include the written approval posture for clarity. If a worker is still blocked by approval prompts, send a narrowly scoped follow-up that repeats the approval posture instead of broadening the task.

Do not edit Codex internal state files to force approval policy changes. Treat app state as diagnostic evidence only. Real approval changes must come from the app UI, supported tool parameters, or an explicit user-approved configuration change.

## Coordination Loop

1. Read each worker thread status and latest output.
2. List expected files in the shared output root.
3. If every worker is still running, write a short status note and do not dispatch.
4. If some workers are complete and others are running, record partial completion and do not interrupt active workers.
5. If all workers are complete, read all expected outputs and cross-check:
   - role boundary compliance
   - required files
   - validation results
   - unsafe claims or actions
   - conflicts between worker outputs
6. If safe and actionable, generate:
   - `ROUND_N_<topic>_CROSS_CHECK_AND_NEXT_PLAN.md`
   - `DEVELOPMENT_ROUND_(N+1)_DISPATCH.md`
7. Send each worker only its own scoped task, with inputs, forbidden areas, validation commands, and exact output path.
8. If work cannot continue without user input, generate the input checklist and pause dispatch.

## Stop Conditions

Stop automatic advancement and write a risk or blocker report if any worker:

- fails, stalls with an error, or omits a required output file
- reports validation failure without an accepted follow-up plan
- crosses role boundaries
- proposes or performs destructive git operations
- creates overwrite or merge conflicts
- reaches a user/environment gate that cannot be solved locally
- leaks or requests secrets, tokens, raw prompts, production payloads, or paid external calls outside the approved scope

Also stop on domain-specific hard boundaries supplied by the user.

## Safety Boundaries Template

For API relay, billing, payment, or production-like systems, default to these boundaries unless the user explicitly replaces them:

- no production launch
- no real production payment funds flow
- no real upstream production keys
- no public registration launch
- no automatic renewal
- no unsupported financial aggregation claims
- no migration-complete claims without evidence
- no new funds ledger unless explicitly approved
- no estimating missing usage or silently charging
- no caching prompts, responses, tool outputs, file context, full keys, upstream keys, or raw payment payloads

Use the user's project-specific boundary wording in generated dispatches.

## Dispatch Prompt Pattern

Each worker prompt should include:

- source coordinator thread ID, if available
- worker label, role, and exact scope
- worker-specific worktree/path
- files to read before designing
- preflight commands: confirm cwd, run `git status --short`, and report unexpected dirty files
- approval posture and stop gates
- forbidden areas and data-safety rules
- required validation commands
- final output path or final response requirements

Never ask a worker to perform another worker's scope. Never ask active workers for new work before the current round completes.

Use this preflight block in every code worker dispatch:

```text
First do:
1. Confirm cwd equals the assigned worktree.
2. Run `git status --short`.
3. Report any unexpected dirty files before editing.
4. Keep all writes inside the assigned worktree unless explicitly told otherwise.
```

## Automation Handling

For heartbeat automations:

- Inspect existing automations before creating a new heartbeat; update a matching heartbeat instead of creating duplicates.
- Include worker thread IDs, labels, worktree paths, current round, stop gates, and latest integration rule in the automation prompt.
- Keep the heartbeat attached to the coordinator thread when the user wants the same conversation to continue managing the project.
- Keep notifications quiet while no user action is needed.
- Notify only when advancing a round, hitting a blocker, needing user input, or stopping automation.
- If automation would keep polling a known user-input blocker, pause or delete it and explain how to resume.
- Do not leave a stale heartbeat running just to restate the same blocker.

## Resuming After User Input

When the user provides environment details or other blockers:

1. Validate that inputs are non-production unless explicitly approved.
2. Redact secrets in docs and chat.
3. Generate a small preflight plan before worker dispatch.
4. Dispatch only the workers whose scopes can make progress.
5. Keep unavailable scopes marked `pending`; do not coerce them into `pass`.

## Integration Gate

Before integrating worker changes into the main checkout:

1. Confirm every worker thread is complete, not merely that files exist on disk.
2. Read each worktree's `git status --short` and diff.
3. Check overlap by file path and domain boundary.
4. Protect the main checkout's dirty worktree; do not overwrite or revert user changes.
5. Run targeted tests first, then broader regression if the changes touch shared contracts.
6. Only commit or push after the integrated tree is verified and the user asked for that step.

## Common Mistakes

- Dispatching the next round while one worker is still `inProgress`.
- Treating a file appearing on disk as completion when the worker thread has not finished.
- Creating workers from an unverified saved project that points to a non-git or wrong directory.
- Assuming `create_thread` configured auto-approval when the tool schema has no approval field.
- Sending work before verifying the child thread's actual cwd and git status.
- Continuing automation after the project is blocked on user-provided environment inputs.
- Letting a worker broaden its role because another worker is idle.
- Writing "passed" for evidence that is only a command template or pending prerequisite.
- Embedding project-specific thread IDs inside reusable instructions.
