---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, geo, aeo, ga4, trafego]
---

# Segmentar tráfego de origem de IA (GA4) no Motor de Percepção

## Problema
RN-86 define que `trafego_real` considera apenas tráfego orgânico
(excluindo pago), mas não há distinção de tráfego vindo de referência de
IA (ChatGPT, Perplexity como origem) — hoje esse tráfego cai dentro de
"orgânico" genérico ou fica invisível, sem regra clara de classificação.

## Impacto
Fonte de tráfego crescente sem visibilidade no diagnóstico — o cliente
pode estar recebendo tráfego relevante de IA sem que o Growth Machine
reconheça isso como sinal de sucesso.

## Proposta de ajuste
Avaliar a viabilidade de segmentar tráfego de referral de IA no GA4 (Fase
2, Motor de Percepção), como métrica complementar ao `trafego_real`. Ver
[[01-Ideias/growth-machine-geo-aeo-oportunidades]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
- Ideia: [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
