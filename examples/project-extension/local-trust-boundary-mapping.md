# Local Trust-Boundary Mapping Example

## Goal

This example shows a small local mapping for a constrained project.
It demonstrates posture, not policy.

---

## Example posture

### Data classes

- public
- internal
- restricted

### Model posture

- hosted models allowed for public work
- hosted models allowed for low-risk internal planning only
- local runtime required for restricted context

### Tool posture

- read tools broadly allowed in bounded lanes
- write tools restricted to approved execution lanes
- outbound tools disabled for restricted context
- destructive tools always require human gate

---

## Example lane mapping

### Lane A — public planning

- data class: public
- hosted model allowed: yes
- read tools allowed: yes
- write tools allowed: no
- review posture: bounded self-check

### Lane B — internal review

- data class: internal
- hosted model allowed: maybe, if local posture permits
- read tools allowed: yes
- write tools allowed: only if the lane explicitly allows them
- review posture: local review may be required depending on risk

### Lane C — restricted execution

- data class: restricted
- hosted model allowed: no
- local runtime required: yes
- outbound tools allowed: no
- human approval required: yes

---

## Why this example matters

This kind of mapping makes it easier to answer:

- why a given model was acceptable or not
- why a tool was blocked or allowed
- why the lane was suggestion-only instead of execution-capable

That clarity is useful in constrained environments,
but it still belongs in the local layer rather than the framework core.
