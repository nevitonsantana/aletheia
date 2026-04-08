# Iterative Maintenance — Three-Round Loop

## Goal

This example shows how AletheIA can make an iterative maintenance loop more legible **without** introducing a new round schema or copying the SWE-CI benchmark architecture.

The example treats each round as a **work slice composition** built from existing artifacts.

---

## Scenario

A team is maintaining a shared configuration-normalization helper.

The maintenance loop evolves across three rounds:

### Round 1
- introduces a bounded improvement
- validates it sufficiently
- closes without relevant regression

### Round 2
- expands the helper to another path
- accidentally regresses a previously stable legacy alias behavior
- escalates the round instead of pretending progress is clean

### Round 3
- resolves the regression
- widens validation because the area now has recent regression history
- stores a reusable learning for future rounds

---

## Why this matters

The point is not to simulate CI scoring.
The point is to show that AletheIA can make a maintenance loop easier to read across:

- round framing
- decision continuity
- regression-aware gating
- restartable handoff
- reusable learning

---

## Artifact layout

### `round-1/`
- `README.md`
- `task-brief.json`
- `decision-record.json`
- `execution-record.json`

### `round-2/`
- `README.md`
- `task-brief.json`
- `decision-record.json`
- `execution-record.json`
- `handoff-record.json`

### `round-3/`
- `README.md`
- `task-brief.json`
- `decision-record.json`
- `execution-record.json`
- `handoff-record.json`
- `learning-record.json`

---

## Experimental question

Does this example make a maintenance loop:

- more legible
- more auditable
- less dependent on implicit memory
- more explicit about how regression changes the next gate?

If not, the pattern should stay optional and continue evolving before any contract is hardened.
