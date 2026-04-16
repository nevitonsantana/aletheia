# Clean Restart Command Adapter Example

This example shows how a team may expose the existing slice-finalization flow through adapter-style commands without turning AletheIA into a runtime platform.

---

## Situation

- the slice was validated
- the next action is explicit
- the restart package is compact
- the next slice should not inherit stale execution context

The finalization outcome is:

- `recommend-clean-restart`

---

## Logical command sequence

### 1. `/finalize-slice`

Meaning:

- fill the finalization review
- emit the restart package
- confirm that transcript replay is not needed

Result:

- finalization outcome = `recommend-clean-restart`

### 2. `/clean-restart`

Meaning:

- the operator should now begin a fresh session rather than continue inside the stale thread

### 3. `/resume-from-package`

Meaning:

- the next slice starts from the restart package only

---

## Codex-style mapping

- `/finalize-slice` -> fill `starter-pack/templates/slice-finalization-review-template.md`
- `/clean-restart` -> open a fresh session or use the runtime's clean-start action if available
- `/resume-from-package` -> paste the restart package and a prompt based on `starter-pack/templates/restart-bootstrap-prompt-template.md`

Illustrative note:

- a local adapter may mention `/clear`, but the framework still treats that as runtime-local behavior

---

## Claude Code-style mapping

- `/finalize-slice` -> fill the finalization review artifact
- `/clean-restart` -> open a fresh session
- `/resume-from-package` -> continue from the restart package and explicit entrypoint only

---

## No-slash fallback

If the runtime has no slash-command support, the operator may execute the same flow as plain steps:

1. finalize the slice
2. inspect the outcome
3. start a clean session if recommended
4. resume from the restart package and bootstrap prompt only

---

## Example restart bootstrap prompt

```text
Continue the project from a clean session.

Read only:
- the restart package below
- docs/feature-review-notes.md
- docs/DECISIONS.md if referenced by the package

Do not replay old transcript history unless the restart package proves insufficient.

Objective:
Start the review-only continuation of the next slice.
```
