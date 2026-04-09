# AletheIA

**AletheIA** is an operating framework for AI-assisted work.

It helps teams coordinate tasks, context, memory, skills, governance, validation, and learnings **without letting raw model output act directly on the system**.

In simple terms:

`model or agent output -> AletheIA -> execution`

---

## Why the name AletheIA

The name combines **Aletheia** — the idea of truth as something brought into the open rather than left hidden — with **IA**, signaling the framework's focus on AI-assisted work.

Conceptually, the name points to the framework's main intention:

- make reasoning more explicit
- make decisions more reviewable
- make validation and learnings less hidden
- keep AI work from moving straight from output to action without an operating layer

In that sense, AletheIA is not about treating AI output as truth.
It is about creating the conditions for AI-assisted work to become more inspectable, governable, and revealable before execution.

---

## Why AletheIA exists

Many AI workflows still follow a fragile pattern:

`prompt -> output -> execution`

That can be fast, but it is often weak in:

- traceability
- scope control
- policy enforcement
- quality gates
- reusable learnings

AletheIA introduces an explicit operating layer between output and action.

Its goal is not to slow teams down for the sake of ceremony.

Its goal is to make AI-assisted work:

- clearer
- safer
- more predictable
- more reusable across projects

---

## What this is

AletheIA is:

- a framework
- provider-agnostic by design
- focused on safe and explainable AI-assisted work
- built to be reusable across projects
- designed for structured decision-making before execution

## What this is not

AletheIA is not:

- a chatbot
- an app
- a wrapper around a single LLM
- a product-specific toolkit
- a system that assumes automation is always the right answer

---

## Core operating loop

AletheIA works through a controlled loop:

`intent -> context -> decision -> execution -> validation -> learning`

This means the framework helps answer questions such as:

- What exactly is the task?
- What context is truly needed?
- What decision is being made?
- Why is this allowed, blocked, or escalated?
- What validation happened before closure?
- What should be learned from success or failure?

---

## What the first public alpha proves

The current public alpha is meant to prove that:

- an input can become a structured decision
- governance can block unsafe or poorly framed closure
- failed validation can generate reusable learnings
- the framework can stay small, inspectable, and deterministic
- the core can be reused outside its original pilot project

---

## Repository structure

- `engine/` — minimal deterministic kernel, governance, and learnings helpers
- `schemas/` — JSON schemas for framework contracts
- `policies/` — governance packs and policy definitions
- `examples/` — canonical examples and golden fixtures
- `tests/` — contract, golden, e2e, and learning-oriented checks
- `starter-pack/` — reusable operating guides, checklists, and templates
- `docs/` — architecture, roadmap, pilot narrative, and migration notes

---

## Initial examples

The alpha starts with a few small examples that make the framework tangible:

- `hello-world` — the smallest end-to-end path
- `low-confidence-review` — when ambiguity should stop direct execution
- `high-risk-human-gate` — when risk requires explicit human approval
- `learning-from-failed-validation` — when failed closure should also produce reusable learning
- `governance` — process-oriented rule evaluation using facts and a policy pack

---

## Design principles

1. Clarity over speed
2. Control over automation
3. Consistency over convenience
4. Reuse before duplication
5. Learnings must be reviewable
6. The framework should stay inspectable and debuggable

---

## Current status

This repository is the first public alpha draft of AletheIA.

It was born from real operational work inside the `Crisis Monitor` project and then extracted into a standalone reusable framework.

Today, this public draft already contains:

- an Alpha 1 baseline for governance, token discipline, durable decisions, enforcement clarity, quality, and learnings
- an explicit Alpha 2 bridge for self-application, pilot conversion, and project extension, now reinforced by real-world Crisis Monitor validation
- an Alpha 3 adoption baseline for getting started, existing-project application, contribution guidance, and starter-pack reuse
- an Alpha 4 handoff baseline for model-agnostic restart packages, project conventions, and semi-automated handoff capture
- an Alpha 5 experimental baseline for structured risk inference in higher-risk work, including concrete example artifacts
- an Alpha 6 distribution baseline for presets, adapters, adoption modes, and cross-surface delivery mappings
- a current operational-composition baseline for work slices, risk-to-gate mapping, stronger restart-package examples, and optional filesystem context-routing experiments
- an early Alpha 7 bootstrap-and-delivery baseline for future tooling contracts that still remains outside the core

In practical terms, that currently includes:

- core contracts
- a minimal kernel
- a governance pack
- an explicit token policy
- a small executable governance baseline
- a lightweight durable decision discipline
- an explicit boundary between behavioral and technical enforcement
- a quality baseline
- a first learnings path
- a reusable starter-pack slice
- an advisory-only model-strategy guidance slice for task shape, capability profile, reasoning depth, and trust / hosting fit
- a first structured risk inference slice
- a first iterative-maintenance governance slice for round-based continuation, regression-aware gates, reusable learning across rounds, and a clearer proportional pattern of proof, contract, health, alert, investigation, and summary
- concrete example artifacts for bounded semantic-risk scenarios
- a first concrete distribution baseline for packaging shape, delivery surface, adoption depth, and meaning preservation across surfaces
- a lightweight operational-composition baseline for work slices, risk-to-gate mapping, compact handoff continuity, iterative maintenance guidance, and optional filesystem context-routing experiments
- a first Alpha 7 tooling baseline across principles, boundaries, output shapes, generator contract, and output contract

---

## Reading order

If this is your first time here, start with:

1. `docs/getting-started.md`
2. `docs/00-overview.md`
3. `docs/architecture.md`
4. `docs/governance.md`
5. `docs/token-policy.md`
6. `starter-pack/guides/model-strategy-by-task.md`
7. `docs/durable-decisions.md`
8. `docs/enforcement-boundaries.md`
9. `docs/quality.md`
10. `docs/self-application.md`
11. `docs/pilot-crisis-monitor.md`
12. `docs/pilot-conversion.md`
13. `examples/pilot-conversion/crisis-monitor-real-world-validation.md`
14. `docs/project-extension-pattern.md`
15. `docs/apply-to-existing-project.md`
15. `CONTRIBUTING.md`
16. `starter-pack/`
17. `starter-pack/templates/project-extension-template.md`
18. `starter-pack/templates/project-model-strategy-template.md`
19. `docs/agent-handoffs.md`
20. `starter-pack/guides/agent-handoff-generation.md`
21. `starter-pack/templates/agent-handoff-template.md`
22. `docs/project-handoff-conventions.md`
23. `docs/handoff-capture-pattern.md`
24. `docs/work-slice-pattern.md`
25. `starter-pack/templates/work-slice-template.md`
26. `starter-pack/guides/risk-to-gate-mapping.md`
27. `docs/structured-risk-inference.md`
28. `starter-pack/templates/inference-artifact-template.md`
29. `starter-pack/guides/inference-trigger-guidance.md`
30. `starter-pack/guides/inference-artifact-generation.md`
31. `docs/inference-pilot-scenarios.md`
32. `examples/work-slices/standard-slice/README.md`
33. `examples/handoffs/compact-reviewable-handoff.md`
34. `examples/handoffs/high-stakes-handoff.md`
35. `examples/structured-risk-inference/README.md`
36. `examples/model-strategy/README.md`
37. `examples/`

---

## Near-term direction

The next steps are:

- keep the current Alpha 6 baseline coherent without losing the Alpha 5 inference baseline, the Alpha 4 handoff baseline, or the Alpha 3 adoption gains
- keep validating the Crisis Monitor pilot and adjacent real slices
- keep converting pilot learnings into framework improvements with the Crisis Monitor pilot as the strongest current Alpha 2 evidence
- keep using AletheIA to improve AletheIA itself
- keep Alpha 5 proportional, selective, and grounded in bounded semantic-risk scenarios
- keep the operational-composition baseline lightweight, teachable, and clearly outside the core contracts
- keep the new model-strategy guidance advisory-only, provider-agnostic in the framework, and translated locally by each project
- keep iterative-maintenance guidance focused on round legibility, regression-aware continuation, reusable learning, and proportional proof/health reads rather than benchmark imitation
- keep experimental workspace context routing optional, inspectable, and clearly non-canonical
- keep Alpha 6 focused on distribution clarity rather than tooling promises
- keep Alpha 7 small, bounded, and tooling-light even as its baseline becomes clearer
- let future domain packs remain future-facing layers rather than near-term core work

---

## Current phase map

- Alpha 1 established the governance and validation baseline.
- Alpha 2 established the pilot, self-application, and conversion bridge.
- Alpha 3 is making the framework easier to adopt and contribute to.
- Alpha 4 is making inter-agent continuity explicit, reusable, and more operational.
- Alpha 5 now provides an experimental baseline for decision-quality in higher-risk work.
- Alpha 6 now provides a first concrete distribution baseline for presets, adapters, adoption modes, and delivery mappings.
- Alpha 7 now includes bootstrap principles, delivery-tooling boundaries, output examples, a first future-facing generator contract, and a first future-facing delivery output contract for optional automation.
- A current operational-composition baseline now makes bounded work, restartable handoffs, risk-sensitive validation, iterative maintenance, and regression-aware continuation more tangible without expanding the core contracts.
- The starter-pack now also includes advisory-only model-strategy guidance for matching task shape, capability profile, reasoning depth, and trust / hosting constraints without turning model choice into framework enforcement.

---

## First Alpha 2 bridge

The first explicit bridge into Alpha 2 is:

- `docs/self-application.md`
- `docs/pilot-crisis-monitor.md`
- `docs/pilot-conversion.md`
- `docs/project-extension-pattern.md`

Together, these documents explain how AletheIA should evolve itself, learn from pilots, and preserve a clear boundary between framework core and local project extensions.

The current Alpha 3 adoption baseline after this bridge is:

- `docs/getting-started.md`
- `docs/apply-to-existing-project.md`
- `CONTRIBUTING.md`
- `starter-pack/templates/project-extension-template.md`

The first Alpha 4 handoff baseline now adds:

- `docs/agent-handoffs.md`
- `starter-pack/guides/agent-handoff-generation.md`
- `starter-pack/templates/agent-handoff-template.md`
- `docs/project-handoff-conventions.md`
- `docs/handoff-capture-pattern.md`

The current Alpha 5 experimental baseline now adds:

- `docs/structured-risk-inference.md`
- `starter-pack/templates/inference-artifact-template.md`
- `starter-pack/guides/inference-trigger-guidance.md`
- `starter-pack/guides/inference-artifact-generation.md`
- `docs/inference-pilot-scenarios.md`
- `examples/structured-risk-inference/README.md`

---

## Current Alpha 5 and Alpha 6 baselines, plus future direction

The current and next layers should stay clearly separated by role:

- **Alpha 5** — an experimental baseline for decision-quality through structured, evidence-oriented inference in higher-risk work
- **Alpha 6** — a first concrete distribution baseline for packaging the same framework meaning across environments
- **Alpha 7** — optional bootstrap and delivery tooling after the distribution model is already stable

The current Alpha 6 baseline now adds:

- `docs/distribution-presets-adapters.md`
- `docs/preset-taxonomy.md`
- `docs/adapter-taxonomy.md`
- `docs/adoption-mode-guidance.md`
- `docs/delivery-mapping-examples.md`

A separate future track will also shape reusable domain governance packs.
The first planned packs in that track are:

- **Web App Security & Trust Boundaries Pack**
- **AI Agent Security & Prompt Injection Pack**

These future phases and domain packs are about extending AletheIA's reach and delivery discipline.
They are not about redefining the framework core.

The domain packs should sit between the reusable framework core and project-local rules:

`AletheIA core -> domain governance pack -> project extension`

See also:

- `docs/structured-risk-inference.md`
- `starter-pack/templates/inference-artifact-template.md`
- `docs/distribution-presets-adapters.md`
- `docs/preset-taxonomy.md`
- `docs/adapter-taxonomy.md`
- `docs/adoption-mode-guidance.md`
- `docs/delivery-mapping-examples.md`
- `docs/bootstrap-principles.md`
- `docs/delivery-tooling-boundaries.md`
- `docs/bootstrap-output-examples.md`
- `docs/domain-governance-packs.md`
- `docs/web-app-security-trust-boundaries.md`
- `docs/ai-agent-security-prompt-injection.md`

---

## Contribution entrypoint

If you want to contribute to AletheIA, start with:

- `CONTRIBUTING.md`

This is the fastest way to understand what kinds of changes belong in the framework core, what should stay local, and how to contribute without inflating the project.

---

## Minimal governance baseline

Alpha 1 now includes a small executable governance check:

- `bash scripts/check-governance.sh`

This is intentionally modest.

It does not try to be a heavy enforcement layer yet.
It only proves that AletheIA can move from governance prose into a small technical baseline.
