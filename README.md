# Estrutura-Git

Cofre Obsidian que centraliza a ideia inicial, o funcionamento, os ajustes
de fluxos e as informações dos produtos em desenvolvimento.

Comece sempre por **[[00-Cerebro]]** — é a nota raiz com a ideia inicial,
o funcionamento geral e o estado atual dos fluxos e do backlog.

## Estrutura

- **00-Cerebro.md** — nota raiz: ideia inicial, funcionamento, fluxos ativos, problemáticas e backlog. Leitura obrigatória antes de qualquer outra nota.
- **01-Ideias/** — brainstorms, insights soltos, coisas a explorar. Não precisam estar maduras.
- **02-Fluxos/** — processos e workflows (como algo deve funcionar), e ajustes feitos neles ao longo do tempo.
- **03-Produtos/** — uma pasta por produto, com specs, status e contexto de desenvolvimento.
- **04-Decisões/** — registros de decisões (estilo ADR): o que foi decidido, por quê, e alternativas consideradas.
- **05-Backlog/** — itens nascidos de problemáticas identificadas nos fluxos, linkados de volta ao fluxo de origem.
- **_templates/** — modelos para novas notas em cada categoria.
- **_attachments/** — imagens e arquivos anexados às notas.

## Convenções e linkagem

- Arquivos em Markdown, nomes em `kebab-case` ou frases curtas legíveis.
- Use `[[wikilinks]]` para conectar notas relacionadas (ex: uma ideia que virou produto, um fluxo referenciado numa decisão, um problema de fluxo que virou item de backlog).
- Cada nota nova parte do template correspondente em `_templates/`.
- Nenhuma nota deve ficar órfã: toda nota nova precisa de pelo menos um link de entrada (a partir de `00-Cerebro.md` ou do README da pasta) e, quando aplicável, links de saída para notas relacionadas.
- Veja `CLAUDE.md` para as regras completas de linkagem usadas por IA ao ler/editar o cofre.
