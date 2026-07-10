---
tipo: decisao
status: aceita
criado: 2026-07-10
tags: [growth-machine, cluster, contrato, informacoes, artigos, seo, geo, aeo, google-2026, gregory]
---

# Cluster via /informacoes e /artigos como camada de ranqueamento fora do contrato

## Contexto
O contrato comercial vende **páginas por palavra-chave** (modelo
keyword-a-keyword), mas o Google recompensa **cluster, entidade e
intenção** (topical authority, absorvido no core ranking / Helpful
Content). Os core updates de março/maio de 2026 miram explicitamente
**scaled content abuse** — sites com páginas em massa por
modificador/variação, sem camada editorial, caíram 50–80% de tráfego.

O caso real do site emtecorp.com.br (DR 6, ~0 backlinks por página,
padrão de LPs por modificador — `empresa-`/`fornecedores-`/`fabrica-`
sobre o mesmo produto) evidenciou esse risco em produção — ver
[[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]].

O próprio PRD de estudo entregue pelo Gregory (Etapa 0 — Pré-mapeamento)
**exclui `/informacoes` e `/artigos` do crawl de páginas MPI contratadas**
— ou seja, essas subcategorias já não fazem parte do que é vendido por
keyword, e existem como padrão replicado em todos os domínios da casa.

Análise completa em
[[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]].

## Decisão
Adotar o **cluster wrapping**, escopo **só aditivo**:

1. A página MPI contratada continua sendo o **pilar** — o cliente recebe
   exatamente o entregável comprado. **O contrato não é alterado.**
2. `/informacoes` e `/artigos` passam a ser estruturados como o **cluster
   de suporte** — conteúdo editorial informacional (intenção que a página
   comercial não serve), com profundidade, entidade e sinais de E-E-A-T.
3. A **linkagem interna sobe do cluster para o pilar** (auditada pela
   Dimensão 3), elevando a autoridade temática da página vendida.
4. Conteúdo answer-first/extraível no cluster serve GEO/AEO (citabilidade
   em IA), sem prometer medição de citação no MVP (mantido para Fase 2,
   decisão F-28).

**Escopo explicitamente excluído desta decisão:** consolidar ou remover as
páginas-modificador (doorway) já existentes (`empresa-`, `fornecedores-`,
`fabrica-` etc.). Essa ação tocaria entregáveis já aprovados pelo cliente e
esbarra na RN-84 (hoje bloqueia sugestão de remoção) — fica para uma
decisão posterior, condicionada ao ajuste da RN-84.

## Por que resolve sem tocar o contrato
O contrato define o **entregável** ("página que ranqueia para a
keyword X"), não a **arquitetura** do site. A keyword deixa de ser uma
página isolada e passa a ser a porta de entrada de um cluster: o pilar é a
página vendida, o cluster de apoio é conteúdo aditivo da casa. Mudou o
**como** se ranqueia, não o **quê** foi vendido.

## Alternativas consideradas
- **Renegociar o contrato para vender cluster** — descartado por ora: alta
  fricção comercial, ciclo lento, não resolve o risco urgente de doorway.
- **Reconstruir as páginas MPI existentes em formato de cluster** —
  descartado para esta decisão: altera o entregável já aprovado, esbarra na
  RN-84; fica como evolução possível, não parte desta decisão.
- **Seguir a concatenação prescrita literalmente pelo Gregory
  (palavra×região×tipo em escala)** — descartado como estratégia primária:
  é exatamente o padrão que os core updates 2026 penalizam quando aplicado
  em escala sem camada editorial humana.

## Consequências
- **Positivo**: ganho de ranqueamento sem risco comercial/contratual — a
  ação é puramente aditiva.
- **Positivo**: antídoto direto ao padrão doorway/scaled content já
  observado em produção (emtecorp e replicável em outros domínios da casa).
- **Positivo**: cobre lacunas já mapeadas (E-E-A-T on-page, conteúdo
  original, extrabilidade GEO/AEO) sem abrir nova frente comercial.
- **Negativo / ação necessária**: exige **camada editorial humana** real
  para o conteúdo de `/informacoes` — não pode ser gerado em escala
  mecânica, sob pena de recriar o mesmo risco que motivou a decisão.
- **Negativo / ação necessária**: define-se convenção para não confundir
  conteúdo de cluster (`/informacoes`, fora do teto de pacote) com
  bonificação de palavras contratual (RN-85, dentro do teto de 50% do
  pacote) — âmbitos diferentes, mesma superfície de produto.
- **Estrutura na GM**: Dim 1 (estudo passa a mapear o cluster), Dim 3
  (audita linkagem cluster→pilar e a canibalização entre subdomínios), Dim
  2 (gera o conteúdo do cluster) — ver
  [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]].

## Relacionados
- Análise completa: [[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]]
- Origem do padrão de risco: [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]]
- Estruturação por dimensão: [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]]
- PRD de estudo do Gregory (exclui /informacoes e /artigos): [[03-Produtos/growth-machine/reconciliacao-regras-gregory]]
- Fluxo de cluster/silo que sustenta a decisão: [[02-Fluxos/estudo-de-keywords]]
- PRD consolidado: [[03-Produtos/growth-machine/prd-v2-mvp]]
- [[03-Produtos/growth-machine]] · [[00-Cerebro]]
