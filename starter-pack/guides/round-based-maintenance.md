# Round-Based Maintenance

## Goal

This guide explains how to operate **iterative maintenance work** with AletheIA by treating each round as a **composed work slice**.

It does not introduce a new round schema.
It does not require a benchmark harness.
It uses the contracts that already exist.

---

## What a round is

A round is one bounded maintenance move inside a longer chain of evolution.

A healthy round should answer:

- what this iteration is trying to improve
- what it will deliberately leave for later
- what risk it carries
- what proof is required before it may close
- whether a regression changed the next step

A round is not the whole maintenance story.
It is one legible step inside that story.

---

## Round as work slice

The safest way to model a round in AletheIA is as a **work slice composition**.

A round can usually be made explicit through:

1. `task brief`
2. `decision record`
3. `execution record`
4. `handoff record` when the next boundary matters
5. `learning record` when the round generates reusable learning

This means round-based maintenance should begin as an operating pattern, not as a new core contract family.

---

## Generic roles inside a round

You do not need to copy SWE-CI's exact roles.
AletheIA can stay generic.

A practical round often involves some mix of:

- **planner** — frames the next bounded move
- **executor** — performs the change
- **reviewer** — evaluates whether the round may truly advance or must slow down

Sometimes one agent or one human may play more than one role.
The important part is that the transitions stay reviewable.

---

## What the decision record should clarify

Before execution, the round should make explicit:

- the current gap being addressed
- what was accepted into this round
- what was intentionally left out
- what risk posture applies
- what validation is expected
- what kind of failure would change the gate

That is what keeps a round from collapsing into “another attempt.”

---

## Minimum validation for a round

Every round should declare its minimum proof before execution ends.

That proof might include:

- targeted tests
- smoke checks
- diff inspection
- review of sensitive files
- contract consistency checks
- selective structured inference when semantic risk is hard to validate directly

The key is not maximum ceremony.
The key is visible closure discipline.

---

## Regression as a round event

If a previously stable behavior breaks, the round should no longer be read as clean progress.

In practice, regression can change the round in several ways:

- `validation-pending -> review`
- `review -> blocked`
- `blocked -> escalated` when the regression stays unresolved or becomes more sensitive

Regression should also influence later rounds.
A recent regression in the same area is a signal that the next round deserves a stronger gate.

Silent degradation matters too.
A round can still look superficially successful while a useful operational signal is getting weaker.
When that happens, the next continuation should not be read as fully clean progress.

---

## When to widen the gate

Increase the validation or review burden when:

- a round touches a path with recent regression history
- the new change sits on top of an earlier fragile decision
- the regression is semantic and not easy to catch by simple tests
- the next round crosses an agent or ownership boundary
- the cost of another failure is now higher than in the first round
- a lane health reading suggests that quality is eroding even when the main path still works

Do not widen the gate just because work is iterative.
Widen it because the round history justifies it.

---

## A proportional operational sequence

For more important iterative loops, a useful sequence is:

1. prove the round or lane with a real bounded slice
2. harden the contract that keeps the lane coherent
3. expose a small health metric when quiet degradation matters
4. add an alert if degradation should change behavior
5. make the degraded case investigable
6. keep a compact summary for the next continuation or reviewer

This should stay proportional.
It is not required for every maintenance task.
It is useful when the loop is important enough that continuation quality matters.

---

## When to hand off

Generate a handoff when:

- a reviewer or next maintainer needs to resume from the current round
- a regression changed the expected next action
- the next iteration depends on a compact summary of what failed, what was fixed, and what is still open
- the round should pause at a review or trust boundary

A handoff should remain a restart package, not a transcript of the whole loop.

---

## When to generate a learning record

Generate a learning record when the round exposed something reusable, for example:

- a recurring regression pattern
- a missing validation rule
- a fragile module that deserves stronger default scrutiny next time
- a context gap that made the wrong change easier to introduce
- a planner/executor/reviewer coordination mistake that is likely to repeat
- a signal that should exist before the next continuation is treated as safe

Learning is most useful when it helps the next round avoid the same failure mode.

---

## Suggested round recipe

1. Frame the round as a bounded work slice.
2. Record the round decision before execution.
3. Execute with the minimum declared validation.
4. If regression appears, change the round state and re-read the gate.
5. Add a compact health reading only when the loop is important enough to justify it.
6. Create a handoff if the next boundary matters.
7. Store a learning record if the round taught something reusable.

---

## Example

See:

- `examples/iterative-maintenance/three-round-loop/README.md`
- `examples/pilot-conversion/crisis-monitor-real-world-validation.md`

Together, these examples show both:

- a generic three-round loop
- a real pilot conversion where proof, contract, health, alert, investigation, and summary hardened the reusable guidance without changing the core contracts
