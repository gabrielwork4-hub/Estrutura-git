---
tipo: backlog
status: pronto-para-refinamento
prioridade: alta
criado: 2026-07-01
ultima-revisao: 2026-07-01
origem-fluxo: "[[02-Fluxos/prompt-avaliacao-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo]
---

# [MPI-XXX] Substituir prompt de avaliação de keywords (v1 → v3)

> PO: [nome] · Epic: Evolução do pipeline de Estudo/Keywords (MPI Plus)
> Texto completo dos prompts em [[02-Fluxos/prompt-avaliacao-keywords]].

## Contexto
O prompt em produção (v1) avalia keyword por keyword, isolada — sem
cluster, sem checar canibalização entre páginas. O v3 resolve isso mantendo
foco em keywords para produção de conteúdo (sem entrar em briefs, linkagem,
KPIs ou cronograma, cortados desta versão).

## Story
**Como** PO do MPI Plus, **quero** trocar o prompt de avaliação de keywords
pelo v3, **para que** o sistema entregue cluster de keywords + arquitetura
de páginas sem canibalização, em vez de keywords soltas.

## O que muda (v1 → v3)

| Item | v1 (atual) | v3 (proposto) |
|---|---|---|
| Saída | Lista de keywords avaliadas (intenção/especificidade/relevância/justificativa) | + Cluster de Keywords (50–80, 8 clusters) + Content Map (15–25 páginas) + Análise Competitiva (Top 5) + Estratégia GEO |
| Canibalização | Não verificada | 1 keyword principal por página, zero repetição |
| Corte de relevância | Não definido | Descarta keyword com relevância < 3 |

**Fora de escopo:** pipeline de Construção de Conteúdo (inalterado); Briefs,
Linkagem Interna, KPIs e Plano de Implementação (cortados do v3).

## Critérios de aceite
1. Saída retorna as 4 seções: Cluster de Keywords, Content Map, Análise
   Competitiva, Estratégia GEO (quando aplicável).
2. Keyword com relevância < 3 não aparece na saída final.
3. Content map: 1 keyword principal por página, sem repetição, 15–25 páginas.
4. Sem componente geográfico → Estratégia GEO pode ser omitida.
5. `{keyword}` do content map segue compatível com o pipeline de Conteúdo existente.

## Relacionados
- [[02-Fluxos/prompt-avaliacao-keywords]]
- [[03-Produtos/mpi-plus]]
