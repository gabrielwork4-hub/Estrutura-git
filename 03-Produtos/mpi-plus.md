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

## Responsáveis
_A preencher — PO ainda mapeando stakeholders (ver [[00-Painel-Estado]])._

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

A história Jira **oficial** de mudança de prompt para essa etapa (v1 → v3)
está em
[[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]], pronta
para ser criada no board e refinada com o time de DEV.

Há uma segunda história, complementar, mais upstream — **enviada ao Jira
em 2026-07-03**, resolvendo o gargalo que travava o fluxo de geração de
termos rodar de ponta a ponta:
[[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] — inverte
a etapa de **geração de termos** (antes sementes + Google Autocomplete +
concatenação mecânica) para a IA gerar os termos direto do briefing, com o
KeywordTool só enriquecendo (volume/CPC/concorrência), sem filtrar nada.

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
- [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] —
  história para inverter a geração de termos (IA gera, KeywordTool só
  enriquece), etapa anterior à clusterização.

## Ideias relacionadas
-
