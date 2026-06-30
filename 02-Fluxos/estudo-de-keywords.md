---
tipo: fluxo
status: ativo
criado: 2026-06-30
ultima-revisao: 2026-06-30
tags: [seo, keywords, prompt]
---

# Estudo de Keywords

## Objetivo
Definir como o prompt/processo de estudo de keywords deve pensar a pesquisa
de termos para gerar conteúdo, evitando abordagem ingênua de keyword única
e produzindo agrupamentos que realmente convertem em estrutura de conteúdo.

## Etapas
1. Levantar o universo de termos relacionados ao tópico (não uma keyword isolada).
2. Agrupar os termos em **clusters** por intenção de busca, não por volume isolado.
3. Mapear quais termos do cluster apontam para a mesma página, evitando
   que duas páginas diferentes disputem a mesma intenção (**canibalização**).
4. Incluir variações **locais** (cidade/região/“perto de mim”) como parte
   do cluster, não como lista separada — elas pertencem à mesma intenção,
   só com modificador geográfico.
5. Validar o cluster final antes de gerar conteúdo, conferindo que cada
   página-alvo tem um cluster próprio e exclusivo.

## Responsáveis
-

## Histórico de ajustes
| Data | Mudança | Motivo |
|------|---------|--------|
| 2026-06-30 | Prompt passou a pensar em **clusterização de termos** em vez de keyword isolada | O estudo padrão sempre partiu direto da keyword, sem agrupar por intenção, o que gerava risco de conteúdo desalinhado e sobreposição entre páginas |
| 2026-06-30 | Adicionada checagem de **canibalização**: cada cluster deve mapear para uma única página-alvo | Termos próximos estavam sendo direcionados para páginas diferentes, fazendo elas competirem entre si no ranqueamento |
| 2026-06-30 | Variações **locais** passaram a ser tratadas como parte do mesmo cluster de intenção, não como lista à parte | Tratar localização separadamente fragmentava o cluster e perdia a relação de intenção entre o termo genérico e sua variação geográfica |

## Problemáticas identificadas
- Estudo anterior gerava listas de keywords soltas sem agrupamento por intenção → ver [[05-Backlog]] para itens derivados.

## Cruzamento com transcrições (Notion, 2026-06-30)
- [[02-Fluxos/processo-kickoff-discovery]] — no Discovery, o "questionamento de
  palavras-chave" e o "mapear para validar fluxo" são o ponto onde esse
  estudo de keywords começa, antes de virar cluster formal.
- [[03-Produtos/growth-machine]] — implementação de blog e conteúdo MPI Plus
  dependem deste fluxo para não cair em keyword isolada.

## Prompt operacional
A materialização prática deste fluxo num prompt de IA está versionada em
[[02-Fluxos/prompt-avaliacao-keywords]] — o prompt v1 em uso ainda não
incorpora clusterização, anti-canibalização nem variação local; é o que está
sendo desenhado agora na v2.

## Notas relacionadas
- [[00-Cerebro]]
- [[02-Fluxos/processo-kickoff-discovery]]
- [[02-Fluxos/prompt-avaliacao-keywords]]
- [[03-Produtos/growth-machine]]
