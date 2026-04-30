# Context Graph Test Record — C: PR Review (62 files)

Rodada comparativa. Tarefa: revisar um conjunto grande de mudanças acumuladas no
Crisis Monitor antes de merge (branch de trabalho vs main).

Projeto: Crisis Monitor (Next.js + TypeScript + Python backend)
Estado: working tree com 62 arquivos alterados vs `origin/main`

---

## Rodada 1 — Baseline (sem grafo)

```
slice_id: crisis-monitor-pr-review-baseline
project_id: crisis-monitor
task_shape: review
risk_posture: high
planning_depth: high-assurance
round: baseline

cold_boot_budget: extended
exploration_events: 5
expansion_events: 4
expansion_reason_present: yes

graph_used: no
graph_operation: none
context_source: direct-read
files_suggested_by_graph:
files_actually_read: 18
blast_radius_size:

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: review-required
human_review_level: substantial-review
manual_rescue_required: no

handoff_quality: compact
restart_burden: medium

graph_helpfulness:
graph_overhead:
```

Sem o grafo: `git diff --stat` → priorizar por tipo (lib/ primeiro, depois src/,
depois docs/). Leitura seletiva de 18 arquivos de maior risco. Identificação manual
de padrões de mudança. Revisão custosa — 62 arquivos exige julgamento sobre o que
pular, e o julgamento manual tem risco de omissão.

---

## Rodada 2 — Com grafo

```
slice_id: crisis-monitor-pr-review-graph
project_id: crisis-monitor
task_shape: review
risk_posture: high
planning_depth: high-assurance
round: graph

cold_boot_budget: extended
exploration_events: 3
expansion_events: 2
expansion_reason_present: yes

graph_used: yes
graph_operation: review-context
context_source: code-graph
files_suggested_by_graph: 82
files_actually_read: 18
blast_radius_size: 82

runtime_id: claude-code
agent_class: coding-agent
retry_count: 0
retry_pattern: none

validation_outcome: review-required
human_review_level: substantial-review
manual_rescue_required: no

handoff_quality: compact
restart_burden: low

graph_helpfulness: medium
graph_overhead: low
```

Query executada: `get_review_context` para os 62 arquivos alterados.

Output do grafo:
- 130 nós diretamente alterados
- 500 nós impactados em 82 arquivos adicionais
- **98 funções sem cobertura de testes identificadas** (buildEmailHtml,
  buildGenericWhatsappPayload, buildMetaGraphWhatsappPayload, createDispatchRun, etc.)
- Sinalização explícita: "Wide blast radius: 500 nodes impacted. Consider splitting
  into smaller PRs."

O dado mais valioso foi a lista de 98 gaps de teste em funções de alto risco
(`report-dispatch.ts`, WhatsApp Meta Graph). Esse sinal seria difícil de produzir
manualmente em 62 arquivos sem ler cada um.

A sugestão de dividir o PR em menores também foi relevante — o PR mistura 3 domínios
distintos (PR comms backend, design system Pulso, landing page).

---

## Resultado

```
better_than_baseline: yes (parcial)
where_it_helped:
  - identificou 98 gaps de teste em funções de dispatch/comms que seriam difíceis de localizar manualmente
  - sinalizou que o PR mistura domínios diferentes (PR comms + design system + landing)
  - reduziu eventos de exploração de 5 para 3 (grafo deu estrutura inicial)
  - restart_burden caiu de medium para low (grafo gerou um mapa consultável)
where_it_hurt:
  - 82 arquivos adicionais sugeridos vs 18 lidos — lista ainda exige filtro manual
  - falsos positivos nos arquivos adicionais: docs e arquivos de configuração como "impactados"
open_dependencies_found: lib/report-dispatch.ts tem 4 funções não testadas em fluxo crítico (WhatsApp Meta Graph)
false_positives: ~60 de 82 arquivos adicionais (73%)
decision: keep-optional — útil para PR reviews com muitos arquivos; inútil para escopo de impacto
```

---

## Notas

O caso de uso mais forte do grafo nesta avaliação: **gap de teste em PR review**.
Em 62 arquivos, identificar manualmente qual função crítica não tem teste é custoso.
O grafo fez isso em uma query, com nomes de funções específicos.

Essa função (test gap detection) funciona independentemente do F1 de impact accuracy
— ela não está predizendo quais arquivos foram afetados, está lendo o que mudou e
cruzando com a base de testes existente no grafo. É uma query sobre o grafo, não uma
predição de propagação.

**Conclusão consolidada dos 3 testes:**

| Critério | Test A (2 arquivos) | Test B (13 arquivos) | Test C (62 arquivos) |
|---|---|---|---|
| Grafo ajudou? | Não | Não | Parcialmente |
| Onde ajudou | — | — | Gap de testes + sinalização de PR grande |
| Overhead | Médio | Médio | Baixo |
| Falsos positivos | 97.5% | 95% | 73% |
| Decisão | Rejeitar | Rejeitar | Manter opcional |

O grafo tem um caso de uso válido no Crisis Monitor: **detecção de gaps de teste
em PR reviews grandes**. Para scope de impacto e contexto mínimo em projetos Next.js,
o F1=0.041 (benchmark) e os falsos positivos observados (73–97%) indicam que
leitura direta é mais eficiente.
