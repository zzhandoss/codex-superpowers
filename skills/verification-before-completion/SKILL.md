---
name: verification-before-completion
description: Use before claiming a fix, task, slice, feature, or implementation is complete, passing, or ready to hand off.
---

# Verification Before Completion

Do not claim success without fresh verification evidence.

This skill exists because unverified success claims break trust, hide regressions, and create fake progress.

## Core Principle

**Evidence before claims.**

If you have not run the verification that proves the claim you are about to make, you cannot honestly make that claim.

<HARD-GATE>
Do NOT claim that work is:
- complete;
- fixed;
- passing;
- ready to merge;
- ready to hand off;
- ready to close

until you have run fresh verification evidence for that exact claim.
</HARD-GATE>

## Use This Skill When

- you are about to say a task is done;
- you are about to say a bug is fixed;
- you are about to say tests pass;
- you are about to hand work to the next workflow stage;
- you are about to commit, open a PR, merge, or close out a slice.

## Checklist

You MUST complete these stages in order:

1. **Identify the claim** - state exactly what you are about to claim
2. **Identify the proving verification** - decide what command, check, or manual validation actually proves that claim
3. **Run the verification fresh** - do not rely on old output or assumptions
4. **Read the result fully** - check exit status, failures, warnings, and missing checks
5. **Compare result to claim** - confirm whether the evidence truly supports the claim
6. **State the real status** - report success only if the evidence supports it; otherwise state the actual outcome

## Claim Types

Different claims require different evidence.

Examples:
- `tests pass`
  - requires the relevant test command to pass now
- `bug fixed`
  - requires the original reproduction or failing test to pass now
- `slice complete`
  - requires the planned verification for that slice, not just code changes
- `ready for review`
  - requires the implementation state to match the plan and verification expectations
- `ready to merge`
  - requires the merge-ready verification gate, not just local optimism

Do not substitute a nearby signal for the real one.

## Fresh Means Fresh

Fresh verification means:
- run in this completion attempt;
- for this exact code state;
- for this exact claim.

Do not use:
- a previous run from earlier in the conversation;
- a partial run for a broader claim;
- "it should still pass";
- "the agent said it passed".

## Delegation and Review

If another agent reported success:
- verify independently before repeating the claim.

If code review feedback was applied:
- rerun the verification needed for the updated claim.

Do not convert reported success into claimed success without evidence.

## Manual Verification

If the plan requires manual verification:
- run the manual checks fresh;
- record what was checked;
- do not replace required manual verification with a vague statement like "looks good."

## Output

When reporting status, include:
- what was verified;
- what evidence was run;
- what the result actually was;
- what remains unverified, if anything.

If verification failed or was incomplete, say so plainly.

## Boundaries

This skill does not:
- decide what to build;
- replace debugging;
- replace planning;
- waive verification because the work feels simple.

## Drift Signals

You are drifting out of this skill if you start:
- saying "should pass" or "seems fixed";
- claiming completion from code inspection alone;
- trusting agent reports without rerunning proof;
- skipping manual verification that the plan required;
- making merge or handoff claims from partial evidence.

## Handoff

After verification is complete:
- hand off to the next workflow stage only if the evidence supports the claim

Otherwise:
- report the real status;
- return to debugging, execution, or planning as appropriate.
