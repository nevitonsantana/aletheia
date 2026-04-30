# Context Graph Test Record — B: Design System Refactor (13 files)

Rodada comparativa. Tarefa real: unificar tokens de cor, score bands e contraste
semântico no Pulso Design System integrado ao Crisis Monitor.

Projeto: Crisis Monitor (Next.js + TypeScript)
Commit referência: `9e7b871` (fix pulso — 13 arquivos, 1690 inserções)

---

## Rodada 1 — Baseline (sem grafo)

```
slice_id: crisis-monitor-pulso-tokens-baseline
project_id: crisis-monitor
task_shape: bounded-execution
risk_posture: medium
planning_depth: standard
round: baseline

cold_boot_budget: moderate
exploration_events: 3
expansion_events: 2
expansion_reason_present: yes

graph_used: no
graph_operation: none
context_source: direct-read
files_suggested_by_graph:
files_actually_read: 8
blast_radius_size:

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: validated
human_review_level: substantial-review
manual_rescue_required: no

handoff_quality: not-needed
restart_burden: low

graph_helpfulness:
graph_overhead:
```

Sem o grafo, a estratégia foi: ler `globals.css` → identificar tokens afetados →
seguir os imports para `design-system/page.tsx` → expandir para componentes que usam
os tokens (`metric-card.tsx`, `risk-levels/page.tsx`). 8 arquivos lidos, 2 expansões
justificadas. A cascata de `globals.css` para componentes é previsível pelo padrão
de design system — não requer grafo.

---

## Rodada 2 — Com grafo

```
slice_id: crisis-monitor-pulso-tokens-graph
project_id: crisis-monitor
task_shape: bounded-execution
risk_posture: medium
planning_depth: standard
round: graph

cold_boot_budget: moderate
exploration_events: 4
expansion_events: 1
expansion_reason_present: yes

graph_used: yes
graph_operation: impact-radius
context_source: code-graph
files_suggested_by_graph: 187
files_actually_read: 8
blast_radius_size: 187

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: validated
human_review_level: substantial-review
manual_rescue_required: no

handoff_quality: not-needed
restart_burden: low

graph_helpfulness: low
graph_overhead: medium
```

Query executada: `get_impact_radius` para 5 arquivos-chave do conjunto de 13
(`globals.css`, `design-system/page.tsx`, `risk-levels/page.tsx`,
`metric-card.tsx`, `design_tokens.json`) →
182 arquivos adicionais sugeridos (500 nós, truncado).

O blast radius de `globals.css` no grafo captura todos os arquivos que importam
qualquer classe CSS — que em um design system é virtualmente todo o projeto.
O número 182 é estruturalmente correto mas operacionalmente inútil: não discrimina
quais arquivos precisam de revisão versus quais apenas herdam o token sem usar os
valores que mudaram.

Nenhum arquivo adicional relevante foi identificado pelo grafo que a leitura direta
não tivesse encontrado. A cascata de tokens CSS não requer traversal de grafo —
requer entender quais tokens semânticos mudaram e onde são aplicados, o que é
informação de domínio, não estrutural.

---

## Resultado

```
better_than_baseline: no
where_it_helped: confirmou que globals.css tem alto blast radius — útil como sinal de risco, não de escopo
where_it_hurt: 182 arquivos sugeridos vs 8 necessários; filtrar a lista consumiria mais tempo que a leitura direta
open_dependencies_found: nenhuma que a leitura direta não identificasse
false_positives: ~174 de 182 (95%)
decision: reject para refatorações de design system baseadas em CSS global
```

**Achado importante:** o blast radius de `globals.css` é sempre máximo porque CSS
global não tem granularidade semântica no grafo. Qualquer arquivo que importa o
design system aparece como "afetado". O sinal correto aqui seria: "globals.css
alterado → revisar todos os tokens que mudaram semânticamente" — um critério
de domínio, não estrutural.

---

## Notas

Caso de exceção possível: se a refatoração alterasse a *interface* de um componente
compartilhado (não apenas tokens CSS), o grafo poderia identificar consumidores não
óbvios. Neste caso, a mudança era em tokens, não em APIs — logo o grafo não agregou.

O sinal de risco (blast_radius alto → aumentar planning depth) funcionou: a tarefa
foi planejada em `standard` e teve revisão humana substancial. Mas esse sinal poderia
vir de uma regra simples ("globals.css alterado = risco médio") sem necessidade do grafo.
