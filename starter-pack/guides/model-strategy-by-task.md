# Model Strategy by Task

## Goal

This guide helps teams choose a **model capability profile**, a **reasoning depth**, and a **trust / hosting fit** for a task.

It is an operating guide.
It is **advisory-only**.
AletheIA may suggest a fit, but the user may still choose a different model.

---

## Why this guide exists

AletheIA already makes two things explicit:

- `docs/token-policy.md` explains how much context and cost expansion is justified
- the Alpha 5 baseline explains when deeper reasoning is worth the extra effort

What was still missing was a reusable way to answer:

**what kind of model should carry this task, and how much reasoning depth is proportional?**

That answer should depend on:

- the shape of the task
- the risk and ambiguity involved
- the reversibility of the work
- the trust or hosting constraints of the context
- the user's freedom to override the recommendation

---

## What this guide is not

This guide is **not**:

- a universal vendor ranking
- a policy pack
- a runtime router
- a core framework contract
- an automatic override blocker

It is a practical starter-pack layer.

---

## The four decision axes

### 1. Task shape

Start by identifying the dominant task shape:

- housekeeping / formatting / support work
- bounded execution
- planning / decomposition / arbitration
- review / critique / validation
- handoff / compression / restart package generation
- structured risk inference

### 2. Capability profile

Use one of these three profiles:

#### Lightweight helper

Best fit for:
- small reversible tasks
- mechanical cleanup
- basic summarization
- light transformation work

#### Balanced executor

Best fit for:
- bounded implementation
- moderate context assembly
- handoff packaging with some judgment
- execution work that still needs care, but not the deepest reasoning

#### Deep planner / reviewer

Best fit for:
- ambiguous planning
- architectural decomposition
- high-stakes review
- semantic-risk refactors
- structured risk inference

### 3. Reasoning depth

Use reasoning depth as a practical shorthand for how much deliberate work the task should receive.

#### Light

Use when:
- the task is local
- the work is reversible
- correctness is easy to inspect afterward

#### Standard

Use when:
- the task has real but bounded complexity
- the work touches more than one relevant artifact
- some judgment is required, but the downside is still moderate

#### Elevated

Use when:
- ambiguity remains high
- reviewability matters more than speed
- the cost of a wrong decision is meaningful
- the task is hard to validate after the fact

### 4. Trust / hosting constraint

Before choosing a real model, check the boundary posture:

- **externally hosted allowed**
- **hosted but restricted**
- **self-hosted preferred**
- **self-hosted required**

Trust / hosting constraints may override cost or convenience.

---

## Default recommendation matrix

| Task shape | Recommended capability profile | Recommended reasoning depth | Trust / hosting default | Escalate when | Reduce cost when | Override note |
|---|---|---|---|---|---|---|
| Housekeeping / formatting / support work | Lightweight helper | Light | Externally hosted allowed | hidden ambiguity appears or the work stops being local | the task is clearly mechanical | user may deliberately choose a different model |
| Bounded execution | Balanced executor | Standard | Externally hosted allowed, unless local constraints apply | the work becomes cross-boundary, harder to validate, or more semantic than expected | the plan is already stable and the execution is repetitive | user may deliberately choose a different model |
| Planning / decomposition / arbitration | Deep planner / reviewer | Standard or Elevated | Hosted allowed unless project trust rules narrow it | the decision is hard to reverse, ambiguous, or high-impact | the planning question becomes local and mechanical | user may deliberately choose a different model |
| Review / critique / validation | Deep planner / reviewer | Elevated | Hosted but restricted by default when sensitive material is involved | semantic ambiguity, trust-boundary impact, or weak validation design appear | the review becomes a narrow checklist against a stable diff | user may deliberately choose a different model |
| Handoff / compression / restart package generation | Lightweight helper or Balanced executor | Light or Standard | Hosted but restricted when continuity artifacts contain sensitive context | ambiguity is high, the next agent needs stronger interpretation support, or the context is sensitive | the handoff is narrow and already well-bounded | user may deliberately choose a different model |
| Structured risk inference | Deep planner / reviewer | Elevated | Hosted but restricted, or self-hosted preferred/required for sensitive contexts | assumptions are weak, downside is high, or reviewability matters before execution | structured inference is not actually proportional to the slice | user may deliberately choose a different model |

---

## Escalation rules

Escalate capability or reasoning depth when one or more of these appear:

- higher ambiguity than first expected
- lower reversibility
- trust-boundary impact
- validation that is hard to design or hard to trust
- handoff that carries real interpretation risk
- semantic-risk refactor
- review that needs stronger challenge rather than fast execution

Typical moves:

- `Lightweight helper -> Balanced executor`
- `Balanced executor -> Deep planner / reviewer`
- `Light -> Standard -> Elevated`
- `externally hosted allowed -> hosted but restricted -> self-hosted preferred/required`

---

## De-escalation rules

Reduce cost or depth when:

- the plan has already been closed
- the task is now stable and repetitive
- the work became mechanical transformation rather than judgment-heavy reasoning
- the same result can now be achieved with a smaller model class
- the context can be safely handled with a less sensitive hosting posture

AletheIA should not keep a premium model in the loop once the hard part is over.

---


## Usage-plan posture

A useful local next step is to turn the guidance into a **user-approved usage plan** for a session, workstream, or feature slice.

That plan may say things such as:

- which model class is preferred for planning
- which model class is preferred for execution
- which fallback is acceptable
- when a stronger model is justified
- when a cheaper model is enough
- what trust / hosting boundary applies

This is still **advisory-only**.
The plan may guide choices, but it does not remove the user's ability to override them.

The important distinction is:

- a usage plan can make local defaults explicit
- a usage plan does **not** imply automatic model switching in the framework
- a usage plan does **not** make a project-local preference into framework truth

## User override principle

AletheIA suggests.
The user decides.

That means:

- a recommendation is a default, not a lock
- a user may deliberately choose a different model
- the local project may document trade-offs, warnings, or preferences
- this guide does **not** require automatic blocking or automatic routing
- a user-approved usage plan may organize local defaults, but it still does not authorize framework-level auto-routing

Good override examples:

- choosing a stronger model for comfort on a medium-risk planning task
- choosing a cheaper model after the plan is already stable
- choosing a self-hosted option because the context is sensitive

Poor override examples may still happen, but they should be described as **higher-cost**, **lower-quality**, or **trust-riskier** choices — not as impossible choices.

---

## Relationship to local project profiles

This guide stays provider-agnostic on purpose.

Real model names such as:

- Opus
- Sonnet
- GPT
- Gemini
- Llama
- Qwen
- DeepSeek

belong in a **project-local model strategy profile**, because they depend on:

- which models are actually available
- budget ceilings
- trust boundaries
- hosting setup
- tool integrations
- team preference

Use:

- `starter-pack/templates/project-model-strategy-template.md`

for that local translation layer.

---

## Suggested next reading

- `docs/token-policy.md`
- `starter-pack/guides/risk-to-gate-mapping.md`
- `starter-pack/guides/inference-trigger-guidance.md`
- `docs/project-extension-pattern.md`
