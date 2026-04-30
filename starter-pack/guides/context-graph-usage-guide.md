# Context Graph Usage Guide

## Goal

Give practical rules for when and how to use a code-structure graph (such as `code-review-graph`) inside an AletheIA slice.

The underlying principle is proportional access: the graph earns its use by reducing irrelevant reads and avoiding missed dependencies. If it does not do either, skip it.

---

## Graph operations

This guide uses five operations, named consistently with the `code-review-graph` interface:

| Operation | What it answers |
|---|---|
| `minimal-context` | Smallest set of files needed to understand a task |
| `impact-radius` | All files structurally affected by a change |
| `review-context` | Files a reviewer needs to evaluate a PR or diff |
| `traversal` | Dependency path between two specific nodes |
| `semantic-search` | Files most relevant to a concept or query |

---

## Usage rules by task shape

### Bug in a known file

**Default: do not use the graph.**

Read the file directly. If the fix reveals an unexpected dependency, then use `traversal` or `minimal-context` to locate it. Do not start with a graph query on a one-file bug.

**Overhead signal:** if the graph query takes longer than the direct read would have, record it as `graph_helpfulness: low`.

### Bug with uncertain dependencies

**Optional: use `minimal-context`.**

When the first read leaves the dependency unclear, run `minimal-context` before expanding further. This prevents unstructured expansion across unrelated files.

Steps:

1. Read the known file
2. If dependency is unclear, run `minimal-context`
3. Read only the files the query returns that are relevant
4. Do not read the full suggestion list by default

### Refactor touching multiple files

**Use `impact-radius` before execution and before validation.**

Before starting: run `impact-radius` to know the full structural footprint. Use this to inform planning depth (see `docs/planning-depth-profiles.md`). A large radius signals `Standard` or `High-Assurance` depth.

Before validating: run `impact-radius` again to confirm all affected files were reviewed. Record delta.

Steps:

1. Run `impact-radius` before writing any code
2. Record `blast_radius_size`
3. If radius is large (more than ~10 files): review gate 3 before proceeding
4. After completing the refactor, re-run to verify coverage
5. Record `files_suggested_by_graph` vs `files_actually_read`

### PR review

**Use `minimal-context` → `review-context` → selective read.**

Steps:

1. Run `minimal-context` for the changed files
2. Run `review-context` to get the reviewer's minimum context
3. Read selectively from the returned list — do not read the full list without filtering
4. Note gaps (files the graph did not suggest but that seem relevant based on reading)

**Precision warning:** `code-review-graph` favors recall. Expect false positives in the suggestion list. Use your own judgment to filter before reading.

### Architecture exploration or onboarding

**Use overview, communities, hubs, bridges, and gaps.**

These operations give structural understanding without requiring specific query files. Useful at the start of a new project or before designing a significant change.

Steps:

1. Run a broad overview query
2. Identify hubs (high-centrality nodes) and communities (clusters of related files)
3. Identify bridges (files that connect clusters)
4. Identify gaps (areas with no connection to the proposed change)

This is the highest-value use case for the graph. Record findings as context in the slice record before proceeding.

### Product or governance decision

**Do not use the graph as decision evidence.**

The graph informs technical impact only. It cannot tell you whether a product direction is right, whether a risk is acceptable, or whether a stakeholder decision is sound. Use it to estimate technical scope if needed, then hand the decision to the appropriate human gate.

---

## Measuring helpfulness

After each graph use, record three objective signals in the slice telemetry:

| Signal | How to measure |
|---|---|
| `files_suggested_by_graph` | Count of files returned by the query |
| `files_actually_read` | Count of files actually opened and read |
| `blast_radius_size` | Count of files in the `impact-radius` result |

Derive two judgment fields:

| Field | Values | Guidance |
|---|---|---|
| `graph_helpfulness` | `low / medium / high` | Low if you read fewer than 30% of suggestions; high if suggestions matched what you needed |
| `graph_overhead` | `low / medium / high` | High if the query added steps without reducing reads or clarifying scope |

Record these in the test record template. After 3–6 slices, use them to evaluate whether the graph is worth keeping in the workflow.

---

## When to skip the graph entirely

Skip the graph when:

- the file is known and the change is local
- the slice is already in execution and a graph query would interrupt momentum without adding new information
- the task is governance, product, or communication — not code structure
- you already ran `impact-radius` this round and the question has not changed
- the project is **Next.js with a shared design system** — F1=0.041 for impact accuracy; 2-hop traversal reaches the entire project for any UI file (73–97% false positives observed in controlled tests)
- the change touches **CSS global or design tokens** — blast radius is always maximal and does not discriminate which consumers were actually affected

The graph is not a mandatory step. It is a conditional tool.

---

## Gate interaction

| Gate | Graph input | What to do |
|---|---|---|
| Gate 1 (context minimum) | Graph confirms files found | Confirm, then read selectively |
| Gate 2 (decision clear) | Graph shows unexpected dependencies | Return to `tighten` before proceeding |
| Gate 3 (risk mapped) | Large `blast_radius_size` | Increase planning depth; do not treat coverage as complete |
| Gate 4 (handoff usable) | Graph-identified files and open dependencies | Include in restart package |
| Gate 5 (runtime fit) | Graph adds too much overhead for the slice | Consider lighter approach or skip graph |

---

## Suggested next reading

- `docs/context-graph-integration.md`
- `docs/readiness-gates-spec.md`
- `docs/planning-depth-profiles.md`
- `starter-pack/templates/context-graph-test-record-template.md`
- `examples/resource-aware-operations/context-graph-adapter-example.md`
