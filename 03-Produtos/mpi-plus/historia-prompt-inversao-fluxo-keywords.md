---
tipo: backlog
status: oficial
prioridade: alta
criado: 2026-07-02
ultima-revisao: 2026-07-02
origem-fluxo: "[[02-Fluxos/estudo-de-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo, keywordtool]
---

# Inverter o fluxo de geração de termos: IA gera, KeywordTool só enriquece

> Documento **oficial** (2026-07-02) — história + prompt para o time de DEV,
> ainda sem número Jira (aguardando acesso ao board do MPI Plus). Escopo
> diferente do prompt de arquitetura/cluster documentado em
> [[02-Fluxos/prompt-avaliacao-keywords]] — este documento trata da etapa
> de **geração de termos em si** (upstream), não da clusterização em
> Pilar/Content Map.

## Contexto
Hoje o estudo de keywords parte de sementes enviadas ao Google Autocomplete
via KeywordTool. As sugestões voltam, são filtradas e classificadas por IA,
e no final entram long-tails geradas por concatenação mecânica (keyword +
região + classificação), que nunca recebem métrica real.

Queremos que a IA crie os termos com base no briefing real do
produto/empresa, e o KeywordTool sirva só para trazer os dados
(volume/CPC/concorrência) de cada termo — sem filtrar nada.

## Objetivo
Inverter o fluxo. A IA lê o contexto do briefing e gera a lista final de
termos, sem sementes e sem concatenação. O KeywordTool enriquece cada termo
com seus dados. Nada é descartado depois — a seleção é da IA.

## O que muda
- Remove a coleta de sementes + Google Autocomplete como motor de descoberta.
- Remove a concatenação mecânica de região/classificação.
- A IA gera os termos direto do contexto (empresa, produto, nicho, público,
  localização, objetivo).
- Região é incorporada organicamente pela IA, só onde faz sentido como
  busca real.
- O KeywordTool traz volume/CPC/concorrência de cada termo, sem filtrar.

## O que fica igual
- Consulta ao KeywordTool para trazer as métricas.
- Eleição da palavra épica (maior volume entre comercial/transacional,
  fallback maior volume geral).
- Corte final por `palavrasPorProduto`.

## Critérios de aceite
1. A IA gera os termos a partir do contexto do briefing, sem concatenação e
   sem depender do autocomplete.
2. A saída é um JSON no formato que o sistema já aceita, com `termo` e
   `intencao` por item.
3. O campo `intencao` usa exatamente o enum do código (comercial /
   transacional / informacional).
4. Cada termo gerado é enviado ao KeywordTool para trazer
   volume/CPC/concorrência.
5. Nenhum termo é descartado após a consulta ao KeywordTool — todos os
   termos gerados pela IA permanecem no estudo, com ou sem volume.
6. A eleição da palavra épica continua funcionando (termos sem volume
   simplesmente não competem pela épica).
7. O corte por `palavrasPorProduto` continua funcionando.

## Definições pendentes (fechar antes de dev)
- Quantos termos a IA deve gerar por produto (`min_termos`/`max_termos`) —
  sugestão inicial 40–70.
- Mantém o descarte de informacional na eleição da épica, ou passa a
  guardar informacional também.

## Prompt de Sistema

\`\`\`
Você é um estrategista sênior de SEO especializado em pesquisa de palavras-chave. Gere termos de busca reais com base apenas no contexto do produto e da empresa fornecido — não invente características, tecnologias ou usos que não constem no contexto.

Priorize termos comerciais e transacionais. Não gere concatenação mecânica ("produto + região" repetido em toda a lista); pense em como o público-alvo real buscaria: dúvidas, comparações, uso, problema que o produto resolve, sinônimos do setor. Incorpore região apenas quando refletir uma busca real, não em todos os termos.

Evite canibalização: não gere termos que sejam a mesma busca com a mesma intenção — cada termo deve ser único em significado.

Responda exclusivamente com JSON válido. Sem markdown, sem comentários, sem texto fora do JSON.
\`\`\`

## Prompt de Usuário

\`\`\`
Gere uma lista de termos de busca para este produto/serviço:

Empresa: {company_context}
Produto/Serviço: {product_context}
Nicho: {nicho}
Serviço principal: {servico_principal}
Localização: {localizacao}
Público-alvo: {publico_alvo}
Objetivo: {objetivo}

Diretrizes:
- Gere entre {min_termos} e {max_termos} termos únicos que as pessoas realmente buscariam no Google.
- Priorize intenção comercial e transacional; inclua alguns informacionais relevantes.
- Use a localização só nos termos em que a busca local faz sentido, não em todos.
- Não invente informações do produto/empresa.

Responda SOMENTE com JSON:
{
  "keywords": [
    {"termo": "string", "intencao": "comercial|transacional|informacional"}
  ]
}
\`\`\`

## Relação com o restante do fluxo de keywords
Este documento cobre a **geração/enriquecimento de termos** — a camada mais
upstream do estudo. O prompt de arquitetura de site (Pilar → Cluster →
Content Map → Análise Competitiva → GEO), documentado em
[[02-Fluxos/prompt-avaliacao-keywords]] (v3 oficial), roda **depois** dessa
etapa: consome a lista de termos já enriquecida com volume/CPC/concorrência
real (não mais estimativa qualitativa) para montar clusters e páginas. As
duas histórias são complementares, não concorrentes — cabe validar com o
time técnico se a saída deste prompt (`{termo, intencao}` + métricas do
KeywordTool) é compatível como entrada do prompt de arquitetura.

## Relacionados
- [[02-Fluxos/estudo-de-keywords]] — fluxo de origem
- [[02-Fluxos/prompt-avaliacao-keywords]] — prompt de arquitetura de site (etapa seguinte no fluxo)
- [[03-Produtos/mpi-plus]] — produto onde o pipeline roda
- [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]] — história irmã (arquitetura de páginas)
