---
name: receiving-code-review
description: Use when receiving code review feedback before implementing suggestions, especially when the feedback may be unclear, incomplete, or in tension with current plans and constraints.
---

# Receiving Code Review

Process review feedback with technical rigor instead of blind agreement.

This skill exists because review comments are inputs to evaluate, not orders to follow without verification.

## Core Principle

**Verify feedback before implementing it.**

Correct feedback should be applied. Wrong, unclear, or context-missing feedback should be questioned, clarified, or pushed back on with technical reasoning.

## Checklist

You MUST complete these stages in order:

1. **Read the full review** - do not respond to isolated comments without understanding the whole set
2. **Classify each item** - blocking, important, minor, unclear, or questionable
3. **Restate the technical issue** - make sure you understand what the reviewer is actually claiming
4. **Check against code and workflow reality** - compare feedback against the plan, upstream constraints, placeholders, tests, and current code
5. **Clarify before acting if needed** - if any item is unclear, stop and ask before implementing partial guesses
6. **Apply one item at a time** - do not batch confusing review items into one uncontrolled patch
7. **Reverify after changes** - rerun the proving checks for the updated claim
8. **Record the outcome honestly** - fixed, rejected with reasoning, deferred, or still unclear

## Feedback Classification

Classify review items explicitly:
- **blocking**
  - correctness, security, broken requirement, major regression
- **important**
  - should be fixed before continuing
- **minor**
  - safe to defer if appropriate
- **unclear**
  - cannot be implemented until clarified
- **questionable**
  - may be wrong for this codebase or conflict with existing constraints

## Verification Against Reality

Before implementing review feedback, check:
- does it match the actual code?
- does it match the current plan or requirement?
- does it preserve engineering and UI/UX constraints?
- does it conflict with placeholders or deferred decisions?
- would it break working behavior or widen scope?

Do not implement feedback just because it sounds professional.

## Pushback

Push back when:
- the reviewer is wrong technically;
- the feedback conflicts with the current plan or preserved constraints;
- the suggested fix would create scope drift;
- the item cannot be verified from current code or requirements.

Push back with technical reasoning, not emotion.

## Clarification Rule

If some items are unclear:
- do not implement only the subset you understand if the unclear items could affect the same area;
- ask for clarification first.

Partial understanding often produces wrong fixes.

## Applying Feedback

Apply review feedback one item or tightly related cluster at a time.

After each meaningful fix:
- rerun the relevant verification;
- update status honestly;
- keep later work aligned with the plan.

If the review reveals planning drift, return to planning rather than hiding the change in a patch.

## Output

Receiving-code-review may produce:
- clarified review questions;
- implemented review fixes;
- reasoned pushback notes;
- plan resync notes if the review exposed drift.

## Boundaries

This skill does not:
- blindly accept review feedback;
- replace verification-before-completion;
- turn review into a social performance exercise.

## Drift Signals

You are drifting out of this skill if you start:
- agreeing before checking;
- implementing unclear items without clarification;
- batching many review items into one uncontrolled fix;
- accepting feedback that conflicts with known constraints without escalation;
- using gratitude or approval language instead of technical response and action.

## Handoff

After review feedback is processed:
- hand off back to execution, verification, or planning as appropriate

Stop when each review item is either fixed, explicitly deferred, clarified, or rejected with technical reasoning.
