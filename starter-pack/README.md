# Starter Pack

This folder contains the reusable operating materials that help teams apply AletheIA with discipline.

It is intentionally smaller than the framework core.

The goal is to provide a practical baseline for:

- task framing
- context discipline
- handoffs
- branch isolation
- quality gates
- durable decisions
- advisory model-strategy guidance

Start here if you want the operating method around the framework, not only the technical core.


## Adoption note

If you are starting from an existing repository rather than a blank setup, read:

- `docs/getting-started.md`
- `docs/apply-to-existing-project.md`
- `CONTRIBUTING.md`


## New template

If you are adopting AletheIA inside a real project and need to make the local layer explicit, use:

- `starter-pack/templates/project-extension-template.md`


## Alpha 4 baseline

The current practical Alpha 4 handoff baseline now includes:

- `docs/agent-handoffs.md`
- `starter-pack/guides/agent-handoff-generation.md`
- `starter-pack/templates/agent-handoff-template.md`
- `docs/project-handoff-conventions.md`
- `docs/handoff-capture-pattern.md`

Use this set when you need model-agnostic continuity between agents without relying on hidden thread memory.


## Alpha 5 baseline

If you are exploring the current Alpha 5 structured-risk-inference baseline for higher-risk work, read:

- `docs/structured-risk-inference.md`
- `starter-pack/templates/inference-artifact-template.md`
- `starter-pack/guides/inference-trigger-guidance.md`
- `starter-pack/guides/inference-artifact-generation.md`
- `docs/inference-pilot-scenarios.md`


## Model strategy guidance

If you want practical guidance for matching task shape, capability profile, reasoning depth, and trust / hosting constraints, read:

- `starter-pack/guides/model-strategy-by-task.md`
- `starter-pack/templates/project-model-strategy-template.md`
- `examples/model-strategy/README.md`

This guidance is advisory-only.
AletheIA may suggest a fit, but the user may still choose a different model.

## Current operational-composition baseline

If you want to make bounded work more tangible without changing the core contracts, read:

- `docs/work-slice-pattern.md`
- `starter-pack/templates/work-slice-template.md`
- `starter-pack/guides/risk-to-gate-mapping.md`
- `examples/work-slices/standard-slice/README.md`
- `examples/handoffs/compact-reviewable-handoff.md`
- `examples/handoffs/high-stakes-handoff.md`
- `docs/iterative-maintenance-governance.md`
- `starter-pack/guides/round-based-maintenance.md`
- `examples/iterative-maintenance/three-round-loop/README.md`

This baseline is intentionally smaller than the core contracts and mainly reinforces Alpha 4 continuity plus Alpha 5 validation posture.
It now also makes iterative maintenance rounds and regression-aware continuation more tangible without changing the core contracts.

Taken together, the current starter-pack now covers both:

- advisory model strategy for choosing fit-for-task model profiles
- operational maintenance guidance for carrying bounded work safely across repeated rounds

## Experimental workspace context routing

If you want to test a filesystem-based context-routing pattern as a local experiment, read:

- `starter-pack/experiments/workspace-context-routing/README.md`
