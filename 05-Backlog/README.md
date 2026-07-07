# Backlog

Itens nascidos de problemáticas identificadas em [[02-Fluxos]]. Cada item linka de volta ao fluxo de origem (campo `origem-fluxo` no frontmatter) e, quando aplicável, ao produto e à decisão relacionados.

Use `_templates/template-backlog.md` como ponto de partida.

Itens daqui devem ser referenciados em [[00-Cerebro]] na seção "Backlog gerado" enquanto estiverem ativos.

## Histórias Jira
Quando o item de backlog é uma história pronta para virar card no Jira
(com prompt de IA envolvido ou não), use `_templates/template-historia-jira.md`
em vez do template genérico — segue o formato padronizado (Contexto,
Objetivo, O que muda/fica igual, Critérios de aceite, Definições
pendentes, Prompt de Sistema/Usuário quando aplicável) validado em
[[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]] e
[[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]]. Esse
padrão existe para ficar consistente quando o MCP do Jira for conectado —
a RAG do cofre já entrega o histórico no formato certo para virar card.
