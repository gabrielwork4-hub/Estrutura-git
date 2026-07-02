---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, sentinela, infraestrutura, questoes-abertas]
---

# Resolver escopo e infraestrutura do Módulo Sentinela (Q25/Q26 — Growth Machine)

## Problema
Duas questões em aberto do PRD ainda não definidas: (Q25) escopo exato de
páginas monitoradas por projeto — quantas páginas por site, se inclui ping
ativo de endpoint de formulário; (Q26) infraestrutura do cron — Laravel
Horizon interno vs. serviço externo dedicado de uptime, e se há redundância
caso a própria infraestrutura do GM tenha problema.

## Impacto
O Sentinela roda monitoramento na própria infraestrutura da aplicação — se
o problema for na infra/rede onde o GM roda, o Sentinela pode falhar
exatamente quando mais precisa funcionar, sem redundância geográfica
mencionada. Sem escopo definido, cobertura de "home e principais MPIs" fica
ambígua para 2.500 sites.

## Proposta de ajuste
Fechar Q25 e Q26 com Growth/Tech Lead antes da implementação do módulo. Ver
[[03-Produtos/growth-machine/avaliacao-fluxo]], bloco "Módulo Sentinela".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
