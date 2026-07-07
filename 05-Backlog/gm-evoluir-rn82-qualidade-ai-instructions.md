---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, geo, aeo, rn-82]
---

# Evoluir RN-82 de "existe sim/não" para avaliar qualidade do AI Instructions/LLM.txt

## Problema
RN-82 valida apenas a **presença** de página AI Instructions e LLM.txt,
referenciados no robots.txt e em meta tag no header — não avalia se o
conteúdo desses arquivos realmente ajuda uma IA a entender e citar o site
corretamente.

## Impacto
Um cliente pode "passar" na checagem (arquivo existe) com um conteúdo
raso ou mal estruturado, sem ganho real de citabilidade — a régua atual
mede presença, não eficácia.

## Proposta de ajuste
Expandir a checagem para avaliar qualidade/estrutura do conteúdo desses
arquivos (clareza, cobertura de informação relevante sobre a empresa/
produto), não só existência. Ver
[[01-Ideias/growth-machine-geo-aeo-oportunidades]].

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
- Ideia: [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
