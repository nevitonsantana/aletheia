# Approved Usage Plan Example

> Illustrative local example.
> Not a framework default.
> Not an authorization for automatic model switching.

This example shows how a team may agree on a short-lived usage plan before starting a bounded piece of work.

---

## Context

The team is about to implement a medium-sized feature with:

- some ambiguity in planning
- bounded implementation work afterward
- a final review step
- normal user override still allowed

---

## Agreed local usage plan

### Planning

Preferred default:
- Deep planner / reviewer profile

Local translation example:
- premium hosted planning model when available
- balanced hosted fallback if the planning question narrows quickly

### Execution

Preferred default:
- Balanced executor profile

Local translation example:
- mid-cost hosted execution model
- self-hosted bounded executor when trust posture requires it

### Review

Preferred default:
- Deep planner / reviewer profile

Local translation example:
- stronger hosted reviewer for semantic review
- restricted self-hosted reviewer when the material should not leave the trust boundary

### Handoff / compression

Preferred default:
- Lightweight helper or Balanced executor profile

Local translation example:
- cheaper hosted summarizer for normal context
- self-hosted summarizer for sensitive continuity artifacts

---

## Why this is useful

A usage plan can help the team align on:

- where to spend more model quality
- where to reduce cost
- where trust / hosting posture matters more than convenience
- which fallbacks are acceptable before the work begins

---

## Why this is still advisory-only

Even with this plan:

- the user may still choose another model
- the project may warn about trade-offs
- the framework still does not auto-route models
- the plan remains local to this work item, not framework truth
