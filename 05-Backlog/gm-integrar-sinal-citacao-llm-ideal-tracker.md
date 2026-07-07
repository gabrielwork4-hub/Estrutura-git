---
tipo: backlog
status: direcao-confirmada-pelo-po
prioridade: alta
criado: 2026-07-02
ultima-revisao: 2026-07-03
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, ideal-tracker, geo, aeo, integracao]
---

# Integrar sinal de citação em LLM (Ideal Tracker) ao diagnóstico do Growth Machine

> **Atualização (2026-07-03):** direção confirmada pelo PO — deixa de ser
> hipótese em aberto. Plano concreto: alimentar a **aba GEO do projeto**
> trazendo diretamente as especificidades da plataforma Ideal Tracker para
> dentro do fluxo do Growth Machine, centralizando em vez de manter os
> dois produtos isolados. Ainda é trabalho futuro, não iniciado.

## Problema
O Índice de Performance do Growth Machine (RN-18, pesos 40/40/20) é 100%
métricas de SEO tradicional — posicionamento, tráfego, leads. Não existe
nenhum componente de GEO/AEO (citação em respostas de LLM, Share of Voice)
apesar de essa métrica já existir no cofre, isolada no
[[03-Produtos/ideal-tracker]]. Os dois produtos nunca foram pensados juntos.
Existe uma **aba GEO** no projeto/plataforma que hoje não é alimentada com
esses dados.

## Impacto
O Growth Machine otimiza a causa (estrutura do site para ser citável) mas
não mede o efeito (se está de fato sendo citado por IA) — fica cego para o
canal de busca que mais cresce. A aba GEO existe na interface, mas sem
fonte de dado real conectada, fica vazia/subutilizada.

## Proposta de ajuste (confirmada como direção, 2026-07-03)
Alimentar a aba GEO do projeto trazendo diretamente as especificidades da
plataforma Ideal Tracker (Share of Voice, citação em LLM) para dentro do
fluxo do Growth Machine — centralizando o fluxo num só lugar, em vez de
manter os dois produtos isolados. Ainda precisa ser detalhado tecnicamente
(qual dado exatamente, qual frequência, se é leitura direta ou API) antes
de virar história de dev. Ver ideia original em
[[01-Ideias/growth-machine-geo-aeo-oportunidades]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
- Produto: [[03-Produtos/ideal-tracker]]
- Ideia: [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
