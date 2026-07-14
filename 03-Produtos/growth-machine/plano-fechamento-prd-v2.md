---
tipo: produto
status: vivo
criado: 2026-07-08
ultima-revisao: 2026-07-10
tags: [growth-machine, prd, v2, plano, checklist, roadmap, tracker]
---

# Plano de fechamento do PRD v2 — passos + checklist do PRD ajustado

> Tracker único para **fechar todo o PRD**. Separa (1) as **decisões-gate**
> que destravam o trabalho, (2) as **trilhas paralelas** de execução, e (3)
> o **checklist de implementação no PRD ajustado** (o que efetivamente muda
> em [[03-Produtos/growth-machine/prd-v2-mvp]]). Consolida:
> [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] (gaps dos 13
> blocos), [[03-Produtos/growth-machine/reconciliacao-regras-gregory]]
> (conflitos), [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]]
> (RNs/dimensões novas) e
> [[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]] (ADR).

## 1. Decisões-gate — TODAS FECHADAS (2026-07-10)
Sem estas, algumas trilhas ficavam bloqueadas. As 9 foram resolvidas em
sequência com o PO; 2 viraram ADR formal em [[04-Decisões]].

| # | Decisão | Bloqueava | Resolução |
|---|---|---|---|
| **G1** | Pesos do índice: Gregory 40/30/30 × cofre 40/40/20 × ata "lead é principal" | Track A, Bloco 2/5 | ✅ **Mantido 40/40/20, sob revisão** — calibração por dado real (correlação peso×outcome), não por decreto. [[04-Decisões/adr-camada-calibracao-continua]] (corrige a tentativa inicial 35/20/45, superada) |
| **G2** | Convenção de numeração de RN | Track A/C | ✅ Novas = `RN-SGA-01+`; regras do Gregory = `RN-EST-*` |
| **G3** | Concatenação (Gregory) × anti-concatenação/cluster | Track C, Dim 1/3 | ✅ **Cluster em /informacoes** substitui a concatenação em escala |
| **G4** | Fluxo de keywords: Google Suggest × AI-first | Track C, Dim 1 | ✅ Inversão AI-first prevalece (já oficial/Jira) |
| **G5** | Fonte de posicionamento: GSC direto × relatório MPI Plus | Track D, Fase 2 | ✅ Relatório mensal MPI Plus é a fonte única |
| **G6** | **North Star** do produto | Bloco 2 | ✅ "% carteira diagnosticada na cadência, com fila aprovada" |
| **G7** | Faseamento das dimensões no MVP | Bloco 3/9, Track E | ✅ Dim 1+determinísticas+10 no MVP; Dim 2/3/8 fast-follow |
| **G8** | ADR cluster /informacoes: só aditivo × + consolidar doorway | Track C | ✅ **Só aditivo** agora; consolidação depende do ajuste da RN-84 |
| **G9** | Numeração oficial do PRD (v1.0 × v1.9.14 × v2.0-cofre) | Cabeçalho | ✅ Cofre segue com `v2.0-mvp` interno; numeração do Drive fica pendente de confirmação externa |

## 2. Trilhas paralelas (o que roda ao mesmo tempo)

### Track A — Reconciliar o catálogo de RN (fecha a canibalização) · ✅ CONCLUÍDA 2026-07-10
- [x] Aplicar **G1** (pesos 35/20/45) em todas as notas — feito 2026-07-10
- [x] Threshold da Dim 1 fixado em **<50%** (feito 2026-07-08)
- [x] Convenção de numeração decidida (**G2**: RN-SGA-01+ / `RN-EST-*`) — feito 2026-07-10
- [x] Marcar **`[SUPERSEDIDA]`**: RN-21/22/23/29/32 — aplicado no catálogo real
- [x] Remover resíduo **Bright Data** do texto — RN-64/RN-105 limpas
- [x] Adicionar colunas **Origem + Prioridade** ao catálogo — aplicado aos blocos novos (`RN-EST-*`/`RN-SGA-*`); **122 RNs originais ficam para backlog** (exige validação humana por RN, não é seguro inferir em massa)
- [x] Tirar o "como" de RN de implementação (RN-93 Horizon, RN-99 GPT-5) — reescritas
- [x] Adicionar bloco `RN-EST-*` (regras do estudo do Gregory) ao catálogo — 6 RNs
- [x] Adicionar bloco `RN-SGA-*` (proposta SEO/GEO/AEO) ao catálogo — 16 RNs, marcadas "proposta, pendente de reconciliação externa"

### Track B — Completar os 13 blocos do PRD
- [x] Bloco 5 (RF-00 a RF-46) — feito
- [ ] Bloco 2 — fixar **North Star + métricas de apoio** (G6)
- [ ] Bloco 4 — seção de **personas** dedicada (incl. visão própria do CS)
- [ ] Bloco 6 — fechar **gaps NFR** (disponibilidade fora do horário, retenção LGPD)
- [ ] Bloco 8 — **1 User Story + CA por RF** (hoje só 6 críticos)
- [ ] Bloco 9 — **máquinas de estado** (F-21/F-22)
- [ ] Bloco 11 — tornar **premissas dos números** explícitas
- [ ] Bloco 12 — detalhar **rollout** (piloto, critérios de saída de fase)

### Track C — Estruturação SEO/GEO/AEO (o "PRD ajustado") — ver checklist §3
- [x] Formalizar **ADR do cluster /informacoes** (G8) — [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]], feito 2026-07-10
- [ ] Ajustes de RN existente (RN-07, RN-82, RN-84)
- [x] Criar RN-SGA-01 a RN-SGA-16 (16 novas) — no catálogo, status "proposta" até reconciliar com a vault externa
- [ ] Sub-dimensões 2D (AEO), 2E (E-E-A-T); Dimensão 11 (GEO/Citação)
- [ ] Expandir Dim 3/5/7/8

### Track D — Integração & engenharia (bloqueadores de build)
- [x] Resolver as **7 questões** (Q18-21 Salesforce; Q27-30 MPI Plus) —
  **endereçadas pelo PO em 2026-07-13** (6 com resposta concreta, Q18
  adiada para fase 2). Ver [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]].
- [ ] **Dimensionar cotas** (PageSpeed 400/dia, 6 GSC, SemRush)
- [ ] **ERD** + contratos de API (F-23/F-24)
- [ ] Fonte de posicionamento (**G5**)

### Track E — Prompts & qualidade (risco "casa vazia")
- [ ] Desenho fino dos prompts dos agentes
- [ ] **Golden-set** + processo de validação antes de produção
- [ ] `confidence` mínimo por agente + calibração

### Track F — Achados novos da reconciliação com a vault externa (2026-07-10)
- [ ] **Frente Z1 (mais urgente do documento inteiro deles)** — auditar a
  carteira atual com FireCrawl atrás de páginas quase-duplicatas por
  região/tipo. Sem dependência, pode rodar já.
- [ ] **C3** — backtest da curva `posicionamento_esperado` (quick win, sem dependência)
- [ ] **C4** — correlação peso×outcome de negócio (quick win, sem dependência)
- [ ] Emenda à RN-107 — enumerar "demais canais" antes de implementar RN-123/RN-124 → afeta `RF-13`/`RF-24` do PRD
- [ ] Implementar RN-123 (confirmação de entrega WhatsApp) e RN-124 (paridade spam por canal) → afeta `RF-24` do PRD
- [ ] Referência cruzada RN-121 → RN-123/RN-124
- [x] Esclarecer RN-41 "Tintambi" — **resolvido pelo PO (2026-07-13)**: era o centralizador de páginas MPI formadas por imagem + tópico segmentado
- [ ] Segmentar curva de CTR (Local Pack × orgânica clássica), RN-16 → afeta `RF-09` do PRD
- [ ] Baseline defasada do `ctr_estimado` (janela saudável trimestral)
- [ ] Avaliar expansão GSC (6→9-10 contas) ou alocação dinâmica

## 3. Checklist de implementação no PRD ajustado (Track C detalhado)
O que efetivamente entra/muda no PRD por dimensão. Marca de fase: ✅ MVP ·
🕒 Fase 2. Rastreável ao [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]].

**Dim 1 — Estudo**
- [ ] Estudo passa a mapear **cluster** (pilar contratado + apoio /informacoes) — ✅
- [ ] Regra anti-doorway / limite de variação por intenção (RN-SGA-05) — ✅

**Dim 2 — Conteúdo (maior expansão)**
- [ ] Meta description ≤160 / title ≤60 determinístico (RN-SGA-03) — ✅
- [ ] Ajuste **RN-84** (poda: bloqueio → sugestão + scoring) — ✅
- [ ] Sinal "conteúdo preso em PDF → HTML" (RN-SGA-16) — ✅
- [ ] Sub-dim **2D-AEO** (resposta única + priorização por nicho, RN-SGA-02/04) — 🕒
- [ ] Sub-dim **2E-E-E-A-T** (autor/sobre/fontes, RN-SGA-07) — ✅
- [ ] Extrabilidade / answer-first (RN-SGA-01) — 🕒
- [ ] Sinal de conteúdo original / information gain (RN-SGA-08) — 🕒

**Dim 3 — Arquitetura/Silo**
- [ ] Auditar linkagem **cluster → pilar** (/informacoes sobe p/ página vendida) — ✅
- [ ] Canibalização **www × loja** multi-subdomínio (RN-SGA-06) — ✅

**Dim 5 — PageSpeed**
- [ ] **Ajuste RN-07**: régua por **CWV real** (LCP/INP/CLS), não só Score ≥80 — ✅
- [ ] Accessibility tree / CLS (pilar agêntico) — 🕒

**Dim 6 — Schemas**
- [ ] `sameAs` / entidade (RN-SGA-14) — 🕒

**Dim 7 — Robots/Indexação**
- [ ] Incorporar **controle de crawler de IA** do PRD robots do Gregory (RN-SGA-13) — ✅
- [ ] Evoluir **RN-82** (llms.txt: presença → qualidade) — 🕒
- [ ] Crawl-log real (RN-SGA-12) — 🕒

**Dim 8 — Sinais externos**
- [ ] Reativa → propositiva (ofensiva de backlink, RN-SGA-09) — 🕒
- [ ] Presença de entidade / off-site — 🕒
- [ ] Tráfego de origem IA (RN-SGA-11) — 🕒

**Dim 11 — GEO/Citação (NOVA)**
- [ ] Loop de mensuração via Ideal Tracker (RN-SGA-10) — 🕒

**Transversal**
- [ ] Camada editorial humana reforçada (anti-scaled, core 2026) — ✅

## 4. Sequência recomendada (ordem de ataque)
1. **Fechar G1–G9** (decisões-gate) — 1 rodada com o PO.
2. **Track A** (reconciliação) — barato e destrava a base sem canibalizar.
3. **Track B + Track C-MVP (✅)** em paralelo — completam o PRD "pronto p/ dev".
4. **Track D** (integração) — bloqueador técnico, começar cedo.
5. **Track E** (prompts) — em paralelo desde já (é o maior risco).
6. **Track C-Fase 2 (🕒)** — depois do MVP fechado.

## 5. Definição de "PRD fechado" (pronto para dev)
- [x] Todas as decisões-gate G1–G9 registradas
- [x] Catálogo de RN reconciliado (sem canibalização; Origem/Prioridade nos blocos novos, 122 originais em backlog)
- [ ] 13 blocos completos; 1 US+CA por RF
- [x] Estrutura SEO/GEO/AEO-MVP incorporada às dimensões (2D/2E/Dim 11 na nota-mãe)
- [x] 7 questões de integração resolvidas (2026-07-13)
- [ ] Golden-set dos prompts definido
- [ ] ERD + máquinas de estado anexados
- [x] **Reconciliação com a vault externa (v1.9.19 + `10-modelo-proposto-v2`)** — concluída 2026-07-10, ver [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] (Track F lista os achados novos ainda não executados)
- [x] **PRD final estruturado** — [[PRDFINAL]] (2026-07-10): 13 blocos com as reconciliações como texto principal, 8 RFs novas (RF-47 a RF-54) formalizando RN-SGA/RN-EST já ✅ MVP no checklist §3, e checagem dedicada de aderência a boas práticas Google 2026
- [ ] **RFs do PRD atualizadas quando Track F fechar** — Track F não é
  critério de fechamento do PRD em si (é execução/calibração, roda depois),
  mas 3 itens **alteram RN já citadas em RF existentes** e precisam
  atualizar o PRD quando implementados, para não deixar a doc dessincronizada:
  - RN-123/RN-124 (entrega multicanal) → `RF-24` (Dim 10)
  - Emenda RN-107 ("demais canais") → `RF-13` e `RF-24`
  - Segmentação RN-16 (Local Pack × orgânica) → `RF-09`
  Marcadas `[⚠️ pendente]` inline nas RFs em [[PRDFINAL]].
- [ ] **7 questões de integração**, **golden-set dos prompts** e **ERD/máquinas
  de estado** seguem em aberto — [[PRDFINAL]] não declara o produto "pronto
  para codar" enquanto esses 3 itens (linhas acima) não fecharem.

## Notas relacionadas
- [[PRDFINAL]] — **PRD final (2026-07-10)**, já incorpora G1–G9, RN-SGA/RN-EST/RN-123-124 como RF (RF-47 a RF-54) e a checagem de boas práticas Google 2026; segue sendo esta nota o tracker do que falta para ele ser "fechado" de fato
- [[04-Decisões/adr-camada-calibracao-continua]] — ADR vigente da G1
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] — ADR da G3/G8
- [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] — reconciliação completa, Track F
- [[03-Produtos/growth-machine/prd-v2-mvp]] — rascunho de consolidação, histórico (consolidado em PRDFINAL)
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] — gaps dos 13 blocos
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — decisões-gate G1–G5
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] — RNs/dimensões novas (Track C)
- [[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]] — ADR cluster (G8)
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] — origem das oportunidades
- [[00-Painel-Estado]] · [[00-Cerebro]]
