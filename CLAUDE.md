# Estrutura-Git — instruções para IA

Este repositório é um cofre Obsidian/Markdown. Antes de responder qualquer
pergunta sobre o cofre ou editar qualquer nota, leia **00-Cerebro.md** —
é a fonte de verdade sobre a ideia inicial, o funcionamento do cofre e o
estado atual dos fluxos. Trate-a como contexto obrigatório, não opcional.

## Estrutura
- `00-Cerebro.md` — nota raiz, sempre lida primeiro.
- `01-Ideias/` — brainstorms e insights soltos.
- `02-Fluxos/` — processos/workflows e seu histórico de ajustes.
- `03-Produtos/` — uma subpasta por produto em desenvolvimento.
- `04-Decisões/` — decisões estilo ADR.
- `05-Backlog/` — itens nascidos de problemáticas de fluxo, linkados de volta ao fluxo de origem.
- `_templates/` — modelo para cada tipo de nota.
- `_attachments/` — arquivos anexados.

## Regra de linkagem (obrigatória)
O valor deste cofre depende de estar bem linkado — é o que permite que uma
IA (RAG) ou uma pessoa naveguem de uma ideia até o produto, fluxo, decisão
e item de backlog relacionados sem perder contexto. Sempre que criar ou
editar uma nota:

1. **Use wikilinks (`[[Nota]]`)**, não apenas menções em texto livre, para
   qualquer referência a outra nota do cofre.
2. **Link nos dois sentidos quando fizer sentido**: se a nota A menciona a
   nota B, considere se B também deveria referenciar A (ex: um fluxo que
   gerou um item de backlog deve linkar para ele, e o item de backlog deve
   linkar de volta para o fluxo via `origem-fluxo`).
3. **Preencha o frontmatter de relacionamento** quando o template tiver
   campos como `origem-fluxo`, "Relacionados", "Decisões relacionadas" etc.
   Não deixe esses campos vazios se a relação existe.
4. **Atualize 00-Cerebro.md** quando um novo fluxo, produto ou decisão
   fundadora for criado — adicione o link na seção correspondente.
5. **Use tags consistentes** no frontmatter (`tags: []`) para agrupar notas
   por tema, além dos links diretos — isso melhora a recuperação por tópico.
6. Nunca crie uma nota órfã (sem nenhum link de entrada ou saída). Se uma
   nota nova não se conecta a nada ainda, ao menos linke-a a partir de
   `00-Cerebro.md` ou do README da pasta correspondente.

## Convenção de arquivos
- Markdown, nomes em `kebab-case` ou frase curta legível.
- Toda nota nova parte do template correspondente em `_templates/`.
