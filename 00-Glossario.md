---
tipo: cerebro
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-02
tags: [glossario, core]
---

# Glossário

> Termos e siglas que aparecem repetidamente no cofre. Existe para que
> alguém entrando agora (PO, dev, ou uma IA) não precise decifrar jargão
> por contexto. Atualizar sempre que um termo novo se tornar recorrente.

## Siglas e regras de negócio

| Termo | Significado |
|---|---|
| **RN-XX** | Regra de Negócio numerada — usado no PRD do Growth Machine (RN-01 a RN-122) e em outros documentos técnicos. Cada uma é uma regra específica e rastreável. |
| **NFR-XX** | Non-Functional Requirement (Requisito Não-Funcional) — desempenho, disponibilidade, segurança etc., não comportamento de negócio. |
| **SPOF** | Single Point of Failure — ponto único de falha. No Growth Machine, o MPI Plus é reconhecido como SPOF da integração. |
| **MPI** | Marketing de Posicionamento na Internet — metodologia de SEO proprietária que dá nome ao MPI Plus e estrutura a auditoria do Growth Machine. |
| **TTFB** | Time To First Byte — tempo até o servidor responder o primeiro byte; métrica de performance de infraestrutura (Dimensão 9 do Growth Machine). |
| **CWV** | Core Web Vitals — métricas de experiência de página do Google (LCP, INP, CLS). |
| **GEO / AEO** | Generative Engine Optimization / Answer Engine Optimization — otimização para mecanismos de busca generativos (ChatGPT, AI Overview), diferente de SEO tradicional. Tema central do Ideal Tracker. |
| **SoV** | Share of Voice — participação de menções/visibilidade de uma marca frente a concorrentes, usado no Ideal Tracker para medir presença em LLMs. |

## Conceitos de SEO/keywords (fluxo de estudo de keywords)

| Termo | Significado |
|---|---|
| **Cluster** | Agrupamento de keywords por intenção de busca real, não por volume isolado — base de toda a lógica de [[02-Fluxos/estudo-de-keywords]]. |
| **Canibalização** | Quando duas páginas diferentes competem pela mesma intenção de busca, prejudicando o ranqueamento de ambas. O fluxo do cofre existe justamente para evitar isso. |
| **Silo semântico** | Estrutura de página-pilar + páginas-filhas ligadas por relação de significado real (não só palavras parecidas) — regra central do prompt v3 oficial ([[02-Fluxos/prompt-avaliacao-keywords]]). |
| **Palavra épica** | No sistema real do MPI Plus: a keyword eleita como principal de um produto, escolhida pelo maior volume entre termos comerciais/transacionais (fallback: maior volume geral). |
| **Content Map** | Tabela que define, por página, qual é a keyword principal (nunca repetida entre páginas) e as secundárias — o "mapa" que vira pauta de produção de conteúdo. |
| **Keyword-âncora** | Termo/ponto de partida do Cluster Pillar/Core de um estudo — no prompt v3 oficial, é derivada pelo próprio prompt a partir do serviço principal, não fornecida como entrada (ver correção de 2026-07-02 em [[02-Fluxos/prompt-avaliacao-keywords]]). |

## Termos específicos do Growth Machine

| Termo | Significado |
|---|---|
| **Índice de Performance** | Fórmula do Motor de Percepção (Fase 2): 40% posicionamento + 40% tráfego + 20% leads, classificando cliente em Ruim/Regular/Bom/Ótimo. |
| **Score de Saúde Técnica** | Nota determinística 0-100 calculada a partir das 10 dimensões de auditoria (Fase 3), separada do Índice de Performance. |
| **Parecer Consolidado** | Diagnóstico executivo em linguagem natural gerado por um agente de IA, unindo Índice + Score + as 10 dimensões + Sentinela. |
| **Módulo Sentinela** | Vigilância diária e leve (uptime, SSL, DNS) de 100% dos sites, independente do ciclo de auditoria mensal/trimestral. |
| **Maturação (60 dias)** | Janela de bloqueio de reanálise após uma ação ser validada — evita medir resultado antes do efeito real aparecer. |
| **Dimensão (1 a 10)** | Cada uma das 10 áreas de auditoria técnica do Growth Machine (Estudo, Conteúdo, Arquitetura, W3C, PageSpeed, Schemas, Sitemap, Search Console, Servidor, Leads). |

## Termos específicos do vault/processo

| Termo | Significado |
|---|---|
| **RAG** | Retrieval-Augmented Generation — o motivo de existir a regra de linkagem obrigatória do cofre: permitir que uma IA navegue de uma ideia até produto/fluxo/decisão sem perder contexto. |
| **Nota órfã** | Nota sem nenhum link de entrada ou saída — proibida pela regra do cofre (CLAUDE.md). |
| **Fluxo** | Processo/workflow documentado em [[02-Fluxos]], com histórico de ajustes. |
| **Decisão fundadora** | Decisão registrada em [[04-Decisões]] que molda o funcionamento do cofre ou de um produto — estilo ADR (Architecture Decision Record). |

## Notas relacionadas
- [[00-Cerebro]]
- [[03-Produtos/mapa-dependencia-produtos]]
