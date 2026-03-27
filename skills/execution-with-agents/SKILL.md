---
name: execution-with-agents
description: Use when a planned slice is ready for bounded subagent execution with explicit ownership and orchestration.
---

# Execution With Agents

Execute planned work through bounded subagent delegation while preserving the planning contract, ownership boundaries, placeholders, and orchestration clarity.

Use this skill when the work is worth delegating and can be given to subagents without losing control of architecture, planning, or scope.

## Core Principle

**Delegate bounded slices, not vague goals.**

This skill exists because subagents are useful only when the work is clearly scoped, ownership is explicit, and the main orchestrator keeps control of plan integrity.

<HARD-GATE>
Do NOT delegate a slice until:
- the plan level is appropriate for delegation;
- ownership boundaries are explicit;
- unresolved blocking placeholders are handled honestly;
- the main orchestrator has decided that delegation is better than inline execution.
</HARD-GATE>

## Use This Skill When

- the slice is bounded enough for a clean ownership handoff;
- multiple independent slices can move in parallel;
- a sidecar review, research, or implementation task can run without blocking the main orchestrator's next step;
- the code changes belong to a disjoint file/package/module area.

## Do Not Use This Skill When

- the work establishes greenfield foundation or baseline architectural structure;
- the slice is too coupled or ambiguous to hand off safely;
- the next step depends immediately on the result and delegation would only add latency;
- ownership boundaries are unclear.

## Checklist

You MUST complete these stages in order:

1. **Load the current plan slice** - read the relevant execution or workstream plan and the upstream artifacts it depends on
2. **Decide local versus delegated execution** - choose delegation only if it clearly helps
3. **Check delegation readiness** - confirm placeholders, blockers, consumed seams, and ownership boundaries allow honest delegation
4. **Build the delegation context** - package the exact planning, upstream, placeholder, seam, and verification context the subagent needs
5. **Assign explicit ownership** - define the file/package/module scope the subagent owns
6. **Delegate the bounded slice** - hand off the narrow task, preserved constraints, verification expectations, and stop conditions
7. **Keep the orchestrator on orchestration** - do not duplicate delegated work locally
8. **Review the result** - verify that returned work respects the plan, boundaries, and placeholders
9. **Resync if needed** - update plans or placeholder state when delegated work changes future execution
10. **Close the agent** - if the task is done and the context is no longer needed, close the subagent immediately

## Delegation Readiness

Before delegating, confirm:
- the slice is execution-ready for that ownership area;
- blocking placeholders do not invalidate the delegated work;
- consumed upstream seams exist or are explicitly acknowledged;
- the delegated scope does not overlap dangerously with other active work.

If these conditions do not hold, keep the work local or return to planning.

## Delegation Context Contract

Before spawning or messaging a subagent, build a structured context package that includes:
- the current plan slice being executed;
- the relevant upstream artifacts the slice depends on;
- preserved architecture and UI/UX constraints;
- must-use tools/libraries;
- consumed upstream seams the slice assumes;
- placeholder IDs and their status at this slice;
- exact ownership boundaries;
- required verification;
- explicit stop conditions and escalation conditions.

Do not assume the subagent will reconstruct this context correctly from a vague prompt.

The context package should make these items obvious:
- what the slice is;
- why it is bounded;
- where the subagent may write;
- what it must preserve;
- what it must not touch;
- what blocks the work;
- what to report back.

## Ownership Contract

Every delegated slice should state:
- owned files/packages/modules;
- what must not be changed;
- the exact upstream artifacts and plan slice the work is based on;
- must-preserve constraints;
- consumed seams and assumptions;
- placeholder IDs with their current status;
- required tools/libraries;
- required tests/checks;
- what to do if the slice hits a blocker;
- what completion should look like.

Do not delegate "implement feature X" without this structure.

## Greenfield Foundation Rule

Do not delegate initial repo/app/package/baseline architecture work by default.

If the project is greenfield:
- the main orchestrator should create the initial foundation;
- subagents may work only after the baseline is established and the ownership zones are stable.

## Placeholder Rules

Subagents must not be asked to work through unresolved blocking placeholders as if they were solved.

When placeholders are relevant:
- include the placeholder ID in the delegated task;
- state whether it is advisory, carry-forward, or blocking for that slice;
- keep the main orchestrator responsible for resolving or escalating blocker changes.

## Review and Integration

When delegated work returns:
- check whether it stayed within ownership;
- check whether it preserved architecture and UI/UX constraints;
- check whether it changed later plan assumptions;
- check whether new placeholders or seams were discovered.

If it changed future work, resync planning before continuing blindly.

## Output

Execution-with-agents may produce:
- delegated code changes;
- delegated verification results;
- review notes;
- plan resync notes.

The main orchestrator remains responsible for final integration and workflow integrity.

## Boundaries

This skill does not:
- turn every slice into delegation by default;
- offload greenfield foundation carelessly;
- allow subagents to redefine plans or upstream design silently;
- leave finished agents open without reason.

## Drift Signals

You are drifting out of this skill if you start:
- delegating vague or overlapping work;
- using subagents to avoid making orchestration decisions;
- letting subagents work past blocking placeholders;
- sending weak context that forces the subagent to guess critical constraints;
- keeping finished agents alive without value;
- redoing delegated work locally instead of integrating it.

## Handoff

After delegated work is reviewed and integrated:
- hand off to the next execution slice, next agent task, or plan-resync step.

Stop when the delegated slice is complete, reconciled with the plan, and no longer needs an active subagent context.
