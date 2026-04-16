# Slice Finalization Reference

## Context

A bounded slice finished its useful implementation work and passed the declared validation.

The next step is a separate reviewable task rather than a continuation of the same slice.

## Finalization read

- Slice ID: `example-slice-finalization-001`
- Validation status: `validated`
- Handoff ref: `handoff-record.json`
- Next action: `Start the next review slice using the restart package`
- Resume entrypoint: `docs/feature-review-notes.md`

## AI Fatigue Read

- Stale context risk: `high`
- Transcript replay needed: `no`
- Restart burden: `low`
- Handoff size class: `compact`
- Redundant question risk: `low`
- Governing context changed: `yes`
- Governing context refs:
  - `docs/feature-review-notes.md`
  - `docs/DECISIONS.md`
- Governing context summary: `The active direction narrowed from implementation to review-only closure after validation passed.`

## Finalization outcome

- Outcome: `recommend-clean-restart`
- Reason: `The current slice is validated and complete, but the next task is a distinct review step that should not inherit stale execution context.`

## Restart Package

<!-- RESTART_PACKAGE_BEGIN -->
## Context for Clean Restart
- **Slice ID:** `example-slice-finalization-001`
- **Validation Status:** `validated`
- **Mission Focus:** Close the current slice and begin the review-only continuation with minimal inherited context.
- **Active Spec / Entrypoint:** `docs/feature-review-notes.md`
- **Last Handoff Summary:**
  - implementation work was completed
  - declared validation passed
  - the next boundary is a review slice, not more execution in the same thread
- **Next Immediate Action:** Open the review notes and continue from the explicit next action instead of replaying transcript history.
- **Known Constraints:** Do not resume by scanning old transcript unless the restart package proves insufficient.
- **Governing Context Version:** `review-direction-1`
- **Governing Context Delta:** Shift from implementation mode to review-only closure after validation passed.
<!-- RESTART_PACKAGE_END -->
