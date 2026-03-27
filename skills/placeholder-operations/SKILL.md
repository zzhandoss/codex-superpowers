---
name: placeholder-operations
description: Use when a decision, answer, or engineering detail must be deferred formally instead of being left as an untracked TBD.
---

# Placeholder Operations

## Overview

Use placeholders to defer decisions formally.

Do not write untracked `TBD`, `TODO`, or vague unresolved notes when the missing information affects future design, planning, or implementation work.

## Core Principle

**Deferred does not mean forgotten.**

If something cannot be decided now, record it as a placeholder with a stable ID and enough context for another agent or future stage to resolve it safely.

## When to Use

Use this skill when:
- an engineering decision cannot yet be made;
- the answer depends on later context;
- implementation or planning depends on a missing answer;
- a design/planning artifact must record an unresolved item cleanly.

## Required Placeholder Fields

Every placeholder must have:
- ID
- title
- status
- type
- blocking level
- owner
- created at
- needed by
- resolution trigger
- references
- question
- why deferred
- current context
- resolution

## File Structure

Store placeholders in:
- `docs/superpowers/placeholders/index.md`
- `docs/superpowers/placeholders/PH-XXX.md`

## Rules

1. Never write plain `TBD` if a placeholder should exist.
2. Always give the placeholder a stable ID.
3. Always record where the placeholder is referenced.
4. Always state whether it blocks planning or execution.
5. If the answer becomes known, update the placeholder instead of silently editing only one downstream document.

## Reference Style

In docs and plans, reference placeholders as:
- `Placeholder: PH-017`

If the placeholder is blocking, say so explicitly near the reference.

## Minimal Lifecycle

- create placeholder
- reference placeholder
- update placeholder as context grows
- resolve / obsolete / supersede placeholder

## Output

When using this skill, create or update the placeholder artifact and make sure references are added or corrected in the calling document.
