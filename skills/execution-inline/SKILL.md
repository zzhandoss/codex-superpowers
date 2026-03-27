---
name: execution-inline
description: Use when the main orchestrator should execute a planned slice locally instead of delegating it to subagents.
---

# Execution Inline

Execute a bounded planned slice locally while preserving the planning contract, placeholders, architectural constraints, and UI/UX constraints.

Use this skill when the main orchestrator should keep direct control of implementation instead of delegating to subagents.

## Core Principle

**Execute one bounded slice at a time, from the current plan, without silently re-planning the system.**

This skill exists because not every planned slice should be delegated. Some work is better executed directly by the main orchestrator, especially when the work is foundational, tightly coupled, or still sensitive to context drift.

<HARD-GATE>
Do NOT start implementation until you have:
- a current planning artifact for the slice you are executing;
- the upstream design / engineering / UI/UX inputs that the plan depends on;
- placeholder status that makes execution honest for this slice, with blocking items either resolved or explicitly accepted as non-blocking for this exact slice.
</HARD-GATE>

## Use This Skill When

- the slice is small or tightly coupled enough that delegation would add coordination cost;
- the work sits on the critical path and waiting on a subagent would slow progress;
- the slice touches greenfield foundation or baseline project structure;
- the slice depends heavily on current local context and recent changes;
- approvals, environment setup, or tool behavior make delegation materially worse than local execution for this bounded slice.

## Do Not Use This Skill When

- the work is clearly bounded and safely delegable;
- multiple independent slices can be executed in parallel without overlapping ownership;
- the main orchestrator would become a bottleneck by doing all the work directly.

## Checklist

You MUST complete these stages in order:

1. **Load the current plan slice** - read the relevant execution or workstream plan and the upstream artifacts it depends on
2. **Check execution readiness** - confirm placeholders, blockers, and consumed seams still allow honest execution
3. **Confirm ownership** - verify that this slice should stay with the main orchestrator
4. **Restate preserved constraints** - make visible what architecture, UI/UX, and planning rules must survive the code changes
5. **Execute the bounded slice** - implement only the planned slice, without widening scope casually
6. **Verify the slice** - run fit-for-purpose automated and manual checks from the plan
7. **Record execution reality** - note deviations, newly discovered seams, placeholder changes, and plan drift
8. **Resync if needed** - if execution changed future work, update the plan or hand off back to planning instead of hiding the drift
9. **Hand off cleanly** - stop when the bounded slice is complete and the next stage is clear

## Greenfield Foundation Rule

If the project is new and the work establishes the initial repo, app, package, or baseline architectural structure:
- the main orchestrator owns that work by default;
- do not delegate that foundation work to a subagent unless there is a strong reason and the risk is explicitly accepted.

## Execution Readiness

Before executing, confirm:
- the plan level is appropriate for execution;
- unresolved placeholders do not block this slice, or are explicitly classified as non-blocking for this slice;
- consumed upstream seams actually exist or are explicitly acknowledged as missing;
- the slice still fits the current repo reality.

If any of these checks fail, do not improvise around them. Resync with planning or placeholder handling first.

## Preserved Constraints

Always keep these visible while executing:
- architecture and dependency rules from `engineering-design`
- UI/UX structure and continuity constraints from `ui-ux-design`
- must-use tools and libraries from the plan
- placeholder boundaries and unresolved blockers
- workstream and execution slice boundaries from the planning artifact

## Plan Drift

If execution reveals new reality, classify it:

- **local execution detail**
  - no plan change needed
- **slice-level drift**
  - update the current execution artifact or handoff notes
- **future-plan impact**
  - update the relevant workstream or initiative plan
- **upstream contradiction**
  - stop and return to planning or engineering/UI/UX design instead of silently overriding earlier stages

## Verification

Use fit-for-purpose verification from the plan:
- automated tests
- smoke checks
- manual verification
- observability checks when runtime behavior changed

Do not claim completion without recording what was actually verified.

## Output

Execution-inline may produce:
- code changes
- test updates
- implementation notes
- plan resync notes when needed

If execution drift changes later work, record that explicitly instead of burying it in a generic summary.

## Boundaries

This skill does not:
- rewrite the planning model from scratch
- silently consume blocking placeholders
- widen scope across unrelated workstreams
- delegate foundational work by default

If the slice stops being well-bounded, stop and return to planning or hand off intentionally.

## Drift Signals

You are drifting out of this skill if you start:
- implementing beyond the selected slice
- casually changing future work without updating plans
- treating blocking placeholders as ignorable
- rewriting architecture locally instead of escalating
- doing coordination work that should belong to subagent execution or planning

## Handoff

After the slice is complete:
- hand off to the next execution slice, verification step, or plan-resync step

Stop when the current bounded slice is implemented, verified, and reconciled with the plan.
