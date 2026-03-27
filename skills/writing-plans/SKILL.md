---
name: writing-plans
description: Use after design, engineering, and UI/UX inputs are approved to create planning artifacts for later execution without jumping into implementation.
---

# Writing Plans

Turn approved upstream artifacts into planning artifacts that later execution can follow without re-deciding the work from scratch.

This skill exists because even good design, engineering, and UI/UX artifacts are still not the same as a usable implementation plan.

## Core Principle

**Plan at the right level, with the right inputs, before implementation.**

Do not jump from approved inputs directly into code. Do not always write one giant low-level execution script either.

The output of this skill must reduce ambiguity for execution without collapsing into implementation.

<HARD-GATE>
Do NOT write production code, execute implementation work, or force execution-level detail until the correct planning level and upstream inputs are clear.
</HARD-GATE>

## Checklist

You MUST complete these stages in order:

1. **Inspect approved upstream artifacts** - read the approved design input, engineering design artifact, UI/UX design artifact when relevant, and referenced placeholders
2. **Run a scope check** - if the request still mixes multiple independent subsystems or incompatible scopes, stop and split the work before planning deeply
3. **Determine the plan level** - decide whether the work needs initiative-level, workstream-level, or execution-level planning
4. **Extract planning inputs** - identify constraints, dependencies, must-use tools/libraries, placeholders, unresolved blockers, and verification expectations
5. **Map file/package/module structure when needed** - make decomposition and ownership boundaries explicit before writing deeper tasks
6. **Shape workstream-level implementation approach when needed** - for bounded workstreams, capture the domain-specific architecture, structure, and implementation approach that execution must preserve
7. **Decompose at the correct level** - break the work into workstreams or tasks appropriate to the selected plan level
8. **Write the planning artifact** - save it to the default path unless the user prefers a different location
9. **Plan self-review** - check coverage, consistency, placeholder handling, and execution usability
10. **Hand off cleanly** - stop at a planning artifact and hand off to later execution

## Inputs

Read:
- the approved design input
- the engineering design artifact
- the UI/UX design artifact when relevant
- placeholder registry and referenced placeholder files
- relevant workspace context such as repo structure, package layout, and existing conventions

Ground planning in workspace reality:
- preserve upstream decisions unless you explicitly call out a conflict
- preserve repo and package boundaries from engineering design
- preserve UI/UX constraints and screen/state commitments when relevant
- do not silently replace deferred decisions with guesses

## Scope Check

If the approved inputs still cover multiple independent subsystems or incompatible scopes, do not write one blurred plan.

Instead:
- split the work into separate plans;
- keep each plan independently understandable and executable;
- stop before deep decomposition if the scope is still too wide.

## File Structure

Before deeper task decomposition, decide what structural boundaries matter for this plan:
- packages
- modules
- services
- files or ownership zones

Use structure to improve decomposition, not to force unnecessary refactors.

When structure matters, make it explicit in the plan so later execution does not have to rediscover it.

## Plan Levels

Choose the right level before writing the plan:

- **Initiative plan** - use for large work that still needs top-level sequencing across workstreams
- **Workstream plan** - use for a bounded feature or subsystem that needs structured implementation planning before file-level execution detail
- **Execution plan** - use close to implementation when enough decisions are settled to write deeper execution detail

Do not force execution-level detail when the work is still at initiative or workstream level.

## Planning Depth by Level

Use each level for a different kind of decision:

- **Initiative plan**
  - defines major workstreams, dependencies, sequencing, and expansion gates
  - should be ready to expand, not ready to code
- **Workstream plan**
  - defines the implementation shape for one bounded subsystem or feature area
  - should capture structure, ownership zones, patterns, integration boundaries, and must-preserve implementation approach for that workstream
  - should be ready to expand into execution planning, not necessarily ready to implement directly
- **Execution plan**
  - defines the concrete file/package slice, checks, and execution sequence close to implementation
  - should only be written when execution-blocking placeholders are resolved for that slice

Use deeper planning only when the current level can no longer reduce ambiguity enough on its own.

## Output

Default to a directory-based plan layout instead of one mixed file:

- initiative plan:
  - `docs/superpowers/plans/YYYY-MM-DD-<topic>/initiative.md`
- workstream plans:
  - `docs/superpowers/plans/YYYY-MM-DD-<topic>/workstreams/WS-XX-<topic>.md`
- execution plans:
  - `docs/superpowers/plans/YYYY-MM-DD-<topic>/execution/WS-XX/EX-XX-<slice>.md`

Use a stable topic slug and stable workstream IDs so later stages can find the right artifact without guesswork.

This artifact set is a planning system, not an implementation transcript.
User preference may override the default path, but the skill should still preserve:
- one stable plan root directory per initiative
- separate files per planning level
- explicit parent/child references between initiative, workstream, and execution plans

When useful, structure the artifact using the templates in this folder:
- `initiative-plan-template.md`
- `workstream-plan-template.md`
- `execution-plan-template.md`

Use the template that matches the chosen planning level, then adapt it to the actual work instead of filling it mechanically.

## File Convention

Make the storage layout explicit and easy for later stages to follow.

### Initiative plan

Use one root directory per initiative:

- `docs/superpowers/plans/YYYY-MM-DD-<topic>/initiative.md`

Here, `initiative root` means the initiative directory path:

- `docs/superpowers/plans/YYYY-MM-DD-<topic>/`

This file should:
- describe the initiative-level scope
- list workstream IDs
- link to child workstream plan files when they exist

### Workstream plans

Store each workstream as its own file:

- `docs/superpowers/plans/YYYY-MM-DD-<topic>/workstreams/WS-XX-<topic>.md`

Each workstream plan should:
- have a stable workstream ID such as `WS-01`
- link back to `initiative.md`
- link forward to execution plans created from that workstream
- make clear which placeholders and seams it carries forward

### Execution plans

Store each execution slice as its own file under its parent workstream directory:

- `docs/superpowers/plans/YYYY-MM-DD-<topic>/execution/WS-XX/EX-XX-<slice>.md`

Each execution plan should:
- have a stable execution ID such as `EX-01`
- only require `EX-XX` uniqueness within its parent `WS-XX` directory
- link back to its parent workstream plan
- preserve the workstream ID in its path so agents can locate siblings and parent context easily
- only exist for slices that are close enough to implementation

### Linking rules

Do not rely on memory to connect plan levels.

Prefer repo-relative file paths or markdown links that point to repo-relative paths so later agents can follow references uniformly.

Each plan file should explicitly reference:
- the initiative root
- its own plan level
- its own ID
- parent plan IDs and file paths where relevant
- known child plan IDs and file paths where relevant

When a deeper plan does not exist yet, say so explicitly instead of implying it.

## The Document Must Cover

1. Goal and scope
2. Scope check outcome
3. Plan level
4. Upstream inputs used
5. Constraints that must be preserved
6. Required constraints and must-use tools/libraries
7. Workstreams or tasks
8. Dependencies and ordering constraints
9. Ownership or affected packages/files/modules when known
10. File/package/module structure decisions when relevant
11. Consumed upstream seams when the plan depends on prior workstreams or earlier stages
12. Internal execution seams when later expansion would otherwise have to invent slice boundaries
13. Testing strategy appropriate to the task type
14. Manual verification expectations where relevant
15. Critical observability checkpoints where relevant
16. Observability / delivery implications where relevant
17. Provisional decisions that may need reconfirmation later
18. Deferred decisions and placeholder references
19. Unresolved blockers
20. Execution handoff notes

## Workstream-Level Shaping

When writing a workstream plan, make the implementation approach explicit enough that later execution does not improvise critical structure.

This may include:
- package or module boundaries
- component groupings or ownership zones
- integration boundaries and interface seams
- consumed upstream seams that this workstream assumes already exist
- internal execution seams that later planning expansion should not have to invent from scratch
- expected structural patterns for this workstream
- constraints from engineering design or UI/UX design that must survive execution

Do not hide this inside ad hoc task memory. Put it in the plan when the workstream depends on it.

Treat internal execution seams as planning expansion boundaries, not as code-level architecture instructions.

## Placeholder Rules

Do not write raw `TBD` where a placeholder should exist.

When placeholders affect the plan:
- preserve the placeholder ID
- state whether it is advisory, carry-forward, or blocking at this plan level
- do not write execution-level plans that depend on unresolved execution-blocking placeholders

If a placeholder blocks deeper planning, stop at the correct level instead of faking detail.

## Worktree and Version Control Context

When relevant, note execution context that later implementation may need:
- whether the work should happen in an isolated branch or worktree
- whether checkpoints or commits should happen at workstream or task boundaries

Treat this as planning context, not mandatory ceremony. Use it when it reduces implementation risk or coordination cost.

## Greenfield Foundation Rule

If the project is new and the work includes establishing the initial repo, app, package, or baseline architectural structure:
- default ownership for that foundation work belongs to the main orchestrator
- do not delegate initial structure definition by default to a separate implementation agent
- later bounded work can be delegated after the initial foundation is established and understood

Record this explicitly in the plan when it applies.

## Testing Strategy

Choose fit-for-purpose testing strategy per task or workstream.

Possible strategies include:
- strict TDD
- repro-first
- integration-first
- smoke-first
- spike mode

Do not force one testing style across all tasks by default.

## Planning Input Shape

The plan should make these items easy to extract for later execution:
- upstream inputs used
- plan level
- preserved constraints
- must-use tools/libraries
- expansion gates for the next planning level when relevant
- consumed upstream seams when later work depends on prior slices
- internal execution seams when later planning expansion needs stable slice boundaries
- task/workstream boundaries
- dependencies
- placeholder dependencies
- unresolved blockers
- testing strategy
- critical observability checkpoints where relevant
- manual verification expectations
- execution handoff notes

Treat critical observability checkpoints as planning-facing checkpoints for verification, instrumentation handoff, and runtime visibility expectations. Do not use them to smuggle full telemetry or alerting design into the plan unless that level of detail is already the stated planning scope.

## Self-Review

After writing the plan, review it with fresh eyes:

1. **Upstream coverage check** - does the plan cover the approved design, engineering, and UI/UX inputs that matter?
2. **Placeholder check** - are placeholder IDs preserved correctly, and are blocking conditions called out?
3. **Consistency check** - do task names, scopes, dependencies, and must-use tools line up, or do they contradict each other?
4. **Plan-level check** - is this the right planning depth, or did it become too shallow or too detailed?
5. **Execution usability check** - could a later execution stage actually use this plan without re-planning everything that should already be settled at this level?
6. **Blocker check** - are unresolved blockers visible as first-class planning concerns instead of being hidden in prose?
7. **Expansion check** - does this plan make it clear what the next planning or execution step can safely elaborate without re-arguing the current level?

Fix issues inline before handing off.

## Boundaries

This skill does not:
- write production code
- execute implementation
- casually rewrite upstream decisions
- force execution detail too early

If you start writing code or filling in implementation specifics that belong to execution, stop and return to planning.

## Drift Signals

You are drifting out of this skill if you start:
- writing code instead of plans
- ignoring upstream constraints
- dropping placeholder references
- forcing giant low-level detail too early
- writing vague tasks with no execution value
- hardcoding one testing style for every task
- leaving critical workstream structure implicit when later execution would have to guess it
- delegating greenfield foundation by default without recording why

## Handoff

After the planning artifact is complete:
- hand off to the appropriate later execution mode

Later execution mode may be inline, subagent-driven, or another execution-stage workflow. Keep the planning artifact usable across those modes instead of baking one fixed execution path into the plan.

Mention downstream stages only as handoff targets. Do not implicitly execute them from inside this skill.
Stop when later execution can use the plan without having to rediscover the approved inputs from scratch.
