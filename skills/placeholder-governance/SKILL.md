---
name: placeholder-governance
description: Use when auditing or cleaning the placeholder system to detect stale, orphaned, duplicated, or invalid placeholder states across docs and plans.
---

# Placeholder Governance

## Overview

This skill maintains the health of the placeholder system.

It does not create new product or engineering decisions. It checks whether the placeholder registry still matches the actual state of the docs, plans, and workflow.

## Core Principle

**A placeholder database is only useful if it stays accurate.**

## What to Check

1. Missing placeholder files referenced from docs or plans
2. Placeholder files that are no longer referenced anywhere
3. Open placeholders that are stale
4. Duplicate placeholders for the same unresolved question
5. Resolved placeholders that are still treated as blocking
6. Execution or low-level plans that still depend on execution-blocking placeholders
7. Obsolete placeholders that should be cleaned up or superseded

## Sources of Truth

Read:
- `docs/superpowers/placeholders/index.md`
- `docs/superpowers/placeholders/PH-*.md`
- engineering docs
- planning docs
- any artifact that references placeholder IDs

## Output

Produce an audit report that includes:
- healthy placeholders
- stale placeholders
- orphan placeholders
- dangling references
- duplicate candidates
- cleanup recommendations

## Cleanup Rules

- Do not delete placeholders silently.
- Prefer status updates: `resolved`, `obsolete`, `superseded`.
- If merging duplicates, preserve cross-references.
- If a placeholder is no longer needed, record why.
