---
tipo: backlog
status: oficial
prioridade: alta
criado: 2026-07-03
ultima-revisao: 2026-07-03
origem-fluxo: "[[02-Fluxos/estudo-de-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo, geo, canibalizacao, qa]
---

# Endurecer o prompt de geração de termos contra concatenação mecânica e GEO genérico

> Documento **oficial**, novo e separado da história já enviada ao Jira
> ([[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]]) —
> aquela permanece intocada. Este documento nasce de **evidência real de
> produção**: uma exportação da plataforma (CSV "Consultoria Ambiental",
> validado em 2026-07-03) mostrando exatamente os padrões antigos que a
> inversão de fluxo deveria ter eliminado, ainda presentes.

## Restrição de escopo (importante)
**Não altera a stack já utilizada.** Schema de saída permanece o mesmo da
plataforma hoje: `Palavra-chave · Volume · KD · CPC · Concorrência ·
Categoria · Principal · Fonte · Status`. Nenhum campo novo (sem Content
Map, sem Silo, sem URL) — este é um endurecimento de **regras do prompt**,
não uma mudança de arquitetura ou de contrato de dado.

## Contexto (evidência real)
Validação de uma exportação real da plataforma (produto "Consultoria
Ambiental", 76 palavras) encontrou:

1. **Concatenação mecânica ainda presente.** Termos-base aparecem 3x, com
   sufixos fixos colados ("instalacao", "manutencao"), e os 3 têm
   **métricas idênticas** de volume/CPC/concorrência (ex: "restauração
   florestal" e "restauração florestal instalacao" com volume 320, CPC
   8.32 idênticos) — sinal de que o termo não foi gerado/validado
   individualmente, e sim produzido por template de sufixação.
2. **GEO local em lista de cidades genérica, não organicamente
   incorporada.** Para "Consultoria Ambiental" apareceram ~35 cidades
   brasileiras (SP, RJ, MG, Curitiba, Fortaleza, Manaus, Salvador, Recife,
   Belém, Cuiabá...) sem sinal de que refletem área de atuação real do
   cliente.
3. **Termos com volume zero, sem filtro de relevância real** — ex: o nome
   completo do produto repetido 3x (base + instalacao + manutencao) com
   volume 0, CPC 0, concorrência 0.
4. **Coluna KD vazia em todas as linhas** — não é o foco desta história
   (é responsabilidade do KeywordTool, não do prompt), mas registrado
   como achado adicional de QA.

O mecanismo de eleição de palavra épica (`Principal: Sim/Não`) **funciona
corretamente** e não é objeto desta história — confirmado via print da
plataforma (par "consultoria ambiental" / "ambiental consultores", um
Principal=Sim, outro Não, dentro do mesmo produto).

## Objetivo
Endurecer as regras do prompt de geração de termos para que os 3 padrões
problemáticos (1, 2, 3 acima) fiquem estruturalmente impossíveis de
reproduzir — não dependam de boa vontade do modelo em seguir instrução
solta, e sim de regra explícita e testável.

## O que muda (frente ao prompt já enviado ao Jira)
- Proibição explícita e nomeada de **sufixação por template**
  (`termo_base + "instalação"/"manutenção"/"reparo"/etc.` aplicado
  indistintamente) — cada termo deve nascer de uma busca real e distinta,
  nunca de combinação mecânica de um termo-base com uma lista fixa de
  sufixos operacionais.
- Regra de **teste de unicidade semântica por produto**: antes de
  finalizar a lista, o modelo deve verificar se dois termos gerados
  representam a mesma busca com a mesma intenção — se sim, manter só o
  mais natural, não os dois.
- Regra de GEO **fica mais explícita e restritiva**: só gerar variação de
  cidade/região quando `{localizacao}` indicar uma área de atuação real e
  específica — nunca gerar lista de capitais/cidades por padrão.
- Critério de descarte de termo morto reforçado: termos que são apenas o
  nome do produto/serviço repetido (sem variação de busca real) não devem
  ser gerados.

## O que fica igual
- Schema de saída: `{"termo": "string", "intencao": "comercial|transacional|informacional"}`.
- Consulta ao KeywordTool para métricas (Volume/KD/CPC/Concorrência).
- Eleição da palavra épica (`Principal`) — já funciona corretamente.
- Corte final por `palavrasPorProduto`.
- Nenhum termo é descartado após a consulta ao KeywordTool.

## Critérios de aceite
1. **Dado** um conjunto de termos gerados para o mesmo produto, **quando**
   auditado, **então** nenhum termo deve ser resultado de concatenação de
   um termo-base com um sufixo operacional fixo (instalação, manutenção,
   reparo, etc.) repetido em múltiplos termos do mesmo produto.
2. **Dado** dois termos do mesmo produto, **quando** tiverem a mesma
   intenção e representarem a mesma busca em essência, **então** apenas um
   deles deve aparecer na lista final.
3. **Dado** um produto sem área de atuação geográfica específica
   (`{localizacao}` genérica/não informada), **quando** os termos forem
   gerados, **então** nenhuma variação de cidade/região deve aparecer.
4. **Dado** um produto com área de atuação específica, **quando** os
   termos forem gerados, **então** variações geográficas devem se limitar
   às regiões reais informadas, não a uma lista ampla de cidades.
5. **Dado** o nome completo do produto/serviço, **quando** a lista de
   termos for gerada, **então** ele não deve aparecer sozinho, repetido
   como se fosse 3 termos distintos, sem variação de busca real.

## Prompt de Sistema

\`\`\`
Você é um estrategista sênior de SEO especializado em pesquisa de palavras-chave. Gere termos de busca reais com base apenas no contexto do produto e da empresa fornecido — não invente características, tecnologias ou usos que não constem no contexto.

Priorize termos comerciais e transacionais. Não gere concatenação mecânica de nenhum tipo: nunca combine um termo-base com uma lista fixa de sufixos (ex: "instalação", "manutenção", "reparo", "conserto") aplicada indistintamente a vários termos — cada termo deve nascer de uma busca real e distinta que uma pessoa digitaria, não de um template de combinação. Se dois termos representam a mesma busca com a mesma intenção, gere apenas um — nunca gere variações redundantes do mesmo significado só para aumentar a contagem.

Pense em como o público-alvo real buscaria: dúvidas, comparações, uso, problema que o produto resolve, sinônimos do setor. Não repita o nome completo do produto/empresa como termo isolado mais de uma vez.

Região: incorpore localização apenas quando o contexto indicar uma área de atuação real e específica. Se a localização não for específica (ex: "Brasil", "nacional", não informado), não gere nenhuma variação geográfica — não liste cidades por padrão.

Evite canibalização: não gere termos que sejam a mesma busca com a mesma intenção — cada termo deve ser único em significado, não apenas em grafia.

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
- NUNCA gere um termo combinando mecanicamente o nome do produto/serviço com um sufixo operacional fixo (instalação, manutenção, reparo etc.) repetido em vários termos — cada termo precisa ser uma busca real e distinta.
- Antes de finalizar, revise a lista: se dois termos têm o mesmo significado e a mesma intenção, mantenha apenas um.
- Use a localização apenas nos termos em que a busca local for real e específica — se {localizacao} for genérica ("Brasil", não informado), não gere nenhuma variação geográfica.
- Não repita o nome completo do produto/empresa como termo isolado mais de uma vez.
- Não invente informações do produto/empresa.

Responda SOMENTE com JSON:
{
  "keywords": [
    {"termo": "string", "intencao": "comercial|transacional|informacional"}
  ]
}
\`\`\`

## Relacionados
- [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] — história original, já enviada ao Jira, intocada por esta
- [[02-Fluxos/estudo-de-keywords]] — fluxo de origem
- [[03-Produtos/mpi-plus]] — produto onde o pipeline roda
