---
tipo: decisao
status: aceita
criado: 2026-06-30
tags: [seo, keywords, prompt, llm, arquitetura-site, equipe-tecnologia]
---

# Migração do prompt de avaliação de keywords (v1 → v2)

> Documento de validação para a equipe de tecnologia: o que muda, por que
> muda e o que precisa ser ajustado na integração (parâmetros de entrada e
> formato de saída).

## Contexto
O prompt v1, em produção, avalia cada keyword isoladamente (intenção,
especificidade, relevância 0-5, justificativa) e devolve uma tabela linear
de keywords pontuadas. Esse modelo não agrupa por intenção, não detecta
quando duas keywords aprovadas vão competir pela mesma página
(canibalização) e trata variação local como informação solta — o que gerava
risco de conteúdo duplicado/desalinhado, conforme registrado em
[[02-Fluxos/estudo-de-keywords]].

O ajuste foi pedido para que o estudo de keywords pare de pensar em
"keyword única" e passe a pensar em **clusterização por intenção**, sem
canibalização, com variações locais dentro do próprio cluster — ver
histórico de ajustes em [[02-Fluxos/estudo-de-keywords]].

## Decisão
Substituir o prompt v1 pelo v2 (texto completo de ambos em
[[02-Fluxos/prompt-avaliacao-keywords]]). O v2 muda o escopo do prompt: ele
deixa de devolver apenas uma avaliação de keywords e passa a devolver a
**arquitetura completa de páginas do site**, no modelo **Pilar → Cluster →
Conteúdo de Suporte**.

### Diferenças v1 → v2

| Dimensão | v1 (anterior) | v2 (vigente) |
|---|---|---|
| Unidade de análise | Keyword isolada | Cluster de keywords por intenção real |
| Saída principal | Tabela de keywords avaliadas | Arquitetura de site (pilares + clusters + suporte) + tabela de keywords + decisões estratégicas |
| Canibalização | Não verificada | Regra explícita: "se duas keywords podem ranquear na mesma página → agrupar"; relatório final lista riscos evitados |
| Variação local | Não tratada (ausente do prompt) | Vira um tipo obrigatório de pilar ("Local SEO — cidade/bairro"), não uma lista separada |
| Estrutura de páginas | Nenhuma — o prompt não decide página, só pontua termo | 3 níveis obrigatórios: Página Pilar, Página Cluster, Artigo de Blog (suporte) |
| Categorias de intenção | comercial / transacional / informacional / navegacional | mantém as mesmas 4, mas adiciona "objetivo da busca" (comprar, orçamento, suporte, manutenção, comparação, preço, funcionamento, diagnóstico, outro) |
| Especificidade | head / médio / long_tail | mantém head / médio / long tail, agora por keyword dentro do cluster |
| Relevância | 0–5 por keyword, com critério de descarte automático (0) | mantém 0–5 e descarte automático, mas a decisão final de manter/descartar também considera o cluster, não só a keyword |
| Regra de desempate | Não existe | "Na dúvida entre separar ou juntar → SEMPRE juntar" (consolidação forte) |
| Pilares obrigatórios | Não se aplica (não gera pilares) | Exige tentar cobrir 5 tipos: Assistência/serviço geral, Marcas, Serviços críticos, Local SEO, Orçamento/suporte comercial |

### Parâmetros de entrada — o que muda na integração
- v1 usava variáveis no formato `{$empresaNome}`, `{$segmentosAtuacao}`,
  `{$tipoEmpresa}`, `{$publicoAlvoEmpresa}`, `{$nomePrincipal}`,
  `{$nomeSecundario}`, `{$outrosNomes}`, `{$tipoProduto}`,
  `{$especificacaoTecnica}`, `{$funcionalidades}`, `{$beneficios}`,
  `{$publicoAlvoProduto}`, `{$informacoesAdicionais}`.
- v2 renomeia parte delas e adiciona um bloco de keywords como entrada
  direta: `{$empresa}`, `{$segmentos}`, `{$tipoEmpresa}`, `{$publico}`,
  `{$nomePrincipal}`, `{$nomeSecundario}`, `{$tipo}`, `{$especificacao}`,
  `{$funcionalidades}`, `{$beneficios}`, `{$keywords}`.
- **Atenção da equipe de tecnologia**: os nomes de variável não são
  100% compatíveis com o v1 (ex.: `{$segmentosAtuacao}` → `{$segmentos}`,
  `{$tipoProduto}` → `{$tipo}`, `{$especificacaoTecnica}` →
  `{$especificacao}`). Os campos `{$outrosNomes}`, `{$publicoAlvoProduto}` e
  `{$informacoesAdicionais}` do v1 não têm equivalente direto no v2 e não
  devem ser enviados sem antes confirmar se o v2 precisa deles. É necessário
  mapear o template de chamada do prompt (camada de aplicação) para essas
  novas chaves antes de trocar a versão em produção.

### Formato de saída — o que muda no parsing
- v1: saída é uma lista/tabela simples (intenção, especificidade,
  relevância, justificativa) por keyword — parsing direto, 1 linha = 1
  keyword.
- v2: saída tem 3 blocos obrigatórios que a aplicação precisa tratar
  separadamente:
  1. Arquitetura completa (pilares com seus clusters aninhados, cada um com
     nome, URL sugerida, keyword principal, keywords incluídas, intenção);
  2. Mapeamento completo de keywords (tabela: keyword, intenção, objetivo da
     busca, relevância, nível [pilar/cluster/suporte], cluster/página
     destino, justificativa);
  3. Decisões estratégicas (pilares prioritários, clusters mais lucrativos,
     oportunidades ocultas, riscos de canibalização evitados, keywords
     descartadas).
- Isso significa que qualquer parser/consumidor do output do prompt
  precisa ser reescrito — não é compatível com o parser do v1.

## Alternativas consideradas
- Manter o v1 e adicionar só uma etapa de "agrupamento" por fora do prompt
  (pós-processamento): descartado porque o agrupamento por intenção real
  exige que o próprio modelo raciocine sobre as keywords em conjunto, e
  fazer isso fora do prompt perderia contexto semântico (sinônimos,
  variações locais) que o LLM resolve melhor durante a própria avaliação.
- Versionar o v2 como prompt totalmente novo, sem histórico do v1:
  descartado por quebrar a rastreabilidade exigida pela regra de linkagem
  do cofre — o v1 continua registrado em
  [[02-Fluxos/prompt-avaliacao-keywords]] para referência e auditoria.

## Consequências
- **Positivo**: o time deixa de receber só uma lista de keywords pontuadas
  e passa a receber a arquitetura de páginas pronta para virar backlog de
  conteúdo, com canibalização já checada e SEO local já incorporado.
- **Positivo**: histórico de versões fica registrado e linkado — qualquer
  ajuste futuro do prompt deve ser comparado contra este documento.
- **Negativo / ação necessária**: a equipe de tecnologia precisa atualizar
  (a) o template de variáveis de entrada da chamada ao LLM e (b) o parser
  do output, pois o v2 não é drop-in compatible com o v1 (ver seções acima).
- **Negativo / risco**: a saída do v2 é mais longa e estruturada (3 blocos
  obrigatórios) — pode exigir ajuste de limite de tokens/contexto na
  chamada, a depender do volume de keywords de entrada.

## Relacionados
- Prompt completo (v1 e v2): [[02-Fluxos/prompt-avaliacao-keywords]]
- Fluxo de origem: [[02-Fluxos/estudo-de-keywords]]
- Especificação técnica detalhada (entrada, pipeline, formato de saída, riscos de implementação): [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]]
