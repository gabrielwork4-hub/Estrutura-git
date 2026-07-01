---
tipo: backlog
status: pronto-para-refinamento
prioridade: alta
criado: 2026-07-01
ultima-revisao: 2026-07-01
origem-fluxo: "[[02-Fluxos/prompt-avaliacao-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo]
---

# [MPI-XXX] Substituir prompt de avaliação de keywords pelo Estudo SEO Clusterizado (v3)

> História redigida na posição de PO, para o time de DEV. Título/ID Jira
> (`MPI-XXX`) é placeholder — substituir pelo número real ao criar no board.
> Versão reduzida em 2026-07-01: escopo do prompt cortado para focar em
> palavras-chave para produção de conteúdo mais exata e ajustada — sem
> Briefs de Conteúdo, Internal Linking, KPIs ou Plano de Implementação.
> Documento mantido até a seção de Critérios de Aceite; padronização segue
> em próxima etapa.

## Epic
Evolução do pipeline de Estudo/Keywords do IdealPlus (MPI Plus)

## Tipo
Story (mudança de prompt em produção — sem mudança de infraestrutura)

## Contexto (por que esta história existe)
Hoje, a etapa de avaliação de keywords do MPI Plus roda em cima de um
prompt (v1) que avalia **keyword por keyword, isoladamente** — sem
clusterização, sem checagem de canibalização entre páginas e sem content
map. Essa limitação já está documentada em
[[02-Fluxos/estudo-de-keywords]] e no comparativo
[[04-Decisões/migracao-prompt-keywords-v2]].

O pipeline de **Construção de Conteúdo** do MPI Plus (SERP Search → Domain
Classification → Pattern Analysis → Structure → Section → Cohesion → QA)
já assume uma `{keyword}` pronta como entrada — ele não decide qual
keyword/página deve existir, nem verifica canibalização entre páginas. Essa
decisão acontece **antes** desse pipeline, e é exatamente o prompt que
estamos substituindo.

O novo prompt (**v3**, texto completo em
[[02-Fluxos/prompt-avaliacao-keywords]]) resolve isso, mantendo o foco em
**palavras-chave para produção de conteúdo mais exata e ajustada**: gera
cluster de keywords, content map e análise competitiva/GEO — sem entrar em
escopo de execução (briefs, linkagem, KPIs, cronograma).

## Objetivo da história
Trocar o prompt de produção da etapa de avaliação/clusterização de keywords
(hoje v1) pelo prompt v3, sem alterar o restante do pipeline de Construção
de Conteúdo (SERP Search, Domain Classification, Pattern Analysis,
Structure, Section, Cohesion, QA), que permanece como está.

## Story (formato ágil)
**Como** Product Owner do MPI Plus,
**quero** substituir o prompt de avaliação de keywords existente pelo
prompt v3 (Estudo SEO Clusterizado, focado em keywords),
**para que** o sistema pare de gerar keywords soltas e passe a entregar
cluster de keywords + arquitetura de páginas, sem canibalização, pronto
para alimentar a produção de conteúdo com mais exatidão.

## Escopo desta história (o que muda)

| Item | Hoje (v1) | Depois (v3) |
|---|---|---|
| Unidade de saída | Lista de keywords avaliadas (intenção/especificidade/relevância/justificativa) | Cluster de keywords + content map + análise competitiva + estratégia GEO |
| Volume de keywords | Não especificado | Mínimo 50–80 keywords, organizadas em 8 clusters obrigatórios (Pillar/Core, Problemas/Sintomas, Serviços específicos, Marcas, GEO local, Comparação/preço/decisão, FAQ, Long-tail) |
| Canibalização | Não verificada | Regra explícita: máximo 1 keyword principal por página; content map limitado a 15–25 páginas |
| Critério de corte | Não definido | Descartar (não incluir na tabela final) qualquer keyword com relevância < 3 |
| Análise competitiva | Inexistente | Top 5 concorrentes (DR estimado, tráfego, força, fraqueza, oportunidade de ataque) + 3 oportunidades de ganho de mercado |
| SEO local | Não tratado no prompt de avaliação | Pirâmide de localização (primária/secundária/terciária) com landing page, keywords locais, estratégia de conteúdo e SEO local (GBP, schema, citações) por nível |

**Fora de escopo desta história:**
- Qualquer alteração no pipeline de Construção de Conteúdo
  (`domain_classification`, `pattern_analysis`, `structure`, `section`,
  `cohesion`, `qa`) documentado no guia de prompts do IdealPlus — este
  pipeline continua recebendo `{keyword}` normalmente.
- Briefs de Conteúdo, Internal Linking Strategy, KPIs e Plano de
  Implementação — cortados do prompt v3 em 2026-07-01 para manter o foco em
  keywords/arquitetura, não em execução de conteúdo (ver
  [[02-Fluxos/prompt-avaliacao-keywords]], seção "Escopo intencionalmente
  fora do v3").

## Critérios de aceite
1. **Dado** um briefing de empresa/produto completo, **quando** o estudo
   for executado com o prompt v3, **então** o sistema deve retornar as 4
   seções obrigatórias na ordem: Cluster de Keywords, Content Map, Análise
   Competitiva, Estratégia GEO (quando aplicável).
2. **Dado** o cluster de keywords gerado, **quando** qualquer keyword tiver
   relevância < 3, **então** ela não deve aparecer na tabela final entregue.
3. **Dado** o content map gerado, **quando** for auditado, **então** cada
   página deve ter exatamente 1 keyword principal, sem repetição de keyword
   principal entre páginas (zero canibalização), e o total de páginas deve
   estar entre 15 e 25.
4. **Dado** um nicho sem componente geográfico relevante, **quando** o
   estudo for gerado, **então** a seção de Estratégia GEO pode ser omitida
   ou marcada como não aplicável, sem quebrar o restante da saída.
5. **Dado** o pipeline de Construção de Conteúdo existente, **quando** a
   keyword de uma página do novo content map for usada como `{keyword}` de
   entrada, **então** o pipeline deve continuar funcionando sem alteração
   de contrato/formato de entrada.

## Relacionados
- [[02-Fluxos/prompt-avaliacao-keywords]] — texto completo dos prompts v1, v2 e v3
- [[02-Fluxos/estudo-de-keywords]] — fluxo de origem (clusterização, anti-canibalização, variação local)
- [[04-Decisões/migracao-prompt-keywords-v2]] — decisão e comparativo anterior (v1→v2)
- [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]] — especificação técnica anterior
- [[03-Produtos/mpi-plus]] — produto onde o pipeline roda
