# Clean Restart Command Adapter Example

## Scenario

A bounded slice just finished.

The team now needs to decide whether to:

- continue in the same thread
- stop for review
- or start the next slice in a clean thread with a compact restart package

---

## Step 1 — finalize the slice

Logical command:

- `/finalize-slice`

Review result:

- validation status: complete
- next action: explicit
- restart package: compact
- transcript replay needed: no

Outcome:

- `recommend-clean-restart`

---

## Step 2 — map into a runtime-local clean start

Possible Codex-style local action:

- operator starts a fresh thread or uses a local clean-start action

Possible Claude Code-style local action:

- operator starts a fresh session or clean thread in the local workflow

The framework meaning remains the same:

- the next slice should begin from the restart package, not from inherited thread residue

---

## Step 3 — resume from package

Logical command:

- `/resume-from-package`

Bootstrap prompt shape:

```text
Continue the project with a fresh thread for the next bounded slice.

Read only:
- the restart package
- the active slice / next-slice entrypoint
- any minimal governing refs listed there

Current objective:
prepare the next bounded pilot review

Primary entrypoint:
docs/resource-aware-bounded-pilot.md

Known constraints:
do not replay the old transcript; keep the next slice bounded
```

---

## Why this is healthier than transcript carryover

This pattern is healthier when:

- the finished slice already has reviewable closure
- the next slice is meaningfully new
- old thread context contains more stale residue than useful carryover
- the restart package is strong enough to start the next slice quickly

It is **not** healthier when the next move still belongs to the same slice or the restart package is too weak.

---

## Failure case

Bad pattern:

- `/clean-restart` is used before validation is done
- the restart package is vague
- the next session still needs the whole transcript to proceed

In that case, the real outcome was either:

- `review-required`
- or `not-ready`

not `recommend-clean-restart`.
