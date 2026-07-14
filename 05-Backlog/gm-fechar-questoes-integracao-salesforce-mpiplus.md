---
tipo: backlog
status: resolvido
criado: 2026-07-02
ultima-revisao: 2026-07-13
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, integracao, salesforce, mpi-plus, spof]
---

# Fechar as 7 questões de integração Salesforce/MPI Plus (Growth Machine)

> ✅ **RESOLVIDO em 2026-07-13** — as 7 questões foram endereçadas pelo PO
> (6 com resposta concreta, Q18 adiada explicitamente para fase 2). Ver
> detalhamento abaixo. Maior bloqueador de build do PRD, fechado.

## Problema
17 das 30 questões em aberto do PRD do Growth Machine não têm dono nem
prazo. Dentre elas, 7 estavam concentradas exatamente na camada de
integração mais crítica do sistema — a que o próprio PRD reconhece como
SPOF (MPI Plus): Q18-Q21 (mapeamento GM↔Salesforce) e Q27-Q30 (autenticação
GM→API MPI Plus, reconciliação de assets gerados, publicação WordPress,
idempotência de geração delegada).

> ✅ **As 7 endereçadas pelo PO (2026-07-13):**
> - **Q19/Q20/Q21** (Salesforce): pooling mensal; conteúdo =
>   status/data/especificidades técnicas; nota criada todo mês pra todo
>   cliente (registro completo do backlog na jornada); quando "Ruim", cai
>   na **fila de ações do GM (RN-44)** → analista de Growth
>   demanda/executa (RN-47).
> - **Q18** (objeto do Salesforce): não é mais pendência técnica em
>   aberto — **adiada explicitamente para a 2ª etapa da vinculação
>   Salesforce** (decisão de faseamento do PO).
> - **Q29** (publicação WordPress): confirmado, MPI Plus publica direto.
> - **Q30** (idempotência): confirmado que existe proteção contra
>   duplicidade; mecanismo técnico exato não detalhado.
> - **Q27** (autenticação): ✅ resolvida — via API, mecânica interna (MPI
>   Plus desenvolvido dentro do próprio Grupo, sem OAuth de terceiro).
>
> - **Q28** (reconciliação de assets): ✅ confirmado — é o `IntegrationJob.id`
>   do padrão assíncrono já descrito na RN-101; não era mecanismo novo.
>
> Ver [[03-Produtos/growth-machine/catalogo-regras-negocio]] › RN-74 a
> RN-78 e RN-100 a RN-102. **7 das 7 questões originais endereçadas.**

## Impacto (histórico)
Sem essas definições, não havia como iniciar a construção de ponta a
ponta — eram pré-requisito técnico, não detalhe de refinamento. Era o
maior risco de cronograma do projeto (risco de planejamento, não técnico).

## Ajuste aplicado
Todas as 7 questões foram levadas ao PO e respondidas (2026-07-13) — 6
com resposta concreta, Q18 adiada explicitamente para a 2ª etapa da
vinculação Salesforce. Detalhamento original nos blocos "Agentes de IA" e
"Decisões Técnicas e NFRs" de [[03-Produtos/growth-machine/avaliacao-fluxo]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
