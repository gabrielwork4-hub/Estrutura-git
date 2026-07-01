---
tipo: produto
status: em-desenvolvimento
criado: 2026-06-30
origem:
  - "Notion — transcrição @hoje 10:12 (BRT), conversa com Lucas"
  - "Drive — pasta MPI Plus+ (verificada 30/06: só contém Templates/Wordpress e Templates/Demonstração, sem PRD próprio)"
tags: [produto, mpi-plus, keywords]
---

# MPI Plus

## Visão geral
> _A preencher._ Citado na transcrição de kick-off como produto que passou
> por uma refatoração completa de processo e palavras-chave (v2). O conteúdo
> de negócio real do MPI Plus está referenciado dentro do PRD da
> [[03-Produtos/growth-machine]] (que depende dele como pré-requisito de
> carteira, RN-108) — não há um PRD próprio do MPI Plus na pasta do Drive,
> apenas templates de Wordpress e Demonstração.

## Status atual (10:12 — hoje)
- Refatorou todo o processo e as palavras-chave (**v2**).
- É pré-requisito de carteira para a Growth Machine (RN-108): cliente fora do MPI Plus entra primeiro nele.

## Funcionalidades
- [ ] Documentar o PRD próprio do MPI Plus (não encontrado no Drive ainda — só templates)

## Pipeline de prompts (Estudo + Conteúdo)
Guia de processos e prompts do IdealPlus (documento técnico anexado em
2026-07-01) descreve os dois pipelines de produção: **Construção do Estudo**
(gera `company_context`/`product_context` a partir do briefing) e
**Construção de Conteúdo** (SERP Search → Domain Classification → Pattern
Analysis → Structure → Section → Cohesion → QA, com regra anti-alucinação
injetada em 5 etapas). O pipeline de Conteúdo já assume uma `{keyword}`
pronta — a decisão de qual keyword/página existe roda **antes** dele, na
etapa de avaliação/clusterização de keywords (ver
[[02-Fluxos/prompt-avaliacao-keywords]]).

Há uma história de mudança de prompt em andamento para essa etapa (v1 → v3):
[[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]].

## Cruzamento com outras notas
- O conteúdo do MPI Plus é citado em [[03-Produtos/growth-machine]] como
  dependência da implementação de blog.
- A refatoração de palavras-chave (v2) deve seguir a lógica de
  [[02-Fluxos/estudo-de-keywords]] (clusterização, anti-canibalização,
  variações locais) daqui em diante.
- Faz parte do processo descrito em [[02-Fluxos/processo-kickoff-discovery]].
- O prompt de avaliação de keywords (v1→v2→v3) roda dentro do pipeline de
  Estudo deste produto — ver [[02-Fluxos/prompt-avaliacao-keywords]].

## Decisões relacionadas
- [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]] —
  história Jira para substituir o prompt v1 pelo v3 na etapa de
  avaliação/clusterização de keywords.

## Ideias relacionadas
-
