---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, integracao, salesforce, mpi-plus, spof]
---

# Fechar as 7 questões de integração Salesforce/MPI Plus (Growth Machine)

## Problema
17 das 30 questões em aberto do PRD do Growth Machine não têm dono nem
prazo. Dentre elas, 7 estavam concentradas exatamente na camada de
integração mais crítica do sistema — a que o próprio PRD reconhece como
SPOF (MPI Plus): Q18-Q21 (mapeamento GM↔Salesforce) e Q27-Q30 (autenticação
GM→API MPI Plus, reconciliação de assets gerados, publicação WordPress,
idempotência de geração delegada).

> ✅ **Q19/Q20/Q21 resolvidas pelo PO (2026-07-13)**: mecanismo = pooling
> mensal (não webhook); conteúdo = status/data/especificidades técnicas;
> relatório ao cliente é incondicional. A nota no Salesforce é criada todo
> mês, para todo cliente (registro completo do backlog na jornada — não é
> ferramenta de exceção); o que é condicional a "Ruim" é se esse registro
> **volta a acionar o fluxo do GM** — mecânica exata do retorno ainda não
> detalhada. Ver [[03-Produtos/growth-machine/catalogo-regras-negocio]] ›
> RN-74 a RN-78. **Restam 5 das 7**: Q18 (qual objeto do Salesforce recebe
> a nota) e Q27-Q30 (MPI Plus), todas pendentes de resposta técnica (Tech
> Lead + quem administra Salesforce/MPI Plus).

## Impacto
Sem essas definições, não há como iniciar a construção de ponta a ponta —
são pré-requisito técnico, não detalhe de refinamento. É o maior risco de
cronograma do projeto (risco de planejamento, não técnico).

## Proposta de ajuste
Priorizar a resolução dessas 7 questões antes de qualquer outra frente do
PRD, com Tech Lead/RevOps conforme indicado no próprio documento. Ver
detalhamento completo nos blocos "Agentes de IA" e "Decisões Técnicas e
NFRs" de [[03-Produtos/growth-machine/avaliacao-fluxo]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
