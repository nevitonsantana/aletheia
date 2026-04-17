# Restart Bootstrap Prompt Template

Use this template after a slice has already been finalized and a clean restart has been recommended.

```text
Continue the project with a fresh thread for the next bounded slice.

Read only:
- the restart package
- the active slice / next-slice entrypoint
- any minimal governing refs listed there

Current objective:
{{next_action}}

Primary entrypoint:
{{resume_entrypoint}}

Known constraints:
{{known_constraints}}

Do not replay the old transcript by default.
If context still seems missing, ask only for the smallest missing detail that is not already explicit in the restart package.
```
