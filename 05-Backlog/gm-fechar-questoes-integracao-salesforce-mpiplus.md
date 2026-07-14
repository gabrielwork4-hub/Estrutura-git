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

> ✅ **6 das 7 substancialmente resolvidas pelo PO (2026-07-13):**
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
> - **Q27** (autenticação): parcialmente — MPI Plus é o lado ativo da
>   credencial (consistente com NFR-06/SSO); mecanismo exato (token/OAuth)
>   não detalhado.
>
> Ver [[03-Produtos/growth-machine/catalogo-regras-negocio]] › RN-74 a
> RN-78 e RN-100 a RN-102. **Resta genuinamente em aberto: Q28**
> (reconciliação de assets gerados) — pergunta reformulada, aguardando
> resposta.

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
