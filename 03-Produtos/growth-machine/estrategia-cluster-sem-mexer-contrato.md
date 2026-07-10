---
tipo: produto
status: rascunho
criado: 2026-07-08
ultima-revisao: 2026-07-08
tags: [growth-machine, estrategia, contrato, cluster, entidade, intencao, seo, geo, aeo, informacoes]
candidato-adr: true
---

# Estratégia — ranquear por cluster/entidade/intenção SEM mexer no contrato

> **Problema:** o contrato vende **páginas por palavra-chave** (modelo
> keyword-a-keyword), mas o Google 2026 recompensa **cluster, entidade e
> intenção** (topical authority + Helpful Content). Como melhorar o
> ranqueamento dos ~2.500 sites da casa, alinhado às boas práticas e aos
> core updates, **sem renegociar o contrato**? Nota candidata a ADR.

## A chave já existe na estrutura: `/informacoes` e `/artigos`
O próprio PRD de estudo do Gregory (Etapa 0) **exclui `/informacoes` e
`/artigos` do crawl de páginas MPI** — ou seja, essas subcategorias **não
são as páginas MPI contratadas por keyword**. Elas são o **espaço editorial
livre** do site, fora do escopo do contrato. E existem em todos os domínios
da casa (confirmado no emtecorp; padrão replicado).

**Isso muda o jogo:** dá para inserir cluster/entidade/intenção **em
`/informacoes` e `/artigos`** sem tocar nas páginas vendidas nem no contrato.

## O cenário recomendado — "cluster wrapping" (envelope de cluster)
Manter o que foi vendido e **envelopar** com conteúdo de casa:

1. **A página MPI contratada continua o PILAR** — o cliente segue recebendo
   exatamente o que comprou ("uma página que ranqueia para a keyword X").
   Contrato intacto.
2. **`/informacoes` + `/artigos` viram o CLUSTER de suporte** — conteúdo
   editorial informacional (intenção informacional que a página comercial
   não serve), com profundidade, entidade e E-E-A-T.
3. **Linkagem interna sobe do cluster para o pilar** (Dim 3) — a autoridade
   temática flui do conteúdo de apoio para a página vendida, **elevando o
   ranqueamento do que foi contratado**.
4. **Conteúdo answer-first / extraível** no cluster serve GEO/AEO (ser
   citado em IA), sem prometer medição (Fase 2, F-28).

### A reinterpretação que dispensa mexer no contrato
O contrato define o **entregável** ("página que ranqueia para a keyword"),
não a **arquitetura**. A keyword deixa de ser uma página isolada e passa a
ser a **porta de entrada de um cluster**: o pilar é a página vendida; o
cluster de apoio é conteúdo da casa. **Mudou o COMO se ranqueia, não o QUE
foi vendido** — por isso não toca o contrato nem exige aprovação comercial.

## Por que é o melhor cenário (vs. alternativas)
| Cenário | Toca contrato? | Risco | Veredito |
|---|---|---|---|
| **A. Renegociar p/ vender cluster** | Sim | Fricção comercial, lento | ❌ agora não |
| **B. Reconstruir as páginas MPI em cluster** | Sim (altera entregável) | Mexe no que foi aprovado; RN-84 bloqueia poda | ⚠️ fase posterior |
| **C. Envelope de cluster em `/informacoes`** | **Não** | Baixo — é conteúdo aditivo | ✅ **recomendado** |

## Por que isso ganha ranqueamento nos core updates 2026
- **Helpful Content / core mar-mai/2026:** recompensa profundidade
  editorial original — exatamente o que `/informacoes` passa a entregar.
- **Topical authority:** o cluster de apoio prova autoridade no tema, o que
  o Google mais valoriza hoje — e o emtecorp **não tem** (DR 6).
- **Anti-doorway:** é o antídoto ao padrão de risco atual (as LPs
  `empresa-`/`fornecedores-`/`fabrica-` são doorway em escala). Em vez de
  mais páginas-modificador (que o core 2026 pune), cresce conteúdo genuíno.
- **E-E-A-T:** o cluster carrega autor, fontes, entidade — sinais que a
  página comercial sozinha não tem.
- **GEO/AEO:** blocos informacionais extraíveis são o que a IA cita.

## Como se estrutura na GM (princípio → RN → Dimensão)
Reaproveita o [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]]:
- **Dim 1 (Estudo):** o estudo passa a mapear o **cluster** (pilar
  contratado + tópicos de apoio em `/informacoes`), sem alterar o conjunto
  contratado. Marca lacunas de intenção informacional.
- **Dim 3 (Arquitetura/Silo/Linkagem):** audita se o cluster `/informacoes`
  **linka para cima** (para o pilar) — é literalmente o trabalho da Dim 3.
  Também trata a canibalização `www × loja` (NOVO A2).
- **Dim 2 (Conteúdo):** gera o conteúdo do cluster com intenção/entidade/
  extrabilidade (2C/2D/2E do mapa).
- **Governança (RN-100/47):** GM **detecta** a lacuna de cluster; MPI Plus
  **gera** o conteúdo de `/informacoes` após clique do analista; Front-end
  publica. Fluxo atual, sem nova capability comercial.
- **RN-85 (bonificação 50%):** diferenciar o que é bonificação contratada
  (páginas MPI extras) do que é **conteúdo de casa em `/informacoes`** (fora
  do teto de pacote) — precisa de convenção clara para não confundir.

## A bifurcação a decidir (a única de fundo)
- **Só aditivo (recomendado agora):** construir o cluster em `/informacoes`
  sem tocar nas páginas existentes. Zero risco de contrato, puro ganho.
- **Aditivo + consolidação das LPs-doorway:** além do cluster, consolidar as
  páginas-modificador (`empresa-`/`fornecedores-`/…) num pilar só — **maior
  impacto anti-doorway**, mas toca páginas existentes e esbarra na RN-84
  (poda) e possivelmente no que o cliente "vê como entregue". Fase posterior,
  depende do ajuste da RN-84 (já na fila #1).

## Próximo passo
Se validado, isto vira: (a) uma **decisão formal em [[04-Decisões]]** (ADR:
"cluster em /informacoes como camada de ranqueamento fora do contrato"), e
(b) entra na estruturação do PRD v2 como o **modelo de arquitetura** que a
Dim 1 e a Dim 3 passam a auditar. Aguardando validação do PO.

## Notas relacionadas
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] — onde cada frente se pluga (Dim 1/2/3)
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] — doorway/scaled content e o caso emtecorp
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — PRD de estudo do Gregory (exclui /informacoes e /artigos)
- [[02-Fluxos/estudo-de-keywords]] — lógica de cluster/silo que sustenta a estratégia
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — princípios 1 (intenção) e 2 (anti-canibalização)
- [[03-Produtos/growth-machine/prd-v2-mvp]] · [[03-Produtos/growth-machine]] · [[00-Cerebro]]
