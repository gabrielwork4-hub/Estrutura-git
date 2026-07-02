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
prazo. Dentre elas, 7 estão concentradas exatamente na camada de integração
mais crítica do sistema — a que o próprio PRD reconhece como SPOF (MPI
Plus): Q18-Q21 (mapeamento GM↔Salesforce, objeto usado, direção do sync,
relatório como nota ou só no GM) e Q27-Q30 (autenticação GM→API MPI Plus,
reconciliação de assets gerados, publicação WordPress, idempotência de
geração delegada).

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
