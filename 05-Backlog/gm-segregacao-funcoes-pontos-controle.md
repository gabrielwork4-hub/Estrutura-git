---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, padrao-recorrente, governanca, segregacao-funcoes]
---

# Avaliar segregação de funções em pontos de controle críticos (Growth Machine)

## Problema
Padrão recorrente de concentração de responsabilidade: o CS sozinho valida
o briefing com o cliente na Fase 1 (sem segunda camada de verificação); o
Analista acumula aprovação inicial e validação técnica final na Fase 4,
depois da extinção da persona "Revisor" (RN-49) — reduz segregação de
funções em nome de agilidade, sem um segundo par de olhos independente
(risco de viés de confirmação: quem aprovou a ação tende a validar que ela
foi bem executada).

## Impacto
Menos controle interno em pontos que decidem o que chega ao cliente e o
que é considerado "concluído" — risco de qualidade silenciosa, não
detectável por métricas automáticas.

## Proposta de ajuste
Avaliar reintrodução de segregação de papéis nesses dois pontos, ou pelo
menos amostragem periódica de auditoria humana independente sobre decisões
já aprovadas/validadas pela mesma pessoa. Ver detalhamento em
[[03-Produtos/growth-machine/avaliacao-fluxo]], "Fase 1" e "Fase 4".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
