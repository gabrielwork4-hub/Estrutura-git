---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, ideal-tracker, geo, aeo, integracao]
---

# Integrar sinal de citação em LLM (Ideal Tracker) ao diagnóstico do Growth Machine

## Problema
O Índice de Performance do Growth Machine (RN-18, pesos 40/40/20) é 100%
métricas de SEO tradicional — posicionamento, tráfego, leads. Não existe
nenhum componente de GEO/AEO (citação em respostas de LLM, Share of Voice)
apesar de essa métrica já existir no cofre, isolada no
[[03-Produtos/ideal-tracker]]. Os dois produtos nunca foram pensados juntos.

## Impacto
O Growth Machine otimiza a causa (estrutura do site para ser citável) mas
não mede o efeito (se está de fato sendo citado por IA) — fica cego para o
canal de busca que mais cresce.

## Proposta de ajuste
Avaliar se faz sentido: (a) usar o dado do Ideal Tracker como sinal de
entrada complementar no diagnóstico do Growth Machine, sem fundir os
produtos; ou (b) manter separados por ora e só linkar no painel do
cliente. Ver ideia completa em
[[01-Ideias/growth-machine-geo-aeo-oportunidades]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
- Produto: [[03-Produtos/ideal-tracker]]
- Ideia: [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
