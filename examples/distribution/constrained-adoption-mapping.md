# Constrained Adoption Mapping

This example makes Alpha 6 more tangible through one bounded scenario.

The scenario is intentionally generic:

- the team is adopting AletheIA inside an existing project
- there is more than one working surface
- there are local restrictions on tools, approvals, and model usage
- the framework must remain stable while the project keeps its own local rules

This is **not** an enterprise-ready pack.
It is a concrete Alpha 6 example of packaging and delivery choice.

---

## 1. Selected preset

### Preset

**Existing Project Adoption preset**

### Why

The project already exists.
The immediate need is not to bootstrap from zero.
The immediate need is to:

- introduce the operating layer incrementally
- define the extension boundary clearly
- avoid turning local restrictions into framework truth

### What this preset emphasizes

- `docs/apply-to-existing-project.md`
- `docs/project-extension-pattern.md`
- `starter-pack/README.md`
- starter-pack templates for bounded work

---

## 2. Selected adapters

### Canonical adapter

**Repo-native adapter**

The repository docs remain the canonical meaning source.

### Operational adapter

**Agent instruction adapter**

A compressed operational surface may exist for agents working inside the project, but it must point back to the canonical docs for:

- framework meaning
- boundaries
- validation expectations
- handoff discipline

### Why this combination works

- the repo-native layer keeps the framework inspectable
- the agent-oriented layer improves day-to-day operability
- the compressed layer does not become a hidden fork because the canonical docs stay primary

---

## 3. Selected adoption mode

### Mode

**Standard mode**

### Why

The project is beyond a toy pilot, but it does not need every optional layer activated at once.

Standard mode is enough to justify:

- governance baseline
- project extension discipline
- reusable handoffs where more than one agent is involved
- bounded validation discipline

Standard mode still postpones:

- broad mandatory inference usage
- heavier delivery tooling
- any claim that the framework is already packaged for highly regulated rollout

---

## 4. Project extension boundary

### What stays framework-stable

- operating loop
- governance baseline
- token policy
- project-extension discipline
- handoff structure
- selective risk inference posture

### What becomes project extension

- allowed vs restricted model fleet
- approval rules specific to the project
- local tool allowlists
- storage location for operational artifacts
- local trust-boundary language
- local review and escalation cadence

### Why this matters

This is the main Alpha 6 plugability rule:

**distribution choices can be concrete without moving local restrictions into the framework core.**

---

## 5. Practical delivery read

A practical read of this example is:

1. the team reads the repo-native AletheIA docs as the canonical baseline
2. the project creates a local extension doc for its restrictions and approvals
3. an agent-instruction surface compresses the relevant operating rules for day-to-day work
4. handoffs and risk artifacts remain optional but available when the local context justifies them

This is enough to show packaging shape without requiring CLI tooling.

---

## 6. Why this helps Alpha 6

This example makes three things more tangible:

1. **preset choice** is about project shape, not ideology
2. **adapter choice** is about delivery surface, not framework truth
3. **adoption mode** is about operating depth, not framework versioning

And it reinforces one important boundary:

- local constraints belong in the project extension layer
- they do not redefine the public framework core

---

## 7. Why this is not an enterprise-readiness claim

This example is deliberately smaller than a true regulated-adoption package.

It does **not** claim:

- enterprise-ready rollout
- regulated-domain completeness
- finished trust-boundary starter packs
- packaged support for complex corporate SDLCs

It only proves that Alpha 6 can become more tangible without overclaiming readiness.
