# Pilot: Crisis Monitor

## Goal

This document explains how AletheIA was first tested in a real product flow inside the Crisis Monitor project.

It exists to answer four questions:

1. what problem the pilot was trying to solve
2. what was actually tested
3. what was learned from the product field
4. how those learnings returned to the framework

---

## Why Crisis Monitor matters

Crisis Monitor is not the framework itself.

It is the first real proving ground where the framework could be tested against:

- real user-facing flows
- real decision ambiguity
- real approval logic
- real audit surfaces
- real operational tradeoffs

This matters because AletheIA should not mature only through internal framework theory.

It should mature through contact with actual product work.

---

## The problem observed in the product

Before the pilot, the Cris assistant could already:

- route work to a skill
- generate a proposal
- ask for approval
- write audit signals

But an important gap remained:

**execution was becoming more visible than decision.**

In practice, users could still face ambiguity around:

- why a given skill was chosen
- why a proposal required approval
- what exactly still depended on human decision
- whether chat and audit were telling the same story

That made the product a strong first pilot for AletheIA, because the framework is specifically concerned with the space between:

`output -> decision -> governed action`

---

## Pilot hypothesis

If the product makes the decision path more explicit, then:

- the flow becomes easier to trust
- approval becomes easier to interpret
- audit becomes more useful
- AletheIA gets a real product proof without needing a large new capability

---

## Scope of the first pilot slice

The first pilot slice stayed intentionally small.

It focused on:

- proposal explicability
- routing clarity
- approval rationale
- lightweight proof that chat and audit stay coherent

It did **not** try to:

- redesign the Cris UI
- replace approval policy
- create a full new runtime
- generalize the whole framework through one product feature

---

## What was actually tested

### Slice 1 — Decision trace clarity

In the Crisis Monitor product, the first slice made the proposal card more explicit about:

- chosen skill
- routing origin
- routing reason
- next decision needed
- why the proposal requires approval

This proved that a small change in explicability could already produce meaningful value.

### Slice 2 — Functional authenticated smoke

The next slice raised the proof level.

It validated a real local flow:

1. login
2. real proposal creation by Cris
3. audit read
4. controlled reject
5. final audit read

This mattered because it moved the pilot from:

- static or render-level proof

to:

- real product behavior under controlled conditions

---

## What the pilot proved

The pilot proved that AletheIA can add value in a real product without starting from a giant feature.

More specifically, it showed that:

- explicability can be a valid first proof of the framework
- approval rationale adds real clarity
- audit and chat can be checked as parallel surfaces of the same governed flow
- a lightweight product pilot can generate reusable framework learnings

---

## Product-specific vs reusable

### Product-specific

These belong to Crisis Monitor:

- the Cris assistant
- skill names and routing heuristics
- approval semantics for monitoring/editorial actions
- the specific audit UI and product language

### Reusable for AletheIA

These became reusable framework lessons:

- start pilots with low-risk explicability improvements
- validate decision and audit together
- prefer controlled reversible actions for early proof
- turn pilot findings into framework artifacts, not only product notes

---

## How the pilot fed the framework

This pilot directly influenced the public AletheIA repo by reinforcing:

- governance as something visible, not hidden
- token and scope discipline as operating concerns
- durable decision reasoning
- the need to distinguish behavioral enforcement from technical enforcement
- the self-application loop as a real next step

In other words:

the pilot did not stay trapped in product history.
It became input for framework evolution.

---

## Current reading of the pilot

At this stage, the Crisis Monitor pilot should be read as:

- a **real test field**
- a **source of disciplined learnings**
- a **bridge between Alpha 1 and Alpha 2**

It is not yet the final word on AletheIA adoption.

But it is already enough to prove that the framework can be tested in product reality and then converted into framework maturity.

---

## What Alpha 2 should do next with this pilot

The next useful moves are:

1. deepen the pilot write-up when new slices land
2. keep converting product learnings into explicit framework artifacts
3. avoid mixing product-specific residue with reusable framework core
4. use this pilot as one of the main anchors for the Alpha 2 story

---

## Relationship to self-application

The Crisis Monitor pilot and the self-application loop are complementary:

- the pilot provides real field evidence
- self-application provides the conversion logic back into the framework

Together, they form the real center of Alpha 2:

`pilot -> learning -> framework improvement`
