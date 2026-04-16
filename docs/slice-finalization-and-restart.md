# Slice Finalization & Restart Guidance

## Goal

Define a manual-first way to close a work slice cleanly, preserve continuity through a compact restart package, and recommend a clean new session only when transcript replay is no longer needed.

This is not a "clear chat" feature.
It is a slice-finalization capability.

---

## Why this exists

Long AI-assisted threads tend to accumulate stale context.
That creates two related forms of avoidable fatigue.

### 1. Human fatigue

Examples:

- heavy recap before the next step begins
- repeated questions about decisions that were already settled
- ambiguous reopen state after the useful part of the slice is already done

### 2. Operational fatigue

Examples:

- context inflation from legacy material
- retries that keep happening inside a slice that should already have closed
- drift caused by continuing in the same session after the real boundary was already crossed

AletheIA already has the right principle:

**restart package, not transcript**

This guide turns that principle into an explicit closure practice.

---

## Relationship to existing AletheIA surfaces

This guide reuses existing surfaces.
It does **not** replace them.

It builds on:

- `docs/agent-handoffs.md`
- `docs/work-slice-pattern.md`
- `docs/slice-telemetry-model.md`
- `docs/progressive-policy-signals.md`
- `docs/readiness-gates-spec.md`

Use the existing handoff record as the structured continuity artifact.
Use this guide as the operational review layer for deciding whether the slice is ready for healthy restart.

---

## Finalization flow

A healthy slice finalization should follow this order:

1. validation check
2. handoff / restart check
3. AI fatigue read
4. finalization outcome
5. optional clean-restart recommendation

The goal is not to restart by habit.
The goal is to restart when continuing in the same session would now carry more drag than value.

---

## Minimum finalization questions

Before a slice closes, ask:

### 1. Was the slice validated?

If validation is still incomplete, the slice is not ready.

### 2. Is the next action explicit?

If the next action is unclear, clean restart is unsafe.
The slice needs review first.

### 3. Is a structured continuity artifact available?

A compact handoff or restart package should exist whenever the next boundary matters.

### 4. Does the next step still belong to the same slice?

If yes, continuing in the same session may still be healthier.
If not, a bounded restart may be healthier.

### 5. Would the next session still depend on replaying transcript history?

If yes, the slice has not closed cleanly enough.

---

## AI Fatigue Read

A finalization review should explicitly read these fields:

- `stale_context_risk`: `low | medium | high`
- `transcript_replay_needed`: `yes | no`
- `restart_burden`: `low | medium | high`
- `handoff_size_class`: `compact | inflated | heavy`
- `redundant_question_risk`: `low | medium | high`
- `governing_context_changed`: `yes | no`
- `governing_context_ref`: list of refs
- `governing_context_summary`: short summary when changed

### Hard rule

If `transcript_replay_needed = yes`, the slice is **not** ready for healthy clean restart.

That means the next boundary would still depend on hidden history instead of compact durable context.

---

## Finalization outcomes

### `continue-in-session`

Use when:

- the next step still belongs to the same bounded slice
- context carryover is still useful
- fatigue signals are still low enough that continuing is healthier than resetting

### `recommend-clean-restart`

Use when:

- the slice is validated
- the next action is explicit
- the restart package is compact
- transcript replay is not needed
- stale context risk for the next slice is `medium` or `high`

### `review-required`

Use when:

- the next action is ambiguous
- regression or fork is still open
- the handoff is inflated
- restarting now would carry confusion into the next session

### `not-ready`

Use when:

- validation is incomplete
- conflict or high-risk review is still open
- the closure rule is not yet satisfied

---

## Restart package as a physical block

Do not treat the restart package as only a loose summary inside the handoff.

For this v1, the operator-facing artifact should include a **copyable markdown block**:

```md
<!-- RESTART_PACKAGE_BEGIN -->
## Context for Clean Restart
- **Slice ID:** ...
- **Validation Status:** ...
- **Mission Focus:** ...
- **Active Spec / Entrypoint:** ...
- **Last Handoff Summary:** ...
- **Next Immediate Action:** ...
- **Known Constraints:** ...
- **Governing Context Version:** ...
- **Governing Context Delta:** ...
<!-- RESTART_PACKAGE_END -->
```

This block is meant to let the operator begin a new session with minimal noise.

---

## Project-local governing context

Projects may define their own governing-context sources.

Examples might include:

- active feature or plan docs
- project decision logs
- project state summaries
- local changelog entries

This remains project-local.
AletheIA should require the **meaning** of governing-context continuity, not one universal project file.

---

## Runtime boundary

AletheIA does **not** depend on a runtime command such as `/clear` or `/new`.

In this version:

- runtime actions remain illustrative only
- restart is still a local operator action
- no runtime hooks or auto-reset behavior are part of the core

The core capability is:

- finish the slice
- preserve continuity
- detect fatigue risk
- recommend restart when healthy

---

## Success read

A healthy restart recommendation should usually imply:

- `transcript_replay_needed = no`
- `redundant_question_risk = low`
- `restart_burden = low`

A practical success proxy is:

- **TRC (Time to Recover Context)** `< 2 interactions`

If a restarted session needs more than two back-and-forth turns before it becomes productive, the restart package was not self-contained enough.

---

## What this is not

This guide is not:

- a new canonical reset schema
- a runtime-hook system
- a benchmark layer
- a learning-layer capability
- a promise of zero cognitive effort

It is a bounded operational practice for reducing avoidable AI fatigue.

---

## Suggested next reading

- `docs/agent-handoffs.md`
- `docs/work-slice-pattern.md`
- `docs/readiness-gates-spec.md`
- `docs/slice-telemetry-model.md`
- `starter-pack/templates/slice-finalization-review-template.md`
- `examples/resource-aware-operations/slice-finalization-reference.md`
