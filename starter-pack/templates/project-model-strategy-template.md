# Project Model Strategy Template

Use this template when a project wants to translate AletheIA's provider-agnostic guidance into a real local model fleet.

This template is **recommended**, not mandatory.
It documents local defaults and trade-offs.
It does not remove the user's ability to choose a different model.

---

## Project identity

### Project name

### Team or user scope

### Last updated

---

## Local model inventory

Fill one row per model or runtime that is actually available.

| Model label | Provider / runtime | Hosted vs self-hosted | Allowed data class / trust boundary | Cost posture | Latency posture | Context posture | Best-fit task shapes | Max recommended reasoning depth | Notable weaknesses |
|---|---|---|---|---|---|---|---|---|---|
| Example: Planning premium | Example provider | hosted | public + internal docs only | high | medium | large | planning, review | Elevated | expensive for routine execution |
| Example: Execution default | Example provider | hosted | public + normal working context | medium | fast | moderate | bounded execution, handoffs | Standard | less reliable for high-stakes arbitration |
| Example: Sensitive local runtime | local runtime | self-hosted | restricted / sensitive only | low-medium | medium | moderate | summarization, handoff, restricted-context tasks | Standard | weaker on ambiguous planning |

---

## Capability mapping

Map the real fleet into the AletheIA capability profiles.

### Lightweight helper

Recommended local models:

### Balanced executor

Recommended local models:

### Deep planner / reviewer

Recommended local models:

---

## Local routing guidance

### Recommended default for planning

### Recommended default for execution

### Recommended default for review

### Recommended default for handoff / compression

### Recommended default for structured risk inference

### Escalation triggers

Examples:
- ambiguity stayed high
- trust boundary tightened
- review risk increased
- validation became harder than expected

### Fallback triggers

Examples:
- premium model unavailable
- budget ceiling hit
- task became repetitive
- trust boundary no longer allows the preferred hosted option

### Trust / hosting restrictions

State any project-local constraints such as:
- public-only context for externally hosted models
- self-hosted required for customer-sensitive material
- no third-party model for certain artifacts

---


## Optional session or feature usage plan

Use this section when a team wants to agree on a short-lived plan before work starts.

Examples:
- planning for this feature should default to the deep planner / reviewer profile
- bounded implementation should default to the balanced executor profile
- handoff packaging may use a cheaper or self-hosted option when trust posture requires it
- fallback is acceptable when the preferred model is unavailable or disproportional

### Planning default for this work

### Execution default for this work

### Review default for this work

### Handoff / compression default for this work

### Fallbacks allowed for this work

### Trust / hosting posture for this work

### Reminder

This usage plan is still advisory.
It helps the team align before the work starts, but it does not remove user override.

---

## User override policy

This profile is **recommended**, not obligatory.

### Override principle

The user may choose a different model.

### Benign overrides

Examples:
- stronger model than recommended for comfort or speed of convergence
- cheaper model after the plan is already stable
- self-hosted model for sensitive summarization

### Higher-cost or higher-risk overrides

Examples:
- premium model for routine formatting work
- weak model for high-ambiguity planning
- externally hosted model for material that the project would rather keep restricted

### Alert-only vs block

If the project wants to react to overrides, state the posture clearly.

Examples:
- alert only
- warn on trust mismatch, but do not block
- never auto-block in the local workflow

---

## Notes

Use this template to make local model strategy explicit.
Do not treat it as a universal framework rule.
Replace any example fleet with the models the project actually has.
