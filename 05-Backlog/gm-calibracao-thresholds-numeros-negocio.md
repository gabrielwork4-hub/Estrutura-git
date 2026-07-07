---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, padrao-recorrente, calibracao, parametrizacao]
---

# Documentar origem/calibração dos thresholds de negócio (Growth Machine)

## Problema
Vários números de negócio importantes aparecem no PRD sem rastro de como
foram definidos: threshold de 70% de similaridade vetorial e trava de 50%
do pacote (Fase 1), pesos 40/40/20 do Índice de Performance e taxa de
conversão default de 5% (Fase 2), cota de 400 req/dia do PageSpeed
(Ferramentas Externas). Todos parecem definidos por julgamento de
especialista, não por teste documentado.

## Impacto
Não é necessariamente errado, mas dificulta revisar/recalibrar depois —
sem saber a origem de um número, não dá para saber se ele ainda faz sentido
quando o produto mudar de escala ou perfil de cliente.

## Proposta de ajuste
Documentar a origem/racional de cada threshold citado, mesmo que a resposta
seja "julgamento de especialista X, a validar com dado real após N meses em
produção" — o importante é não deixar esses números como se fossem
verdades absolutas sem contexto. Ver lista completa nos blocos "Fase 1",
"Fase 2" e "Ferramentas Externas Integradas" em
[[03-Produtos/growth-machine/avaliacao-fluxo]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
