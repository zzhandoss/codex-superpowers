---
name: ui-ux-design
description: Use after engineering-design and before writing-plans when the work needs explicit user flows, screen states, mockups, or interface decisions.
---

# UI/UX Design

Turn approved design intent and engineering constraints into a UI/UX design artifact that acts as a planning input for later implementation planning.

This skill exists because product/design intent and engineering decisions are still not enough for frontend-heavy work. Planning and implementation go more smoothly when flows, screens, states, and interaction rules are explicit.

This skill should also translate the relevant engineering boundaries into UI-facing structure decisions, such as shared-versus-local component expectations, design-system continuity, and screen-level ownership zones, without turning into an implementation plan.

This skill is iterative. It supports both:
- **initial UI/UX design** for creating the first approved artifact;
- **UI/UX revision** for updating the approved artifact later without silently breaking planning or implementation.

When multiple screens are involved, this skill must also preserve a stable cross-screen contract instead of treating each screen as an isolated generation request.

## Core Principle

**Do UI/UX concretization before implementation planning when the work needs explicit flows, screens, states, or mockups.**

Do not jump from approved design and engineering design directly into `writing-plans` if important UI/UX decisions are still implicit.

The output of this skill must reduce ambiguity for planning without turning into a task plan.
This skill is approval-driven. Do not silently invent flows, screens, tool-path choices, or design direction and then drop a finished artifact without explicit user confirmation.

<HARD-GATE>
Do NOT invoke `writing-plans`, write an implementation plan, break work into executable tasks, or take implementation action until you have produced a UI/UX design artifact that is sufficient input for later planning.
Exception: if this skill explicitly determines that no dedicated UI/UX artifact is needed for the current scope, use the bypass path instead of manufacturing one.
</HARD-GATE>

## Checklist

You MUST complete these stages in order:

1. **Inspect approved inputs** - read the approved design input, engineering design doc, and relevant workspace context
2. **Determine the mode** - choose `initial` when creating the first approved UI/UX artifact, or `revision` when updating an existing approved artifact
3. **Decide whether UI/UX work is needed** - if the work is backend-only or has no meaningful UI/UX impact, do not force this skill; hand off forward without inventing a UI/UX artifact
4. **Show the UI/UX need and scope packet** - present the UI/UX questions, intended screen/flow scope, and why this stage is or is not needed
5. **Get approval to continue this stage** - do not silently bypass or silently force UI/UX work when the scope is ambiguous
6. **Prepare a structured UI/UX spec** - clarify flows, screens, states, continuity rules, and visual goals before generation-heavy tool use
7. **Choose the tool path explicitly** - use Stitch Kit Integration if explicitly chosen, Visual Companion if explicitly chosen or clearly preferred, or a text-first fallback if that is what the user wants
8. **Show the proposed UI/UX direction** - surface the draft flows, screen set, state coverage, continuity rules, and chosen tool path before generating or locking the artifact
9. **Get approval on the UI/UX direction and tool path** - do not silently self-approve flows, screens, or tooling
10. **Define flows, screens, and states** - make user journeys, screen inventory, navigation, and state coverage explicit
11. **Define the shared shell and continuity contract** - lock shared navigation, recurring sections, stable labels, design-system rules, and screen-to-screen consistency before generating additional screens
12. **Translate engineering boundaries into UI structure** - make explicit what the later implementation must preserve about shared components, screen ownership, design-system continuity, and UI boundary rules
13. **If revising, classify the change and check impact** - determine whether the revision is cosmetic, structural, or flow/scope-changing, then check what planning or implementation it affects
14. **Produce visual or structured artifacts** - mockups, wireframes, diagrams, or structured textual equivalents
15. **Run continuity review after generated output** - check shell, menu, recurring blocks, shared terminology, visual tokens, and state treatment before accepting a screen
16. **Iterate if needed** - use an explicit loop such as generate, edit, variants, and design-system application until the result is planning-ready
17. **Write or update the UI/UX design artifact** - save it to the default path unless the user prefers a different location
18. **UI/UX self-review** - check the artifact against the approved design and engineering design docs and fix drift inline
19. **Hand off cleanly** - stop at a planning input and hand off to later workflow stages without taking them over

When several UI/UX choices naturally belong together, batch them and ask for approval as one packet instead of forcing trivial micro-approvals.

## Inputs

Read:
- the approved design input
- the engineering design artifact
- the current approved UI/UX artifact and accepted revisions when running in revision mode
- relevant project context such as repo structure, existing UI patterns, adjacent docs, and local conventions
- user preferences for visual tools and level of fidelity

Ground decisions in workspace reality:
- inspect the current repo structure and existing UI patterns if they exist
- preserve local patterns unless there is a clear reason to change them
- if UI aspirations conflict with scope or engineering constraints, call that out explicitly

## Modes

Use one of these two modes:

- **Initial mode**
  - create the first approved UI/UX artifact for this scope
- **Revision mode**
  - update an already-approved UI/UX artifact after new learning, theory-checking, implementation feedback, or tool output changes the preferred direction

Revision mode should not silently rewrite history. It should preserve what changed, why it changed, and what planning or implementation is affected.

## Revision Classification and Impact Check

If you are revising an existing UI/UX artifact, classify the change before accepting it:

- **Cosmetic**
  - changes emphasis, spacing, wording, or visual polish without changing flows, states, or UI structure
- **Structural**
  - changes hierarchy, screen composition, shared-versus-local UI structure, or continuity rules
- **Flow/scope**
  - changes user flow, required states, navigation model, screen set, or user-visible behavior

Then check impact:
- does this affect only future work, or also already-completed work?
- does this add new scope or only refine existing scope?
- does this change planning assumptions, execution slices, or placeholders?
- does this require a plan update, a rework task, or only an artifact refresh?

If the revision affects later planning or uncompleted work, produce an explicit planning impact summary instead of assuming the plan will stay valid automatically.
If the revision affects already-completed work, call out that rework impact explicitly even when future planning changes are small.

## Structured UI/UX Spec

Before generation-heavy tool paths, shape the work into a structured UI/UX spec instead of sending vague freeform prompts into tooling.

At minimum, make these explicit:
- primary user journeys
- screen inventory and purpose
- required states and transitions
- visual direction and fidelity target
- what must stay consistent across screens
- shared shell and navigation expectations when the product uses more than one screen
- recurring blocks and stable product vocabulary that must not drift screen-to-screen
- which UI structure or component-system constraints later implementation must preserve

For simple text-first work, this can stay lightweight. For Stitch Kit Integration, this should be explicit enough to support high-quality generation and iteration.

## Tool Path

Pick the tool path that best fits the current question:

- **Stitch Kit Integration** - use when the user explicitly chooses Stitch and you want screen generation, variants, or design-system-backed screen work
- **Visual Companion path** - use when browser-backed visual comparison, mockups, or diagrams will clarify choices better than text
- **Text-first fallback** - use when visual tooling is unavailable, unnecessary, or too expensive for the question

Tool paths are pluggable backends. The skill must still produce a useful UI/UX artifact even without Stitch or any browser-based helper.
If a preferred tool path is unavailable, fall back honestly and record that fallback in the artifact instead of pretending generation occurred.
Do not silently choose a generation-heavy path when the user has not approved it. If more than one path is plausible, present the options and get confirmation.

Operationally:
- **Stitch Kit Integration** means using Stitch project/screen workflows to generate or iterate on planning-grade UI artifacts
- **Visual Companion path** means producing browser-oriented mockups, comparisons, or diagrams for discussion and validation
- **Text-first fallback** means producing the same planning decisions through structured text, wireframe descriptions, and screen/state documentation without visual tooling

Use `Visual Companion path` when side-by-side comparisons, click-path validation, visual diff review, or lightweight visual theory-checking will clarify decisions better than static text.
Treat the `Visual Companion path` as complete when it has produced a planning-usable visual artifact set, such as comparisons, mockups, or diagrams, plus written continuity and decision notes in the UI/UX design artifact.

## Stitch Kit Integration

If the user explicitly chooses Stitch, base the UI/UX path on the Stitch stack while keeping control inside this skill.

Use Stitch as a backend, not as a replacement workflow.

When taking this path:
- prepare a structured spec or prompt shape before generation
- if the user already has a Stitch project or existing design work, ask whether to reuse it
- if there is no existing Stitch project context, create a new project by default
- generate the first accepted screen as a baseline, then lock its shell and continuity rules before generating later screens
- pass the locked shell contract, shared vocabulary, recurring sections, and must-preserve screen rules into each later screen generation step
- use Stitch-oriented ideation, prompt-architecture, generation, editing, or variant steps only insofar as they improve the UI/UX design artifact;
- keep the workflow bounded to UI/UX concretization;
- capture generated screens, variants, and design-system references as planning artifacts;
- preserve cross-screen continuity as an explicit requirement, not an accidental outcome;
- stop before code conversion, component export, or implementation-oriented follow-through;
- write the final UI/UX design artifact in this skill's format even if Stitch produced intermediate artifacts.

Borrow useful Stitch patterns where they help:
- stronger spec/prompt shaping before generation
- explicit tool-driven iteration loops
- design-system continuity across screens
- visual artifact references that later planning can preserve

Do not inherit Stitch behavior blindly. If any Stitch-oriented step conflicts with approved design intent, engineering constraints, or this skill's boundaries, preserve the v2 workflow contract.

If Stitch generation times out, do not treat that as final failure immediately. Check the project state, such as by listing screens, before concluding that generation failed.

For multi-screen Stitch work, do not prompt each screen independently as if it were a new product. Treat each later screen as a continuation of the accepted shell contract.

## Shared Shell and Continuity Contract

When more than one screen exists, define and preserve a shared shell contract before accepting the screen set.

At minimum, make these explicit when relevant:
- stable navigation items and labels
- stable top-level layout regions
- recurring sections or blocks that should persist across screens
- shared terminology for status, progress, completion, streaks, identity, and actions
- visual token continuity such as colors, density, surface treatment, and typography
- what is allowed to vary screen-to-screen versus what must remain fixed

Do not leave this implicit inside screenshots. Write it down in the artifact.

## Approval-Driven Behavior

Before writing or substantially rewriting the UI/UX artifact:
- show the user the current UI/UX scope packet or proposed direction packet;
- make it clear which parts are:
  - proposed and ready to approve
  - still exploratory
  - provisional
  - formally deferred into placeholders;
- make the selected tool path explicit instead of burying it in the final artifact;
- wait for explicit user approval of the current step or related batch of steps.

Good approval checkpoints include:
- whether this stage is needed at all
- the tool path choice
- the proposed flow and screen set
- the shared shell and continuity contract
- the acceptance or rejection of generated visual direction

Do not treat your own preference, implicit momentum, or a generated screen existing as approval.

## Accepted Screen Baseline

When tool-backed generation is used, especially with Stitch:
- treat the first accepted screen as a baseline reference
- record what later screens must preserve from that baseline
- classify each generated screen as:
  - `chosen`
  - `provisional`
  - `reference-only`

Do not assume generated output is accepted just because it exists.

For each accepted or provisional screen, record:
- why it is in that status
- what must be preserved
- what must still be corrected or normalized in later iterations

## Screen Generation Packet

Before generating any second or later screen in a multi-screen set, pass a continuity packet into the generation step.

This packet should include:
- approved design input summary
- engineering constraints that affect UI shape
- accepted screen baseline
- locked shell and navigation rules
- recurring blocks and shared sections
- shared terminology and CTA language
- design-system references
- what the new screen is allowed to vary
- what the new screen must preserve exactly

Do not generate later screens from a blank-slate prompt if a prior accepted screen already exists.

## Continuity Review

After each generated or revised screen, explicitly review:
- shell consistency
- menu and navigation consistency
- recurring block consistency
- shared terminology consistency
- color and token consistency
- state-treatment consistency
- CTA language consistency
- product-role consistency for that screen

If the screen breaks the continuity contract, mark it `provisional` or iterate again instead of silently accepting drift.

## Bypass

If this stage is not needed:
- state briefly that no dedicated UI/UX design artifact is needed for this work
- preserve any already-known UI constraints if they exist
- hand off forward without manufacturing extra design ceremony

In bypass mode, do not create the default UI/UX artifact unless the user explicitly wants a record.

## Output

Write:
- `docs/superpowers/uiux/YYYY-MM-DD-<topic>-uiux-design.md`

This document is a planning input, not an implementation plan.
User preference may override the default path, but the skill should still use a clear file name and stable location.

## The Document Must Cover

1. Purpose and scope
2. Mode: initial or revision
3. Upstream inputs used
4. Current effective UI/UX state
5. Accepted revisions when relevant
6. User journeys / flows
7. Screen inventory and screen purpose
8. Required states per flow or screen
9. Navigation and interaction rules
10. Layout / wireframe / mockup guidance
11. Visual direction appropriate to the product scope
12. UI structure and shared-versus-local component expectations when relevant
13. Shared shell contract when relevant
14. Design-system continuity and cross-screen consistency rules when relevant
15. Accepted screen baseline and screen status when tool-backed generation is used
16. Continuity packet inputs used for later screens when relevant
17. Assumptions
18. Non-goals
19. Risks and tradeoffs
20. Tool path used and visual artifact references
21. Provisional decisions that may need reconfirmation later
22. Deferred UI/UX decisions via placeholder IDs
23. Constraints that implementation planning must preserve
24. Planning impact summary when revisions affect planning or not-yet-completed work
25. Planning-input summary for later `writing-plans`

Required state examples to consider when relevant:
- loading
- empty
- error
- success
- reconnect
- permission

If Stitch Kit Integration was used, also include:
- Stitch project or screen references if available
- screenshot and HTML references if available
- what was generated versus what was only discussed
- what later planning must preserve from Stitch outputs

When multiple screens are involved, also include:
- what must remain visually and structurally consistent across screens
- what design-system or shared-pattern decisions tie the screen set together

When running in revision mode, also include:
- what changed
- why it changed
- change class: cosmetic, structural, or flow/scope
- what plan items or future implementation slices are affected
- whether rework is needed now, later, or not at all

## Decision Quality

For every meaningful UI/UX decision:
- state the chosen option
- give the rationale
- note important rejected alternatives when useful
- make tradeoffs explicit
- make constraints visible to later planning

Do not hide uncertainty behind vague wording.

Use UI structure guidance to preserve intent, not to prescribe implementation detail.

Good examples include:
- what should become shared design-system or shell-level components
- what should stay screen-local or feature-local
- where cross-screen consistency is mandatory
- what later planning must preserve about composition boundaries

Do not drift into file-level component decomposition or code-oriented implementation patterns here.

Scale visual direction to the product stage and scope:
- for early or low-fidelity work, structured wireframes and state coverage may be enough
- for more polished product work, include stronger hierarchy, navigation clarity, and concrete visual references
- do not invent high-fidelity polish when the project only needs planning-grade clarity

## Deferred Decisions

If a UI/UX question cannot be answered yet:
- do not write `TBD`
- create or reference a formal placeholder
- use a formal placeholder ID
- make the blocking level explicit
- label whether the placeholder is blocking or safe to carry forward
- explain why the decision is deferred
- state what stage it blocks, if any
- state the trigger for resolution

Deferred decisions are allowed here if they are formalized clearly and do not pretend to be resolved.

When placeholders are present, keep them centralized in a clear `Open Questions and Placeholders` section instead of scattering them unpredictably across the document.

Minimal reference style inside the UI/UX artifact:
- `Placeholder: PH-017`
- `Blocking placeholder: PH-021`

## Planning Input Shape

The UI/UX design artifact should be easy for `writing-plans` to consume later.

Make sure the document makes these items easy to extract:
- upstream inputs used before visual generation
- current effective UI/UX state
- accepted revisions when relevant
- required flows and screens
- must-have states and transitions
- UI structure rules and shared-versus-local component expectations that later planning must preserve
- provisional UI decisions that may need reconfirmation before execution
- deferred decisions and their placeholder IDs
- visual artifacts or references produced during the process
- UX constraints that planning must preserve
- screen, project, or design-system references when tool-backed generation was used
- screenshot and HTML refs when Stitch-backed generation produced them
- continuity rules that later planning must preserve across the full screen set
- locked shell rules and recurring UI blocks that later implementation should not improvise
- accepted screen baseline and per-screen status when tool-backed generation was used
- planning impact summary when revisions change future work

## UI/UX Self-Review

After writing the UI/UX design artifact, review it with fresh eyes against the approved design doc and engineering design doc:

1. **Design alignment check** - does the UI/UX artifact preserve the approved user-facing intent?
2. **Engineering alignment check** - does it respect the engineering boundaries and constraints?
3. **Flow and state check** - are the main journeys, screens, and critical states explicit?
4. **UI-structure check** - does the artifact capture the UI-side structure, shared-versus-local expectations, and continuity rules that later implementation should not improvise?
5. **Continuity check** - if multiple screens are involved, is consistency across screens explicit rather than implied?
6. **Shell-contract check** - are stable nav items, shared sections, recurring blocks, and vocabulary written explicitly instead of left to screenshot interpretation?
7. **Screen-status check** - is it clear which screens are chosen, provisional, or reference-only?
8. **Placeholder check** - are unresolved UI/UX decisions formalized with placeholder IDs instead of vague prose?
9. **Provisional-versus-deferred check** - is it clear what is provisional versus formally deferred?
10. **Revision-impact check** - if this is a revision, is the impact on plans or implementation explicitly called out instead of being left implicit?
11. **Planning-input check** - is the artifact easy for `writing-plans` to consume, or did it drift into a free-form design essay?
12. **Boundary check** - did the document drift into implementation detail, component code, or execution ordering?

Fix issues inline before handing off.

## Boundaries

This skill does not:
- decompose work into implementation tasks
- define execution order
- prescribe low-level component code
- simulate `writing-plans`
- write production code

If planning or implementation detail starts to dominate, stop and hand off instead of expanding this skill's scope.

## Drift Signals

You are drifting out of this skill if you start:
- breaking work into executable tasks
- prescribing component-by-component implementation
- writing like a planner instead of a UI/UX design layer
- leaving unresolved areas without formal placeholders
- assuming one tool path without fallback
- sending vague freeform prompts into generation-heavy tools without shaping the spec first
- treating multi-screen continuity as optional or accidental
- generating later screens without passing forward the accepted shell contract
- accepting generated screens without reviewing menu, block, or vocabulary consistency
- revising UI/UX direction without stating what changed or what planning it affects
- giving generic UI advice that is not grounded in the approved inputs
- talking about downstream stages as if this skill owns them
- letting Stitch-oriented work continue into code conversion or implementation
- treating Stitch timeout as final failure without checking project state
- always creating a new Stitch project when existing-project reuse should be considered

## Handoff

After the UI/UX design artifact is complete:
- hand off to `writing-plans` when planning-ready UI/UX inputs are in place

Mention downstream stages only as handoff targets. Do not implicitly orchestrate them from inside this skill.
Stop when later planning can extract, without guesswork:
- the required user flows
- the screen inventory
- the must-have states and transitions
- any visual/tooling references that must be preserved
- any deferred UI/UX decisions and their placeholder IDs
