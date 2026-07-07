---
tipo: backlog
status: rascunho
prioridade:
criado: {{date}}
ultima-revisao: {{date}}
origem-fluxo: "[[]]"
tags: [jira, historia]
---

# [PROJ-XXX] Título da história

> Placeholder `PROJ-XXX` — substituir pelo número real ao criar no board.
> Status no frontmatter: `rascunho` → `pronto-para-refinamento` → `oficial`
> (quando validado pelo solicitante/PO) → `criado-no-jira` (quando existir
> no board de verdade).

## Contexto
O estado atual, em poucas frases: o que existe hoje, como funciona, qual a
limitação/dor concreta que motiva a mudança. Sem prosa teórica — direto ao
comportamento real do sistema.

## Objetivo
Uma frase: o que deve passar a acontecer depois desta história.

## O que muda
Lista curta e objetiva do que muda no comportamento/saída do sistema.
Usar bullets, não parágrafo.

## O que fica igual
Lista curta do que **não** muda — importante para delimitar escopo e
evitar que o time técnico refaça algo que não precisa ser tocado.

## Critérios de aceite
Numerados, formato Dado/Quando/Então sempre que possível. Cada critério
deve ser verificável objetivamente — nada de "deve funcionar bem".
1. **Dado** ..., **quando** ..., **então** ...
2. ...

## Definições pendentes (fechar antes de dev)
Perguntas ainda em aberto que bloqueiam o início do desenvolvimento — não
esconder isso dentro dos critérios de aceite. Se não houver nenhuma,
remover a seção.
-

## Prompt de Sistema
*(remover esta seção e a próxima se a história não envolver prompt de IA)*

\`\`\`
Texto do prompt de sistema, verbatim.
\`\`\`

## Prompt de Usuário

\`\`\`
Texto do prompt de usuário, verbatim, com variáveis no formato usado pelo
sistema real (`{$variavel}` ou `{variavel}`, conforme o pipeline).
\`\`\`

## Relacionados
- Fluxo de origem: [[]]
- Produto onde roda: [[]]
- Histórias irmãs/dependentes (se houver): [[]]
