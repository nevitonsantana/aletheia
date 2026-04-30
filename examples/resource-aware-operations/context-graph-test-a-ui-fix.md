# Context Graph Test Record — A: UI Fix (2 files)

Rodada comparativa. Tarefa real: corrigir hierarquia de badges e persistência de
anotações em dois componentes React do Crisis Monitor.

Projeto: Crisis Monitor (Next.js + TypeScript)
Commit referência: `9f6fcb4` (refactor coverage-ui)

---

## Rodada 1 — Baseline (sem grafo)

```
slice_id: crisis-monitor-badge-fix-baseline
project_id: crisis-monitor
task_shape: bounded-execution
risk_posture: low
planning_depth: lite
round: baseline

cold_boot_budget: minimal
exploration_events: 0
expansion_events: 0
expansion_reason_present: no

graph_used: no
graph_operation: none
context_source: direct-read
files_suggested_by_graph:
files_actually_read: 2
blast_radius_size:

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: validated
human_review_level: light-review
manual_rescue_required: no

handoff_quality: not-needed
restart_burden: low

graph_helpfulness:
graph_overhead:
```

Arquivos lidos: `clipping-section.tsx`, `mention-detail-sheet-content.tsx`.
Mudança puramente visual — badges, ícones, estado de save. Sem dependências externas relevantes.
Nenhuma expansão necessária. O task description já identificava os dois arquivos.

---

## Rodada 2 — Com grafo

```
slice_id: crisis-monitor-badge-fix-graph
project_id: crisis-monitor
task_shape: bounded-execution
risk_posture: low
planning_depth: lite
round: graph

cold_boot_budget: minimal
exploration_events: 2
expansion_events: 0
expansion_reason_present: no

graph_used: yes
graph_operation: impact-radius
context_source: code-graph
files_suggested_by_graph: 80
files_actually_read: 2
blast_radius_size: 80

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: validated
human_review_level: light-review
manual_rescue_required: no

handoff_quality: not-needed
restart_burden: low

graph_helpfulness: low
graph_overhead: medium
```

Queries executadas:
1. `get_minimal_context` — retornou apenas stats globais do grafo, sem lista de arquivos
2. `get_impact_radius` para os 2 arquivos → 80 nós adicionais sugeridos, 78 arquivos extras

O grafo calculou 500 nós impactados (truncado) a 2 hops. Para um fix de badge em um
componente React leaf, a propagação de 2 hops num grafo de 3648 nós captura
praticamente o projeto inteiro — não discrimina escopo local.

Nenhum dos 78 arquivos adicionais era relevante para esta tarefa.

---

## Resultado

```
better_than_baseline: no
where_it_helped: nenhum ganho identificado
where_it_hurt: adicionou 2 eventos de exploração sem reduzir leituras; lista de 80 arquivos criou ruído sem sinal
open_dependencies_found: nenhuma
false_positives: 78 de 80 arquivos sugeridos (97.5%)
decision: reject para este tipo de tarefa
```

**Observação crítica:** o benchmark de avaliação do próprio `code-review-graph` reporta
F1 = 0.041 para projetos Next.js — confirmado aqui. O grafo de 2 hops explode no
grafo altamente conectado de uma aplicação Next.js com design system compartilhado.
Para fixes localizados em componentes UI, leitura direta é estritamente melhor.

---

## Notas

A regra do guia de uso — "bug em arquivo conhecido: não usar o grafo" — é validada.
O overhead foi `medium` e não `high` porque a query durou menos de 2s; mas o custo
cognitivo de filtrar 80 sugestões irrelevantes seria alto para um agente que tenta
seguir a lista.
