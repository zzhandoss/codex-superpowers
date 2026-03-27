---
name: finish-work
description: Use when implementation and verification are complete and you need to choose how to preserve, merge, hand off, or discard the work safely.
---

# Finish Work

Close out development work with an explicit integration or preservation decision.

This skill exists because finishing work is not just "done" or "not done." The workflow should clearly decide whether the result should be kept, merged, handed off, or discarded, and it should do that only after verification and review are complete enough.

## Core Principle

**Verify first, then choose the finish path explicitly.**

Do not drift from implementation into merge, PR, keep, or discard behavior without stating which finish path is being taken.

<HARD-GATE>
Do NOT finish the work until:
- the current slice or feature has passed its required verification gate;
- review obligations are complete or explicitly waived by an explicit recorded decision;
- for user-facing or UI-heavy work, manual user-facing verification is complete or its absence is explicitly called out;
- the chosen finish path is explicit.
</HARD-GATE>

## Use This Skill When

- a bounded slice or feature is complete and verified;
- you are about to create a PR;
- you are about to merge or preserve the work;
- you are about to discard or archive the work;
- you need to decide what happens next to the completed changes.

## Checklist

You MUST complete these stages in order:

1. **Confirm finish readiness** - verify that the work has passed the required verification and review gates
2. **Check user-facing closeout readiness when relevant** - determine whether the work needs manual user-facing review before true closeout
3. **Identify the current integration surface** - branch, workspace, worktree, or local change state
4. **Determine the base target when relevant** - identify the intended base branch or integration target
5. **Present explicit finish options** - make the available finish paths clear
6. **Execute the chosen path safely** - merge, open PR, keep as-is, or discard with the right safety checks
7. **Apply cleanup policy** - clean up branches, worktrees, or temporary context only when the chosen path calls for it
8. **Report the resulting state** - say what remains, what was cleaned up, and what the next human or workflow action is

## Finish Paths

Support these finish paths when relevant:

- **Merge locally**
  - merge the current work back to the chosen base branch locally
- **Push and create PR**
  - push the branch and create or prepare a pull request
- **Keep as-is**
  - preserve the current branch/workspace/worktree for later
- **Discard**
  - remove the work only with explicit confirmation

Not every environment will use every path, but the finish decision should still be explicit.

## Finish Readiness

Before presenting finish options, confirm:
- required tests or verification have been run fresh;
- review findings are either resolved or intentionally accepted;
- there is no known blocker being hidden under a finish claim.

If finish readiness is not met, do not present finish as if it were available.

For user-facing, visual, or UX-sensitive work, also confirm one of these:
- a manual user-facing verification check was performed and the result is acceptable;
- the work is intentionally being preserved without claiming final user-facing approval;
- the absence of manual user-facing review is explicitly called out in the finish result.

## Safety Rules

- never discard work without explicit confirmation;
- never imply merge-readiness without verification evidence;
- never clean up preserved work accidentally;
- never assume branch or worktree cleanup is always desired.

## Cleanup Policy

Cleanup should depend on the chosen path:

- **merge locally**
  - cleanup may include deleting the finished branch or removing the worktree when safe
- **push and create PR**
  - keep whatever state is needed for the PR flow unless the user wants cleanup
- **keep as-is**
  - preserve the current state intentionally
- **discard**
  - cleanup should happen only after explicit confirmation

## Output

Finish-work may produce:
- a merge action;
- a PR-ready state;
- a preserved branch/workspace state;
- a discarded-and-cleaned-up state;
- a final status summary of what happened.

The final status summary should make user-facing review state explicit when that kind of review matters.

## Boundaries

This skill does not:
- replace verification-before-completion;
- replace code review;
- assume one universal git workflow;
- discard work casually.

## Drift Signals

You are drifting out of this skill if you start:
- presenting finish options before verification is complete;
- treating review as optional without saying so;
- assuming cleanup should always happen;
- discarding work without explicit confirmation;
- claiming the work is merge-ready from intuition instead of evidence.

## Handoff

After the finish path is executed:
- hand off to the next human or workflow step with the resulting state made explicit.

Stop when the work is either merged, PR-ready, intentionally preserved, or explicitly discarded, and the resulting state is clearly reported.
