# Clean Restart Command Adapters

This guide adds a small operator-facing command vocabulary on top of the existing slice-finalization flow.

It does **not** change the core framework contract.
It only shows how a team may expose clean-restart behavior through lightweight slash-command style adapters.

Use this guide together with:

- `docs/slice-finalization-and-restart.md`
- `starter-pack/templates/slice-finalization-review-template.md`
- `starter-pack/templates/restart-bootstrap-prompt-template.md`

---

## Why this exists

Many teams want a short operator command for:

- closing a slice
- deciding whether to restart cleanly
- resuming from a compact restart package

That is useful, but AletheIA should stay smaller than a CLI or runtime platform.

So this guide defines a **logical command vocabulary**:

- `/finalize-slice`
- `/clean-restart`
- `/resume-from-package`

These commands are **adapter vocabulary only**.

- if a runtime supports slash commands, an adapter may expose them that way
- if it does not, the operator can run the same flow as a checklist with no semantic loss

---

## Command semantics

### `/finalize-slice`

Purpose:

- run the slice-finalization review
- fill the finalization template
- emit a copyable restart package block
- decide the finalization outcome

Required result:

- one of:
  - `continue-in-session`
  - `recommend-clean-restart`
  - `review-required`
  - `not-ready`

Minimum operator inputs:

- slice id
- validation status
- next action
- resume entrypoint
- AI Fatigue read

### `/clean-restart`

Purpose:

- start a fresh session only after the slice is already closed cleanly

Allowed only when:

- finalization outcome is `recommend-clean-restart`

Meaning:

- the operator should begin a fresh session using:
  - the restart package
  - the resume entrypoint
  - the minimal governing-context refs

This command must **never** imply that AletheIA controls:

- chat cache internals
- runtime memory internals
- hidden session state

It only signals that a clean restart is now the healthier operating choice.

### `/resume-from-package`

Purpose:

- resume work from the restart package only

Meaning:

- bootstrap the next slice from:
  - the restart package
  - the restart bootstrap prompt
  - the explicit governing refs when present

Default rule:

- do **not** replay transcript history unless the restart package proves insufficient

---

## Runtime mappings

These are illustrative mappings, not core framework requirements.

### Codex-style clean start

Possible mapping:

- `/finalize-slice` -> fill `starter-pack/templates/slice-finalization-review-template.md`
- `/clean-restart` -> operator opens a fresh session or uses the runtime's clean-start action if available
- `/resume-from-package` -> operator pastes the restart package and a bootstrap prompt based on `starter-pack/templates/restart-bootstrap-prompt-template.md`

Notes:

- a Codex adapter may mention actions like “open a new thread” or `/clear`
- the adapter must still describe these as **runtime-local**, not as AletheIA truth

### Claude Code-style clean start

Possible mapping:

- `/finalize-slice` -> fill the finalization review artifact in repo-native form
- `/clean-restart` -> operator starts a fresh session or uses the runtime's preferred clean-start action
- `/resume-from-package` -> operator starts the next session from the restart package and explicit entrypoint

Notes:

- a Claude Code adapter may describe a fresh chat/session boundary
- the adapter must not depend on runtime hooks or automation to preserve the meaning of the command

### No slash-command support

If the runtime has no slash-command surface, use the same sequence as an operator checklist:

1. finalize the slice with the review template
2. inspect the outcome
3. if the outcome is `recommend-clean-restart`, start a fresh session manually
4. resume from the restart package and bootstrap prompt only

This fallback is equivalent in meaning to the slash-command variant.

---

## Recommended operator sequence

1. `/finalize-slice`
2. inspect the outcome
3. if `recommend-clean-restart`, run `/clean-restart`
4. begin the next slice with `/resume-from-package`

If the outcome is:

- `continue-in-session` -> stay in the current session
- `review-required` -> resolve ambiguity before restart
- `not-ready` -> finish validation or closure first

---

## What this guide does not do

This guide does not:

- define a CLI binary
- define runtime hooks
- define auto-reset behavior
- guarantee native slash-command support
- redefine slice finalization as a tooling problem

It only provides a stable vocabulary for local delivery adapters.
