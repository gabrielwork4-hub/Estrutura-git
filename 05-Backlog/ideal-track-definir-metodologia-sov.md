---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-06-30
origem-fluxo: "[[03-Produtos/ideal-tracker]]"
tags: [ideal-tracker, geo, mvp]
---

# Definir metodologia de medição do Share of Voice (SoV) — Ideal Track

## Problema
O PRD do Ideal Track nunca define com precisão como o SoV é medido: se
"ChatGPT" no MVP é a API (GPT-4o) ou o produto real que o cliente usa, quantos
runs por prompt são feitos por coleta, e como lidar com o não-determinismo
das respostas de LLM frente à exigência de um SoV "reproduzível e auditável".
Também não há definição de fornecedor/custo para coleta de Google AI Overview
(sem API oficial — depende de scrapers de terceiros).

## Impacto
Sem essa definição, o número mostrado ao cliente pode divergir do que ele
mesmo testa manualmente no ChatGPT, quebrando a confiança no produto logo no
primeiro uso. Também trava o cálculo correto dos tetos de prompts/respostas
por plano, que hoje não fecham matematicamente.

## Proposta de ajuste
- Definir explicitamente: produto real vs. API para cada LLM monitorado.
- Definir número fixo de runs por prompt por coleta e documentar a regra de agregação.
- Mapear fornecedor e custo/risco de ToS para coleta de AI Overview.
- Recalcular os tetos de prompts × respostas por plano com a definição acima.

## Relacionados
- Produto: [[03-Produtos/ideal-tracker]]
- Fluxo: [[02-Fluxos/processo-kickoff-discovery]]
