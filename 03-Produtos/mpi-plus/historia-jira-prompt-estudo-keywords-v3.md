---
tipo: backlog
status: oficial
prioridade: alta
criado: 2026-07-01
ultima-revisao: 2026-07-01
origem-fluxo: "[[02-Fluxos/prompt-avaliacao-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo]
---

# [MPI-XXX] Substituir prompt de avaliação de keywords pelo Estudo SEO Clusterizado (v3)

> Versão **oficial** (2026-07-01) — texto integral enviado pelo usuário,
> substitui a versão enxuta anterior. Prompt v3 completo em
> [[02-Fluxos/prompt-avaliacao-keywords]].

## Epic
Evolução do pipeline de Estudo / Keywords do IdealPlus (MPI Plus)

## Tipo
Story (mudança de prompt em produção — sem mudança de infraestrutura)

## Contexto
Hoje, a etapa de avaliação de keywords do MPI Plus roda em cima de um
prompt (v1) que avalia **keyword por keyword, isoladamente**, sem
clusterização, sem checagem de canibalização entre páginas e sem content
map.

O pipeline de **Construção de Conteúdo** do MPI Plus (SERP Search → Domain
Classification → Pattern Analysis → Structure → Section → Cohesion → QA)
já assume uma `{keyword}` pronta como entrada — ele não decide qual
keyword/página deve existir, nem verifica canibalização entre páginas. Essa
decisão acontece **antes** desse pipeline, e é exatamente o prompt que
estamos substituindo.

## Objetivo da história
Trocar o prompt de produção da etapa de avaliação/clusterização de keywords
(hoje v1) pelo prompt v3, sem alterar o restante do pipeline de Construção
de Conteúdo (SERP Search, Domain Classification, Pattern Analysis,
Structure, Section, Cohesion, QA), que permanece como está.

## Story
**Como** PO do MPI Plus, **quero** substituir o prompt de avaliação de
keywords existente pelo prompt v3 (Estudo SEO Clusterizado, focado em
keywords), **para que** o sistema pare de gerar keywords soltas e passe a
entregar cluster de keywords + arquitetura de páginas, sem canibalização,
pronto para alimentar a produção de conteúdo com mais exatidão.

## Escopo desta história (o que muda)

| Item | Hoje (v1) | Depois (v3) |
|---|---|---|
| Unidade de saída | Lista de keywords avaliadas (intenção/especificidade/relevância/justificativa) | Cluster de keywords + content map |
| keywords | Organização de volume extraída | Mínimo 40–70 keywords, organizadas em 8 clusters obrigatórios (Pillar/Core, Problemas/Sintomas, Serviços específicos, Marcas, GEO local) |
| Canibalização | Regra aplicada, mas na prática ainda seguia a canibalização | Regra explícita: máximo 1 keyword principal por página; content map limitado a 15–25 páginas |

Qualquer alteração no pipeline de Construção de Conteúdo
(`domain_classification`, `pattern_analysis`, `structure`, `section`,
`cohesion`, `qa`) documentado no guia de prompts do IdealPlus — este
pipeline continua recebendo `{keyword}` normalmente.

## Critérios de aceite
1. **Dado** um briefing de empresa/produto completo, **quando** o estudo
   for executado com o prompt v3.
2. **Dado** o cluster de keywords gerado, **quando** qualquer keyword tiver
   relevância < 3, **então** ela não deve aparecer na tabela final entregue.
3. **Dado** o content map gerado, **quando** for auditado, **então** cada
   página deve ter exatamente 1 keyword principal, sem repetição de keyword
   principal entre páginas (zero canibalização), e o total de páginas deve
   estar entre 15 e 25.
4. **Dado** um nicho sem componente geográfico relevante, **quando** o
   estudo for gerado, **então** a seção de Estratégia GEO pode ser omitida
   ou marcada como não aplicável, sem quebrar o restante da saída.
5. **Dado** o pipeline de Construção de Conteúdo existente, **quando** a
   keyword de uma página do novo content map for usada como `{keyword}` de
   entrada, **então** o pipeline deve continuar funcionando sem alteração
   de contrato/formato de entrada.

## Relacionados
- [[02-Fluxos/prompt-avaliacao-keywords]] — texto completo dos prompts v1, v2 e v3
- [[02-Fluxos/estudo-de-keywords]] — fluxo de origem
- [[03-Produtos/mpi-plus]] — produto onde o pipeline roda
