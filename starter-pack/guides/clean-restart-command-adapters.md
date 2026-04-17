# Clean Restart Command Adapters

## Goal

Define a small logical command vocabulary for teams that want to test clean thread restart after slice finalization.

These commands are **adapter vocabulary**, not framework truth.
They may become slash commands in a runtime that supports them, or remain a simple operator checklist in a runtime that does not.

---

## Why this layer exists

Teams often want something like:

- `/finalize-slice`
- `/clear`
- `/new`
- `/resume`

The risk is that the runtime command becomes the whole story.

AletheIA should invert that.
The command is only useful if the slice has already been closed well enough for a clean restart to be healthy.

---

## Logical adapter vocabulary

### `/finalize-slice`

Meaning:

- run the slice-finalization review
- decide whether the slice is ready to stop
- emit or update the restart package
- produce one of these outcomes:
  - `continue-in-session`
  - `recommend-clean-restart`
  - `review-required`
  - `not-ready`

Minimum expectations:

- validation status is explicit
- next action is explicit
- restart package is compact enough to replace transcript replay

### `/clean-restart`

Meaning:

- start the next slice in a fresh thread or session
- use only the restart package and minimal bootstrap context
- do this **only** after `recommend-clean-restart`

Boundary:

- this command does **not** mean AletheIA controls hidden runtime memory
- it only means the operator should now prefer a clean start over continued carryover

### `/resume-from-package`

Meaning:

- bootstrap the next slice from the restart package
- use the restart bootstrap prompt and minimal refs
- avoid transcript replay as the default path

This command is especially useful when the runtime has no native slash-command support and the workflow is still manual.

---

## Runtime mapping examples

### Codex-style mapping

Possible local mapping:

- `/finalize-slice` -> fill the review artifact and emit restart package
- `/clean-restart` -> operator starts a new clean session, possibly using a local action such as `/clear` or opening a fresh thread
- `/resume-from-package` -> operator pastes the restart package plus the bootstrap prompt

Important:

- `/clear` is a local runtime convenience, not an AletheIA contract

### Claude Code-style mapping

Possible local mapping:

- `/finalize-slice` -> fill the review artifact and emit restart package
- `/clean-restart` -> operator starts a fresh session or thread in the local workflow
- `/resume-from-package` -> operator provides the restart package and minimal refs to begin the next bounded slice

Important:

- the meaning should remain identical even if the runtime does not expose a specific reset command

---

## Checklist fallback when no slash commands exist

If the runtime supports no custom commands, teams can still use this sequence:

1. **Finalize the slice**
   - confirm validation status
   - confirm next action
   - produce restart package
2. **Decide the outcome**
   - continue
   - clean restart
   - review required
   - not ready
3. **Start clean if recommended**
   - open a fresh thread or session
4. **Resume only from the package**
   - use the restart bootstrap prompt
   - load only minimal refs
   - avoid transcript replay

Semantically, this is equivalent to the slash-command version.

---

## Stop lines

Do **not** use this layer to imply that AletheIA now provides:

- runtime automation hooks
- session lifecycle APIs
- memory/cache deletion
- provider-native command ownership
- benchmark-backed claims about token savings without evidence

Keep it:

- manual-first
- docs-first
- provider-agnostic
- restart-package-centered
