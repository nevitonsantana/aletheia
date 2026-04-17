# Slice Finalization and Clean Restart

## Goal

Define how AletheIA can help teams end one bounded slice, preserve usable continuity, and start the next slice in a fresh thread or session **without depending on transcript replay**.

This document exists because many teams describe the problem as:

- "clear the thread"
- "clear the chat cache"
- "start clean for the next task"

AletheIA should interpret that operationally, not literally.

The framework does **not** manage runtime cache internals.
It helps teams reach a state where a clean restart is healthy because the previous slice has already been finalized well.

---

## Correct framing

The problem is not:

> how do we clear a chat?

The problem is:

> how do we close one slice cleanly enough that the next slice can begin without hauling old thread residue forward?

That is why the framework should keep saying:

- restart packages, not transcripts
- slice closure before clean restart
- continuity by explicit artifact, not hidden memory

---

## What this capability should do

A healthy slice-finalization and clean-restart layer should help teams:

- confirm whether the current slice is actually complete enough to stop
- capture a compact restart package
- decide whether continuing in the same thread is still healthy
- recommend a clean restart only when the next slice no longer benefits from old thread carryover
- bootstrap the next slice with the smallest useful context package

---

## What this capability should not claim

This layer should **not** claim that AletheIA:

- clears model memory or runtime cache internals
- controls `/clear`, `/new`, or provider-native reset commands
- requires runtime hooks or automation to be useful
- replaces project-local governance or trust rules

Those remain local runtime or project concerns.

---

## Finalization outcomes

For this bounded layer, AletheIA can express four practical outcomes:

### `continue-in-session`

Use when:

- the next step is still part of the same bounded slice
- the current thread still contains useful local context
- restart would add ceremony without reducing confusion

### `recommend-clean-restart`

Use when:

- the slice is finished and validated enough to stop
- the next step is a new bounded slice
- transcript replay is no longer the healthiest continuity path
- a compact restart package exists

### `review-required`

Use when:

- the current slice is partially closed but the next move is still ambiguous
- the restart package is too weak or too inflated
- multiple continuations are plausible and the thread should not be cleared yet

### `not-ready`

Use when:

- validation is incomplete
- conflict or unresolved risk is still open
- no usable restart package exists
- a clean restart would only hide unresolved work

---

## Minimum finalization checks

Before a clean restart is recommended, the framework should at least be able to answer:

1. Was the slice validated enough for closure?
2. Is the next action explicit?
3. Is the restart package compact enough to replace transcript replay?
4. Would continuing in the same thread preserve more noise than value?

If the answer to any of those is unclear, `recommend-clean-restart` is premature.

---

## Anti-fatigue rule

AletheIA should treat a clean restart as successful only when it reduces both:

- **human fatigue**
  - recap burden
  - redundant questions
  - confusion about what changed
- **operational fatigue**
  - stale context carryover
  - retry drag
  - thread expansion beyond the healthy slice boundary

A clean restart that still requires replaying the old transcript is not a real win.

---

## Relationship to Alpha 4 and 1.2

This layer does not replace existing handoff or resource-aware work.
It composes them.

It builds on:

- `docs/agent-handoffs.md`
- `docs/handoff-capture-pattern.md`
- `docs/work-slice-pattern.md`
- `docs/token-policy.md`
- `docs/resource-aware-operations-roadmap.md`
- `docs/waste-heuristics.md`
- `docs/progressive-policy-signals.md`
- `docs/readiness-gates-spec.md`

In practice, this layer is a bounded bridge between:

- Alpha 4 restart-package continuity
- the 1.2 resource-aware stop/continue posture

---

## Clean restart as a local runtime action

The framework meaning should stay stable even if runtimes differ.

That means:

- one runtime may expose `/clear`
- another may expose `/new`
- another may require starting a new session manually
- another may offer custom slash commands

AletheIA should care about the **semantic outcome**, not the runtime-specific mechanic.

The semantic outcome is:

> the next slice starts with a compact restart package instead of inherited thread residue.

---

## Recommended local composition

Projects that want to test this pattern should usually compose four artifacts:

1. a slice-finalization review
2. a restart package
3. a restart bootstrap prompt
4. an optional runtime-local adapter mapping

The framework core stays smaller if these remain docs-first and manual-first before any automation attempt.

---

## Healthy first use

The healthiest first use is usually:

- one recently completed bounded slice
- one explicit next slice
- one compact restart package
- one local clean-start action
- one review of whether the next slice could start without transcript replay

This is enough to test the pattern without overbuilding it.
