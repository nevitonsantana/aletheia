# Context Graph Test Record

Use this template to record one slice where a code-structure graph was used (or intentionally skipped as a baseline). Compare paired records — one without graph, one with — to evaluate whether the graph helped.

Extends the base slice telemetry model (`docs/slice-telemetry-model.md`) with graph-specific fields.

---

## Identity

```
slice_id:
project_id:
task_shape:           # bounded-execution | exploration | refactor | review | architecture
risk_posture:         # low | medium | high
planning_depth:       # lite | standard | high-assurance
round:                # baseline | graph
```

---

## Graph usage

```
graph_used:           # yes | no
graph_operation:      # minimal-context | impact-radius | review-context | traversal | semantic-search | none
context_source:       # code-graph | direct-read | mixed
```

---

## Context signals

```
cold_boot_budget:     # minimal | moderate | extended
exploration_events:   # number (graph queries count as exploration events)
expansion_events:     # number
expansion_reason_present: # yes | no
```

---

## Graph output

```
files_suggested_by_graph: # number
files_actually_read:      # number
blast_radius_size:        # number (from impact-radius, if used; else leave blank)
```

---

## Runtime and agent

```
runtime_id:
agent_class:
retry_count:
retry_pattern:        # none | changed-strategy | repeated-without-change
```

---

## Validation and human effort

```
validation_outcome:   # validated | review-required | blocked | escalated | incomplete
human_review_level:   # none | light-review | substantial-review | manual-rescue
manual_rescue_required: # yes | no
```

---

## Handoff and restart

```
handoff_quality:      # not-needed | compact | inflated | restart-still-heavy
restart_burden:       # low | medium | high
```

---

## Graph judgment

```
graph_helpfulness:    # low | medium | high
graph_overhead:       # low | medium | high
```

**Helpfulness guidance:**
- `high` — suggestions matched what was needed; fewer irrelevant files read than without the graph
- `medium` — suggestions partially useful; some irrelevant files still opened
- `low` — fewer than 30% of suggestions were relevant; direct read would have been faster

**Overhead guidance:**
- `low` — graph query added negligible time or steps
- `medium` — query added a noticeable step but was offset by clearer scope
- `high` — query added steps without reducing reads or clarifying scope

---

## Result

```
better_than_baseline: # yes | no | inconclusive
where_it_helped:
where_it_hurt:
open_dependencies_found: # dependencies the graph identified that were not obvious from reading
false_positives:         # files suggested but not relevant
decision:                # incorporate | keep-optional | reject | defer
```

---

## Notes

Free-form space for observations not captured by the fields above. Include gate interactions, unexpected structural findings, or handoff notes.

```
notes:
```

---

## Reference

- `docs/context-graph-integration.md`
- `starter-pack/guides/context-graph-usage-guide.md`
- `docs/slice-telemetry-model.md`
- `docs/runtime-adapter-contract.md`
