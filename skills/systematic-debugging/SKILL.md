---
name: systematic-debugging
description: Use when facing a bug, failure, regression, flaky behavior, or unexpected runtime outcome before proposing fixes or patches.
---

# Systematic Debugging

Investigate technical problems systematically before attempting fixes.

This skill exists because random fixes, stacked guesses, and symptom patches waste time and create new bugs.

## Core Principle

**No fixes without root cause investigation first.**

Do not treat debugging as "try changes until something works." The goal is to locate the real failure point, understand why it happens, and only then choose the smallest valid fix.

<HARD-GATE>
Do NOT propose or implement fixes until you have:
- a reproducible symptom or concrete evidence trail;
- a clear understanding of the failing boundary, component, or data flow;
- at least one explicit root-cause hypothesis grounded in evidence.
</HARD-GATE>

## Use This Skill When

- a test fails;
- a bug is reported;
- behavior is unexpected or inconsistent;
- a build or integration step breaks;
- performance or runtime behavior degrades;
- a prior fix did not work;
- the issue feels "obvious" and you are tempted to patch it quickly.

## Do Not Use This Skill When

- you are not debugging a failure at all;
- the work is purely greenfield feature delivery with no failing behavior to explain.

## Checklist

You MUST complete these stages in order:

1. **Define the symptom** - state what is failing, where, and how it appears
2. **Reproduce or gather evidence** - make the failure concrete, repeatable, or at least observable
3. **Inspect recent change surface** - identify what changed that could plausibly explain the issue
4. **Trace the failing boundary** - follow the data, state, or control flow until you find where expectation diverges from reality
5. **Compare against working references** - find similar working code, flows, or cases and identify the meaningful differences
6. **Form an explicit root-cause hypothesis** - state what you think is actually broken and why
7. **Test the hypothesis minimally** - validate the hypothesis with the smallest possible check or change
8. **Only then choose the fix path** - fix the root cause, not the symptom
9. **Verify the fix** - confirm the original issue is resolved and regressions are not introduced

## Symptom Definition

Make the failure explicit:
- what failed;
- where it failed;
- what the expected behavior was;
- what the actual behavior was;
- how often it reproduces.

If the symptom is still vague, do not guess. Gather more evidence first.

## Evidence Gathering

Prefer concrete evidence over intuition:
- error messages
- stack traces
- failing tests
- runtime logs
- network or API responses
- screenshots or visible UI behavior
- repo diffs and recent changes

For multi-component systems, inspect each boundary instead of assuming the failure location:
- client -> API
- API -> service
- service -> database
- workflow -> script -> runtime

## Root-Cause Tracing

When the error appears deep in the stack:
- follow the bad value, event, or state backward;
- identify where it first becomes wrong;
- keep tracing until you find the originating boundary;
- fix there, not at the final symptom site.

## Working Reference Comparison

Find one or more working references:
- nearby working code in the repo
- another working test or flow
- a similar module using the same pattern

Then identify:
- what is the same;
- what is different;
- which differences are plausible root-cause candidates.

Do not wave away small differences without checking them.

## Hypothesis Discipline

State the debugging hypothesis explicitly:

- "I think X is the root cause because Y evidence points to it."

Then test that hypothesis with the smallest possible probe.

Do not:
- stack multiple unrelated fixes;
- patch several layers at once;
- keep retrying the same idea with no new evidence.

## If Repeated Fixes Fail

If multiple attempted fixes fail:
- stop escalating patch complexity;
- question whether the architecture, interface contract, or plan assumption is wrong;
- return to planning or engineering-design if the issue is not local anymore.

Repeated failed fixes are often evidence of a bad model of the problem, not bad luck.

## Fit With Planning and Placeholders

Debugging may reveal:
- a local implementation defect;
- a bad execution seam;
- a wrong planning assumption;
- a missing or newly needed placeholder;
- an upstream contradiction in engineering-design or UI/UX design.

Classify the outcome explicitly:
- `local bug`
- `execution-plan drift`
- `workstream-plan drift`
- `upstream design contradiction`

If the issue changes future work, resync planning instead of burying it inside the fix.

## Verification

After fixing:
- rerun the failing test or reproduction path fresh;
- run any nearby regression checks that prove the fix did not only move the bug;
- report what evidence now passes.

Do not claim success without fresh verification evidence.

## Output

Systematic debugging may produce:
- root-cause notes;
- instrumentation or evidence notes;
- a bounded fix;
- plan resync notes if the issue exposed planning drift.

## Boundaries

This skill does not:
- skip directly to patching;
- treat evidence gathering as optional;
- hide architecture or planning problems inside local fixes;
- claim success without verification.

## Drift Signals

You are drifting out of this skill if you start:
- proposing fixes before locating the failing boundary;
- changing multiple things at once without a hypothesis;
- calling something "probably fixed" without fresh verification;
- treating repeated failed fixes as a reason to try bigger guesses;
- ignoring evidence that the problem is actually upstream.

## Handoff

After root cause is identified and the bounded fix is verified:
- hand off back to execution if the issue was local;
- hand off to planning or design layers if the issue exposed upstream drift.

Stop when the real cause is understood, the outcome is verified, and any workflow impact is made explicit.
