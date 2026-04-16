# Restart Bootstrap Prompt

Use this template after a slice closes with `recommend-clean-restart`.

The prompt should rely on:

- the restart package
- the next action
- the resume entrypoint
- the governing-context refs when present

It should **not** rely on transcript replay by default.

---

## Template

```text
Continue the project from a clean session.

Read only:
- the restart package below
- the resume entrypoint
- the governing-context refs listed in the package, if present

Do not replay old transcript history unless the restart package proves insufficient.

Objective:
{{next_action}}

Resume entrypoint:
{{resume_entrypoint}}

Restart package:
{{restart_package_block}}
```

---

## Notes

- if the restart package is not self-contained enough, fix the package rather than normalizing transcript replay
- if the package references governing-context docs, load only the minimum needed refs
- if the previous slice ended with `review-required` or `not-ready`, do not use this template yet
