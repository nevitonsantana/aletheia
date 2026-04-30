# Context Graph Adapter Example

## Goal

Show what a runtime adapter record looks like when a code-structure graph was used during a slice.

This extends the base runtime adapter contract (`docs/runtime-adapter-contract.md`) with four graph-specific fields. Everything else follows the same shape.

---

## Example A — Refactor with graph (graph helped)

Task: rename and reorganize a shared utility used in multiple modules.

```yaml
slice_id: crisis-monitor-util-refactor-round-1
project_id: crisis-monitor
round_id: 1
task_shape: bounded-execution
risk_posture: medium
planning_depth: standard

# base context posture
cold_boot_budget: moderate
exploration_events: 2
expansion_events: 1
expansion_reason_present: yes
delegation_events: 0

# runtime / agent
runtime_id: claude-code
agent_class: coding-agent
capability_profile: balanced-executor
reasoning_depth: standard
trust_hosting_posture: externally-hosted-allowed

# review / retry
retry_count: 0
retry_pattern: none
validation_outcome: validated
human_review_level: light-review
manual_rescue_required: no

# restart
handoff_required: no
handoff_quality: not-needed
restart_burden: low

# graph-specific fields
context_source: code-graph
graph_operation: impact-radius
files_suggested_by_graph: 11
files_actually_read: 7
blast_radius_size: 11

# judgment
graph_helpfulness: high
graph_overhead: low
```

**Why this is a good result:** the graph surfaced 11 affected files before execution began. The agent read 7 of them (4 were clearly irrelevant after inspection). No dependency was missed. Without the graph, at least 2 files would likely have been skipped, requiring a second round.

---

## Example B — Bug fix with graph (graph added overhead)

Task: fix a null reference error in a known component.

```yaml
slice_id: crisis-monitor-null-fix-round-1
project_id: crisis-monitor
round_id: 1
task_shape: bounded-execution
risk_posture: low
planning_depth: lite

# base context posture
cold_boot_budget: minimal
exploration_events: 2
expansion_events: 0
expansion_reason_present: no
delegation_events: 0

# runtime / agent
runtime_id: claude-code
agent_class: coding-agent
capability_profile: balanced-executor
reasoning_depth: standard
trust_hosting_posture: externally-hosted-allowed

# review / retry
retry_count: 0
retry_pattern: none
validation_outcome: validated
human_review_level: none
manual_rescue_required: no

# restart
handoff_required: no
handoff_quality: not-needed
restart_burden: low

# graph-specific fields
context_source: mixed
graph_operation: minimal-context
files_suggested_by_graph: 8
files_actually_read: 2
blast_radius_size:

# judgment
graph_helpfulness: low
graph_overhead: medium
```

**Why this is a weak result:** the file was already known. The graph returned 8 candidates, only 2 of which were read. The fix was in the first file. The graph query added one exploration event without reducing scope. Direct read would have been faster. This slice supports the rule: skip the graph for one-file bugs in known locations.

---

## Example C — PR review with graph (mixed result)

Task: review a pull request touching the ingest pipeline before merge.

```yaml
slice_id: crisis-monitor-pr-review-round-1
project_id: crisis-monitor
round_id: 1
task_shape: review
risk_posture: medium
planning_depth: standard

# base context posture
cold_boot_budget: moderate
exploration_events: 3
expansion_events: 2
expansion_reason_present: yes
delegation_events: 0

# runtime / agent
runtime_id: claude-code
agent_class: coding-agent
capability_profile: balanced-executor
reasoning_depth: extended
trust_hosting_posture: externally-hosted-allowed

# review / retry
retry_count: 0
retry_pattern: none
validation_outcome: review-required
human_review_level: substantial-review
manual_rescue_required: no

# restart
handoff_required: yes
handoff_quality: compact
restart_burden: low

# graph-specific fields
context_source: code-graph
graph_operation: review-context
files_suggested_by_graph: 14
files_actually_read: 9
blast_radius_size: 14

# judgment
graph_helpfulness: medium
graph_overhead: low
```

**Why this is a mixed result:** the graph surfaced 14 files. 9 were relevant to the review. 5 were false positives (consistent with the known recall-over-precision tradeoff). One file that was not in the suggestion list was found manually and turned out to be critical — a dynamic dependency the graph did not model. The review caught a real integration risk. The graph contributed but was not sufficient on its own.

---

## Key observations across examples

| Signal | Example A | Example B | Example C |
|---|---|---|---|
| Task shape | Refactor | Bug fix | PR review |
| Graph operation | impact-radius | minimal-context | review-context |
| Files suggested | 11 | 8 | 14 |
| Files actually read | 7 | 2 | 9 |
| Graph helpfulness | high | low | medium |
| Graph overhead | low | medium | low |
| Missed by graph | 0 | 0 | 1 (dynamic dep) |

The table shows the core tradeoff: the graph earns its use in refactors and reviews, struggles with small bugs, and always has a recall-over-precision bias that requires selective reading.

---

## What the adapter does not do

This adapter:

- preserves observable signals for later comparison
- is reviewable by humans
- does not route automatically
- does not score or rank the work
- does not replace the readiness gate review

---

## Suggested next reading

- `docs/context-graph-integration.md`
- `docs/runtime-adapter-contract.md`
- `starter-pack/guides/context-graph-usage-guide.md`
- `starter-pack/templates/context-graph-test-record-template.md`
