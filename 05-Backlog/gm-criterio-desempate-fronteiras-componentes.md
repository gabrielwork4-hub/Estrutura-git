---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, padrao-recorrente, arquitetura, desempate]
---

# Definir critério de desempate entre componentes automatizados que divergem (Growth Machine)

## Problema
Padrão recorrente: fronteiras entre componentes sem critério de desempate
explícito. Dimensão 5 (PageSpeed/front-end) vs. Dimensão 9
(Servidor/TTFB) podem gerar disputa de responsabilidade sobre "problema
predominante" sem dono claro do critério. Na Fase 4, quando IA e Analista
divergem na validação pós-execução (um aprova, outro reprova), o PRD trata
"IA + Analista reprovam" como bloco único, sem descrever o caso de
divergência.

## Impacto
Ambiguidade operacional: sem regra de desempate, decisões ficam sujeitas a
interpretação caso a caso entre times técnicos, ou geram ping-pong de
responsabilidade.

## Proposta de ajuste
Definir regra de desempate objetiva para os dois casos: (1) critério
técnico explícito para classificar problema como Dim 5 vs. Dim 9, (2) regra
de precedência quando IA e Analista divergem na validação (ex: analista
sempre prevalece, ou divergência força escalonamento automático). Ver
[[03-Produtos/growth-machine/avaliacao-fluxo]], "Fase 3" e "Fase 4".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
