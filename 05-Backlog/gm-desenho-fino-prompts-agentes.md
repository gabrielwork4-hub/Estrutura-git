---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, agentes-ia, prompt, qualidade]
---

# Priorizar o desenho fino dos prompts dos 9 agentes de IA (Growth Machine)

## Problema
O PRD constrói toda a arquitetura ao redor dos agentes (contrato de prompt,
schema JSON, versionamento, gates humanos), mas o conteúdo fino de cada
prompt — o que realmente faz o agente confiável — está fora do escopo do
documento, sem cronograma, dono ou processo de validação atribuído.
Citação literal do PRD: *"a casa é entregue vazia; os móveis são os
prompts"*.

## Impacto
É o risco central do produto segundo a própria avaliação: nenhuma
arquitetura, por melhor desenhada que seja, mitiga a ausência do trabalho
de prompt engineering em si. Tratado como possível bloqueador de início de
desenvolvimento, não como detalhe posterior.

## Proposta de ajuste
- Iniciar o desenho fino dos prompts em paralelo à Parte III técnica do
  PRD, não como última etapa.
- Definir o mínimo de `confidence` por agente/dimensão e o processo de
  calibração (LLMs tendem a reportar confiança mal calibrada).
- Criar processo de validação com golden-set antes de promover uma nova
  versão de prompt para produção (hoje só existe rollback reativo).
- Definir dono/responsável para auditar especificamente a Camada de
  Tradução de Diagnóstico, que atravessa todas as dimensões e pode mascarar
  erro de tradução sobre uma fonte determinística correta.

Detalhamento completo em [[03-Produtos/growth-machine/avaliacao-fluxo]],
bloco "Agentes de IA".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
