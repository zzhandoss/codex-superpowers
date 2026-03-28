---
name: engineering-design
description: Use after brainstorming and before implementation planning when a design doc needs engineering decisions, constraints, deferred decisions, and implementation-facing structure.
---

# Engineering Design

## Overview

Turn a design doc into an engineering design doc that acts as an engineering contract for later planning.

This skill exists because a good product/design spec is not yet an implementation-ready engineering contract.

Use this skill to decide and document:
- technologies and libraries;
- architectural style, structural principles, and important patterns when they materially shape implementation;
- package/module/service structure;
- dependency rules, ownership boundaries, and extension seams;
- delivery and environment assumptions;
- observability expectations;
- testing strategy by area;
- explicit assumptions, risks, non-goals, and tradeoffs;
- deferred engineering decisions.

## Core Principle

**Do engineering concretization before implementation planning.**

Do not jump directly from design doc to execution planning if key engineering decisions are still implicit.

The output of this skill must reduce ambiguity for planning without turning into a task plan.
This skill is approval-driven. Do not silently decide the full engineering shape and drop a finished document without explicit user confirmation of the important steps.

<HARD-GATE>
Do NOT invoke `writing-plans`, write an implementation plan, break work into executable tasks, or take implementation action until you have produced an engineering design artifact that is sufficient input for later planning.
</HARD-GATE>

## Checklist

You MUST complete these stages in order:

1. **Inspect design input and workspace reality** - read the design doc, inspect repo structure, config, adjacent docs, and local conventions
2. **Identify engineering gaps** - list the engineering decisions that are still implicit, missing, conflicting, or risky
3. **Show the engineering gap packet** - present the open engineering questions, likely decision groups, and any important unknowns before finalizing them
4. **Get approval to proceed on those groups** - let the user approve step-by-step or as a related batch before locking decisions into the artifact
5. **Resolve what can be resolved now** - choose technologies, boundaries, delivery assumptions, observability expectations, and testing policy where enough context exists
6. **Show the proposed engineering decisions** - surface the proposed choices, rationale, and provisional/deferred areas before writing the final document
7. **Get approval on the proposed decisions** - do not silently self-approve the final engineering shape
8. **Formalize deferred decisions** - create or reference placeholders for unresolved questions instead of writing vague `TBD` text
9. **Write the engineering design artifact** - save it to the default path unless the user prefers a different location
10. **Engineering design self-review** - check the engineering document against the approved design doc and fix drift inline
11. **Hand off cleanly** - stop at an engineering contract and hand off to later workflow stages without taking them over

When several decisions naturally belong together, batch them and ask for approval as one packet instead of interrupting every sentence.
Do not force needless micro-approvals, but do not skip explicit user approval for the main engineering decisions either.

## Inputs

Read:
- the design/spec from `brainstorming`;
- relevant project context such as repo structure, package layout, config, adjacent docs, and existing conventions;
- user preferences for tools and frameworks;
- existing repo conventions and constraints.

Ground decisions in workspace reality:
- inspect the current repo structure, package layout, config, and adjacent docs;
- preserve local patterns unless there is a clear reason to change them;
- if design intent conflicts with repo reality or user preferences, call that out explicitly.

## Output

Write:
- `docs/superpowers/engineering/YYYY-MM-DD-<topic>-engineering-design.md`

This document is a planning input, not an implementation plan.
User preference may override the default path, but the skill should still use a clear file name and stable location.

## The Document Must Cover

1. Purpose and scope
2. Engineering goals
3. Non-goals
4. Assumptions
5. Major technical decisions with status: chosen, provisional, or deferred
6. Required technologies and libraries
7. Architectural style, structural principles, and pattern-level decisions that materially constrain implementation
8. Repo/package/module/service boundaries
9. Dependency rules, ownership boundaries, and extension seams
10. Data/auth/validation/logging choices
11. Delivery and environment assumptions
12. Observability expectations
13. Testing policy by area
14. Risks, tradeoffs, and important rejected alternatives
15. Deferred decisions via placeholder IDs
16. Constraints that implementation planning must preserve
17. Planning-input summary for later `writing-plans`

## Decision Quality

For every meaningful engineering decision:
- state the chosen option;
- state whether the decision is chosen, provisional, or deferred;
- give the rationale;
- note important rejected alternatives when useful;
- make tradeoffs explicit;
- make constraints visible to later planning.

Do not hide uncertainty behind vague wording.

Use pattern-level guidance only when it materially changes later implementation shape.

Good examples include:
- dependency inversion or layering rules
- plugin/adapter/strategy/factory style extension seams
- where composition should happen versus where concrete implementation should stay isolated
- domain or service boundaries that later planning must preserve

Do not fill the document with generic pattern advice detached from the actual work.

## Approval-Driven Behavior

Before writing or substantially rewriting the engineering design artifact:
- show the user the current engineering gap packet or proposed decision packet;
- make it clear which decisions are:
  - ready to lock
  - still provisional
  - better deferred into placeholders;
- wait for explicit user approval of the current step or related batch of steps.

Good approval checkpoints include:
- the grouped engineering gaps that still need choices
- the proposed stack and major technical direction
- the architectural structure and boundary rules
- the deferred-decision set and placeholder plan

Do not treat silence, your own preference, or momentum as approval.
Do not write the final document as if those decisions were already approved when they were not.

## Deferred Decisions

If an engineering question cannot be answered yet:
- do not write `TBD`;
- create or reference a formal placeholder;
- use a formal placeholder ID;
- make the blocking level explicit;
- label whether the placeholder is blocking or safe to carry forward;
- explain why the decision is deferred;
- state what stage it blocks, if any;
- state the trigger for resolution.

Deferred decisions are allowed here if they are formalized clearly and do not pretend to be resolved.

Do not allow unresolved sections to drift into generic placeholders, vague prose, or implicit future work.

When placeholders are present, keep them centralized in a clear `Open Questions and Placeholders` section instead of scattering them unpredictably across the document.

## Planning Input Shape

The engineering design artifact should be easy for `writing-plans` to consume later.

Make sure the document makes these items easy to extract:
- must-use libraries and technical choices;
- architectural principles and pattern-level constraints that later work must preserve;
- provisional decisions that may need reconfirmation before execution;
- deferred decisions and their placeholder IDs;
- repo and boundary rules that planning must preserve;
- delivery, observability, and testing obligations that later plans must carry forward.

## Engineering Design Self-Review

After writing the engineering design artifact, review it with fresh eyes against the approved design doc:

1. **Design alignment check** - does the engineering document preserve the approved product/design intent?
2. **Drift check** - did engineering choices quietly change scope, user flows, or core behavior without being called out?
3. **Constraint check** - are the engineering constraints explicit and compatible with the design doc?
4. **Architecture-shaping check** - did the document capture the structural principles, dependency rules, and pattern-level decisions that materially affect implementation?
5. **Placeholder check** - are all unresolved decisions formalized with placeholder IDs instead of vague prose?
6. **Planning-input check** - is the document easy for `writing-plans` to consume, or did it drift into a free-form essay?
7. **Boundary check** - did the document drift into planning, implementation steps, or execution ordering?

Fix issues inline before handing off.

## Boundaries

This skill does not:
- decompose work into implementation tasks;
- define execution order;
- prescribe low-level implementation steps;
- simulate `writing-plans`;
- write production code.

If planning or implementation detail starts to dominate, stop and hand off instead of expanding this skill's scope.

## Drift Signals

You are drifting out of this skill if you start:
- breaking work into executable tasks;
- prescribing command-by-command implementation;
- writing like a planner instead of an engineering decision layer;
- leaving unresolved areas without formal placeholders;
- giving abstract architecture advice that is not grounded in the workspace;
- talking about downstream stages as if this skill owns them.

## Handoff

After the engineering design doc is complete:
- hand off to `ui-ux-design` if the work needs explicit UI/UX flow, screen, or mockup design;
- hand off to `writing-plans` when planning-ready engineering inputs are in place.

For user-facing work, do not treat `ui-ux-design` as optional just because engineering decisions are already documented.
If flows, screens, states, shell rules, or visual/tooling direction are still implicit, hand off to `ui-ux-design` before `writing-plans`.

Mention downstream stages only as handoff targets. Do not implicitly orchestrate them from inside this skill.
Stop when the engineering design artifact is sufficient input for later planning.
