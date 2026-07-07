---
tipo: decisao
status: aceita
criado: 2026-07-02
tags: [jira, historia, template, padronizacao]
---

# Padronizar formato de história Jira no cofre

## Contexto
Duas histórias reais para o MPI Plus já foram escritas e validadas neste
formato: [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]]
(arquitetura de site) e
[[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] (geração
de termos). Ambas convergiram, por tentativa e ajuste, para a mesma
estrutura: Contexto → Objetivo → O que muda → O que fica igual → Critérios
de aceite → Definições pendentes → Prompt de Sistema/Usuário (quando
aplicável) → Relacionados.

O MCP do Jira ainda não está conectado neste ambiente — as histórias hoje
existem só como notas no cofre, para depois virarem cards reais.

## Decisão
Formalizar esse formato como `_templates/template-historia-jira.md` e usá-lo
como ponto de partida para toda história de mudança de comportamento
técnico documentada no cofre (prompt, fluxo de sistema, integração), estilo
Jira, quer o item exista fisicamente no board ainda ou não.

Quando o MCP do Jira for conectado, esse padrão já validado deve minimizar
retrabalho: os campos do template mapeiam diretamente para os campos
esperados num card (título, descrição/contexto, critérios de aceite) — a
inteligência de formato já fica pronta na RAG do cofre.

## Alternativas consideradas
- Usar o `_templates/template-backlog.md` genérico para histórias Jira
  também: descartado porque o formato genérico não força Critérios de
  Aceite no formato Dado/Quando/Então nem separa "o que muda" de "o que
  fica igual" — duas seções que se mostraram essenciais para o time
  técnico não reabrir escopo já decidido.

## Consequências
- **Positivo**: qualquer história nova de mudança técnica no cofre já nasce
  no formato que o Jira vai esperar, reduzindo fricção quando o MCP for
  conectado.
- **Positivo**: força o autor (ou a IA) a explicitar "definições pendentes"
  antes de considerar a história pronta para dev — evita histórias com
  ambiguidade escondida dentro dos critérios de aceite.
- **Negativo/atenção**: quando o MCP do Jira for conectado, será necessário
  mapear explicitamente os campos deste template para os campos reais do
  board (Epic, Tipo, prioridade, labels) — o template não assume uma
  estrutura de projeto Jira específica ainda.

## Relacionados
- [[_templates/template-historia-jira.md]]
- [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]]
- [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]]
- [[05-Backlog]]
