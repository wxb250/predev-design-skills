---
name: multi-session-project-coordinator
description: Use when coordinating multiple existing Codex threads or sessions, or when planning a project that may need long-lived multi-session collaboration, round dispatch, cross-checks, blockers, or automation management.
---

# Multi-Session Project Coordinator

## Overview

Use this skill to act as a main coordinator for several already-running Codex sessions that share one project but own different domains. The coordinator does not replace domain workers; it reads their state, checks their outputs, manages round boundaries, and decides whether to dispatch, pause, or escalate.

This skill complements `dispatching-parallel-agents`: use that skill for creating independent worker tasks; use this one for supervising existing long-lived threads across rounds.

## When To Use

Use when the user provides or implies:

- A Plan mode project design or implementation planning request that may benefit from multiple long-lived sessions.
- Multiple Codex thread/session IDs.
- Role boundaries such as A/B/C ownership.
- A shared output directory.
- Recurring coordination, heartbeats, or status polling.
- Cross-checks before the next round.
- Safety boundaries or blocker gates.

Do not use for a single-thread task, one-off code review, or ordinary subagent execution inside the current session.

## Plan Mode Decision Gate

When in Plan mode, invoke this skill before writing the detailed plan if the work appears to have two or more independent domains, such as frontend/backend/payment/deployment, research/design/implementation, or multiple worktrees.

Before creating worker threads or dispatch documents, ask the user whether to use multi-session coordinated development. Keep the question short:

```text
这个任务可以拆成多个长期会话协同推进。是否启用多会话协同模式？
```

If Plan mode provides a structured user-input tool, use it for this one decision. Recommend multi-session coordination only when it reduces conflict or speeds independent work; otherwise recommend single-session execution.

If the user chooses multi-session coordination, continue with the setup checklist below. If the user declines, proceed with the normal single-session planning workflow and do not create worker threads.

## Required Setup

Before coordinating, identify:

- Worker sessions: ID, label, role, worktree/path, expected output files.
- Shared output root: all coordinator and worker artifacts must go there.
- Round number and current dispatch document.
- Hard boundaries: actions that must stop automation and require user confirmation.
- Resume condition: what evidence is required before dispatching the next round.

If any of these are missing, infer conservatively from local files and thread history; ask the user only when a wrong assumption could cause unsafe work.

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
   - `ROUND_N_...CROSS_CHECK_AND_NEXT_PLAN.md`
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

## Output Pattern

Keep coordinator files predictable:

```text
ROUND_N_<topic>_CROSS_CHECK_AND_NEXT_PLAN.md
DEVELOPMENT_ROUND_(N+1)_DISPATCH.md
USER_<topic>_INPUT_REQUIRED.md
AUTOMATION_<id>_HEARTBEAT_<timestamp>_STATUS.md
AUTOMATION_<id>_..._PAUSED_OR_DELETED.md
RISK_REPORT_<timestamp>.md
```

For worker outputs, preserve the user's naming pattern:

```text
SESSION_A_ROUND_N_<topic>.md
SESSION_B_ROUND_N_<topic>.md
SESSION_C_ROUND_N_<topic>.md
```

## Dispatch Prompt Pattern

Each worker prompt should include:

- source coordinator thread ID, if available
- files to read
- worker-specific worktree/path
- exact section of the dispatch document to execute
- round goal
- forbidden areas
- required validation commands
- final output path

Never ask a worker to perform another worker's scope. Never ask active workers for new work before the current round completes.

## Automation Handling

For heartbeat automations:

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

## Common Mistakes

- Dispatching the next round while one worker is still `inProgress`.
- Treating a file appearing on disk as completion when the worker thread has not finished.
- Continuing automation after the project is blocked on user-provided environment inputs.
- Letting a worker broaden its role because another worker is idle.
- Writing “passed” for evidence that is only a command template or pending prerequisite.
- Embedding project-specific thread IDs inside reusable instructions.
