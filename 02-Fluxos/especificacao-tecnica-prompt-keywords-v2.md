---
tipo: fluxo
status: ativo
criado: 2026-06-30
ultima-revisao: 2026-06-30
tags: [seo, keywords, prompt, llm, especificacao-tecnica, equipe-tecnologia]
---

# Especificação Técnica — Prompt de Arquitetura de Keywords v2

> Documento técnico de referência para implementação/integração do prompt
> v2. Foca nas características do prompt em si (entrada, processamento,
> saída, regras de validação). Para o histórico da decisão e o comparativo
> completo v1 vs v2, ver [[04-Decisões/migracao-prompt-keywords-v2]]. Para o
> texto integral dos prompts, ver [[02-Fluxos/prompt-avaliacao-keywords]].

## Objetivo do prompt
Gerar a **arquitetura completa de páginas de um site** a partir de uma lista
de keywords, no modelo **Pilar → Cluster → Conteúdo de Suporte**, eliminando
canibalização e redundância semântica. Não é um avaliador de keyword
isolada — é um gerador de estrutura de site.

## 1. Parâmetros de entrada

| Variável | Descrição | Obrigatório |
|---|---|---|
| `{$empresa}` | Nome da empresa | Sim |
| `{$segmentos}` | Segmentos de atuação | Sim |
| `{$tipoEmpresa}` | Fabricante / Distribuidor / Prestador de Serviços etc. — define o lado da transação (compra vs. contratação) | Sim |
| `{$publico}` | Público-alvo da empresa | Sim |
| `{$nomePrincipal}` | Nome principal do produto/serviço | Sim |
| `{$nomeSecundario}` | Sinônimo/nome alternativo do produto | Não |
| `{$tipo}` | Tipo de produto/serviço | Sim |
| `{$especificacao}` | Especificação técnica do produto | Não |
| `{$funcionalidades}` | Funcionalidades — fonte de long-tails de oportunidade | Sim |
| `{$beneficios}` | Benefícios — fonte de long-tails de oportunidade | Sim |
| `{$keywords}` | Lista bruta de keywords a processar | Sim |

**Nota de implementação**: comparado ao v1, os campos `{$outrosNomes}`,
`{$publicoAlvoProduto}` e `{$informacoesAdicionais}` não têm equivalente
direto no v2 — não enviar sem antes validar se serão absorvidos por
`{$publico}`/`{$funcionalidades}`/`{$beneficios}` ou descartados.

## 2. Princípios de processamento (regras de negócio do prompt)
1. **Pilar ≠ Cluster** — pilar é macro-intenção de alta autoridade; cluster
   é sub-intenção real de serviço/problema específico.
2. **Uma intenção = uma página** — variações linguísticas/sinônimos
   ("conserto", "reparo", "assistência") não geram páginas novas.
3. **Anti-canibalização obrigatória** — se duas keywords podem ranquear na
   mesma página, devem ser agrupadas no mesmo cluster.
4. **Consolidação forte** — regra de desempate: na dúvida entre separar ou
   juntar clusters, sempre juntar.
5. **SEO local é um pilar, não uma lista à parte** — variações geográficas
   (cidade/bairro/"perto de mim") entram como o pilar "Local SEO", não como
   anexo separado.

## 3. Estrutura de saída obrigatória (3 níveis)

| Nível | Tipo de página | Intenção | Exemplo |
|---|---|---|---|
| 1 | Página Pilar | Alta busca, alta competitividade, serviço completo | "assistência técnica notebook" |
| 2 | Página Cluster | Sub-serviço, problema específico, ação técnica | "troca de tela" |
| 3 | Conteúdo de Suporte (blog) | Informacional, diagnóstico, educação do usuário | "por que notebook esquenta" |

O prompt tenta cobrir 5 tipos obrigatórios de pilar: Assistência Técnica
(geral), Marcas, Serviços críticos, Local SEO, Orçamento/suporte comercial.

## 4. Pipeline interno do prompt (etapas)
1. **Análise individual de keyword** — intenção (comercial / transacional /
   informacional / navegacional), objetivo da busca (comprar, orçamento,
   suporte, manutenção, comparação, preço, funcionamento, diagnóstico,
   outro), tipo (head / médio / long tail), relevância (0–5). Descarte
   automático de termos irrelevantes, concorrentes diretos ou genéricos sem
   contexto.
2. **Clusterização semântica** — agrupamento em Pilares / Clusters /
   Suporte seguindo as regras da seção 2.
3. **Definição de arquitetura final** — para cada pilar e cluster: tipo de
   página, nome, URL sugerida (SEO friendly), keyword principal, keywords
   incluídas, intenção dominante.
4. **Saída final** — três blocos (ver seção 5).

## 5. Formato de saída — 3 blocos (parsing)
A resposta do modelo deve ser tratada pela aplicação como 3 seções
distintas, não uma tabela única:

1. **Arquitetura completa** — lista de pilares, cada um com: nome,
   intenção, URL, keyword principal e seus clusters aninhados (nome, URL,
   keywords incluídas, intenção).
2. **Mapeamento completo de keywords** — tabela: keyword, intenção,
   objetivo da busca, relevância (0–5), nível (pilar/cluster/suporte),
   cluster/página de destino, justificativa curta.
3. **Decisões estratégicas** — pilares prioritários (top 20% SEO), clusters
   mais lucrativos, oportunidades ocultas de conteúdo, riscos de
   canibalização evitados, keywords descartadas (relevância 0).

**Impacto técnico**: qualquer parser do output do v1 (1 linha = 1 keyword)
precisa ser reescrito — o v2 não é compatível com esse parsing.

## 6. Critérios de descarte automático (relevância = 0)
- Keyword em outro idioma ou tópico não relacionado ao produto.
- Head term genérico sem qualificador ligado ao produto/segmento.
- Descreve produto diferente do avaliado, mesmo que do mesmo segmento.
- Refere-se a marca/concorrente alheio sem relação com o que a empresa vende.

## 7. Riscos / pontos de atenção para implementação
- Saída mais longa e estruturada que o v1 — validar limite de
  tokens/contexto conforme volume de `{$keywords}` de entrada.
- URLs sugeridas pelo prompt são uma proposta, não uma validação contra
  URLs já existentes no site — a aplicação ainda precisa checar conflito
  com páginas reais antes de publicar.
- O prompt não define versionamento de pilares/clusters ao longo do tempo
  (o que fazer quando um novo lote de keywords não se encaixa nos pilares já
  criados anteriormente) — ainda não coberto, candidato a item de backlog.

## Notas relacionadas
- [[00-Cerebro]]
- [[02-Fluxos/estudo-de-keywords]]
- [[02-Fluxos/prompt-avaliacao-keywords]]
- [[04-Decisões/migracao-prompt-keywords-v2]]
