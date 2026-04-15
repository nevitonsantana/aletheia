# Workflow / Readiness Example

## Context

A slice begins as a medium-sized implementation task with:

- bounded execution
- moderate semantic risk
- a likely review step before closure

Initial planning read:

- planning depth -> `Standard`
- runtime fit -> balanced executor

## Quick readiness review before execution

### Context minimum exists

Pass.
The slice has the relevant files, local objective, and known constraint boundary.

### Decision is clear enough

Pass.
The next move and validation shape are explicit.

### Risk is mapped enough

Pass.
The work is meaningful but still reviewable.

### Handoff is usable enough

Not yet needed.
A handoff is possible, but not required before execution starts.

### Runtime fit is acceptable enough

Pass.
The current runtime is proportional to the slice.

## What changed mid-slice

During execution:

- ambiguity rose
- retries increased
- the likely review burden became heavier than expected

## Better operational read

The slice still exists, but the posture changed.

Healthier next move:

- keep the slice bounded
- reconsider runtime fit
- prepare a clearer review or handoff boundary before continuing

That means the slice may now move from:

- `Standard` planning depth with `continue`

to:

- `Standard` planning depth with a `review` or `handoff` outcome

## Why this matters

The value is not more ceremony.
The value is noticing early that the work is no longer healthy to push forward in the same posture.
