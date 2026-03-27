---
name: requesting-code-review
description: Use when a bounded slice, major feature, or merge-ready change should be reviewed before further execution or completion.
---

# Requesting Code Review

Request a focused code review with explicit scope, comparison surface, and review expectations.

This skill exists because review works best when the reviewer receives bounded context instead of vague "please review this" instructions.

## Core Principle

**Request review with explicit scope and evidence, not vague confidence.**

## Use This Skill When

- a bounded execution slice is complete and needs review;
- a major feature is ready for review before moving on;
- delegated work returned and should be reviewed before integration;
- work is approaching merge or completion;
- you want a fresh technical check before continuing.

## Checklist

You MUST complete these stages in order:

1. **Define the review scope** - state exactly what changed and what should be evaluated
2. **Identify the governing inputs** - gather the relevant plan slice, upstream artifacts, and preserved constraints
3. **Identify the comparison surface** - define what commit range, diff, or file scope the reviewer should inspect
4. **State what was verified already** - include fresh verification evidence or say what remains unverified
5. **Request the review explicitly** - ask for findings first, not praise or general impressions
6. **Record the review target** - make it clear whether this is slice review, feature review, or merge-readiness review

## Review Scope Contract

A review request should make these items explicit:
- what was implemented;
- what plan or requirement it was supposed to satisfy;
- what files or diff surface matter;
- what constraints must be preserved;
- what was already verified;
- what kind of review is being requested.

Do not request review with only "look over my changes."

## Review Types

Use the smallest useful review type:

- **Slice review**
  - one bounded execution slice
- **Feature review**
  - several related slices forming one feature
- **Merge-readiness review**
  - final review before completion, PR, or merge

## Reviewer Focus

Default reviewer focus should be:
- correctness bugs;
- behavioral regressions;
- missed requirements;
- architecture drift;
- missing tests or wrong verification;
- placeholder or plan-contract violations.

Do not ask for vague aesthetic commentary unless that is the point of the review.

## Delegated Work

If the reviewed work came from a subagent:
- do not forward the agent's success report as proof;
- provide the actual diff or changed files;
- state what you independently verified before requesting review.

## Output

A review request may produce:
- a review prompt or review handoff;
- explicit review scope notes;
- comparison refs;
- verification notes attached to the review request.

## Boundaries

This skill does not:
- replace verification-before-completion;
- accept review feedback automatically;
- claim success just because review was requested.

## Drift Signals

You are drifting out of this skill if you start:
- requesting review with vague scope;
- asking for review before you know what changed;
- using review as a substitute for verification;
- treating review as performative approval instead of technical evaluation.

## Handoff

After the review request is prepared:
- hand off to the reviewer or review workflow

Stop once the review scope, evidence, and constraints are explicit enough for a focused technical review.
