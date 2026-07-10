---
tipo: produto
status: vivo
criado: 2026-07-08
ultima-revisao: 2026-07-10
origem: "Upload do PO — 'Regras Growth Machine — Entregue pelo Gregory' (.docx→PDF), 4 sub-PRDs"
tags: [growth-machine, prd, reconciliacao, gregory, regua, seo, geo, aeo, core-update, canibalizacao]
---

# Ultra-análise — Regras do Gregory × o que temos estruturado

> Cruzamento linha a linha das **regras entregues pelo Gregory** (fonte
> autoritativa da régua de Growth — o kickoff já dizia "Pesos da Régua:
> pegar com o Gregory") contra todo o cofre já estruturado
> ([[03-Produtos/growth-machine]], [[03-Produtos/growth-machine/catalogo-regras-negocio]],
> [[03-Produtos/growth-machine/prd-v2-mvp]]) e contra boas práticas +
> Google core updates. Objetivo: garantir que **as RNs e o PRD não se
> canibalizem** — separar o que o Gregory **confirma**, o que ele **entra
> em conflito**, e o que ele **resolve/avança**.

## O que o Gregory entregou (4 sub-PRDs)
1. **Curva de rampagem + Projeção de leads + Fórmula de percepção** — a
   matemática do Motor de Percepção (Fase 2).
2. **Método de construção do estudo** — Etapa 0 (pré-mapeamento) → 1
   (validação cliente) → 2 (geração de keywords) → 3 (validação de legado).
3. **Schema JSON-LD** — arquitetura de dados estruturados por template.
4. **robots.txt automatizado** — geração por tipo (Produto/Serviço) + IA.

---

## Parte 1 — Convergências que VALIDAM decisões nossas (boas notícias)

| Tema | O que o Gregory diz | O que já tínhamos | Efeito |
|---|---|---|---|
| **Threshold crítico do Estudo** | Score de qualidade: Adequado 80–100 · Ajuste 50–79 · **Crítico <50%** | Acabamos de reconciliar o gate da Dim 1 para **<50%** (F-03) | ✅ **Confirma a decisão de ontem** — a fonte autoritativa fecha o F-03 em <50%, não <60% |
| **CTR por faixa** | 1–3 → 20% · 4–10 → 5% · >10 → 1% | RN-16 (sem arredondamento; 10,5 = 1%) | ✅ Idêntico. Confirma RN-16 |
| **Posicionamento esperado** | `posicionamento_esperado = maturidade_final` | **Q23 estava em aberto** (régua de posicionamento por período) | ✅ **Resolve a Q23** — o esperado é a própria curva de maturidade |
| **`ctr_estimado` — origem** | Definido da posição média do Search Console → faixa | F-08 (Will) apontava "ctr sem origem" | ✅ Resolve a origem do ctr_estimado |
| **Calibração dos números** | Curva, teto, conversão 5%, CTR, thresholds — todos parametrizáveis, com validação (0–1, faixas não sobrepostas, soma=100%, ordem lógica) | Backlog "números sem origem" + Tela 8/RN-18/RN-122 | ✅ Dá **origem autoritativa** aos números e um contrato de validação pronto p/ virar CA |
| **Curva de maturidade + teto** | 0-3:5-15 · 4-6:15-30 · 7-12:30-55 · 13-18:55-75 · 19-24:75-90 · >24:90 / teto 12m 60, 24m 90, 36m 100 | RN-17 idêntico | ✅ Idêntico |
| **Status** | Ruim <0,60 · Regular 0,60-0,79 · Bom 0,80-0,89 · Ótimo ≥0,90 | RN-19 | ✅ Idêntico |
| **Schema anti-spam** | FAQPage, Review/AggregateRating, Offer (preço) → **Fase 2 (futuro)**, fora desta entrega | RN-117 (só marca schema real/verificável) | ✅ **Confirma RN-117** — o Gregory não fabrica review/rating/preço |
| **Controle de crawler de IA** | robots.txt com blocos para **GPTBot, Google-Extended, ClaudeBot, PerplexityBot**, controláveis | GEO Lacuna 2 dizia "não monitoramos acesso de crawler de IA" | ✅ **Avança GEO** — cobre a parte de *permissão* (robots) da prontidão agêntica |

---

## Parte 2 — Conflitos / canibalização (decisão do PO antes de propagar)

> Estes são os pontos onde a régua do Gregory **diverge** do que está
> escrito no cofre/PRD. Não vou propagar nada sem sua decisão — é
> exatamente o risco de canibalização que você pediu para evitar.

### ✅ C1 — RESOLVIDO (2026-07-10): Pesos do Índice fixados em 35/20/45
- **Gregory:** `indice_final = (pos × 0,4) + (traf × 0,3) + (leads × 0,3)`.
- **Cofre (era):** 40 pos / 40 traf / 20 leads.
- **Decisão final:** nem 40/40/20 nem 40/30/30 refletiam o consenso 2026 de
  que tráfego é o sinal mais erodido por zero-click/AI Overview (60% das
  buscas sem clique). Fixado em **35 posicionamento / 20 tráfego / 45
  leads** — reduz tráfego além do que o Gregory propôs, eleva leads ainda
  mais. Ver ADR completo: [[04-Decisões/adr-pesos-indice-performance-2026]].
  Propagado em RN-18, growth-machine.md, cheat-sheet, prep-reuniao,
  prd-v2-mvp (RF-11).

### 🔴 C2 — Colisão de numeração de RN (Gregory usa RN01–RN06 locais)
- O sub-PRD do estudo traz **RN01–RN06 próprios** (ex.: "RN02: palavra
  épica ≤3 termos"; "RN06: páginas MPI ignoradas no crawling").
- Isso **colide** com o catálogo mestre RN-01…RN-122 (onde RN-02 = cadência,
  RN-06 = rejeição de briefing).
- **Risco:** dev implementa a RN errada. **Recomendação:** namespacar — as
  regras do estudo do Gregory viram, no cofre, um bloco próprio (ex.
  `RN-EST-01…`) ou são mapeadas para RNs já existentes, **sem reusar
  números do catálogo mestre**. Decisão de convenção sua.

### ✅ C3 — RESOLVIDO (2026-07-10): cluster substitui a concatenação em escala
- **Gregory (4.3.7/4.3.8):** concatenar 3 palavras × 2 regiões e palavra ×
  tipo (com "ajuste semântico via IA para naturalidade").
- **Cofre:** [[03-Produtos/mpi-plus/historia-prompt-endurecimento-anti-concatenacao-geo]]
  — história **oficial**, motivada por QA de produção real, que
  **endurece contra** concatenação mecânica / GEO genérico.
- **Decisão final:** a concatenação em escala não é adotada como estratégia
  primária — é exatamente o padrão de "scaled content abuse" punido pelos
  core updates 2026. No lugar, adota-se o **cluster via /informacoes e
  /artigos** (aditivo, sem tocar as páginas MPI contratadas) como caminho
  de ranqueamento. Ver
  [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] e o caso real
  em [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]].

### ✅ C4 — RESOLVIDO (2026-07-10): inversão AI-first prevalece
- **Gregory:** KeywordTool + **SEMrush** + **Google Suggest** como descoberta.
- **Decisão final:** prevalece
  [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] (já
  oficial, enviada ao Jira) — geração via IA primeiro; as ferramentas do
  Gregory (SEMrush/KeywordTool/Suggest) passam a **enriquecer** (volume,
  CPC, concorrência), não a descobrir.

### ✅ C5 — RESOLVIDO (2026-07-10): relatório mensal MPI Plus é a fonte única
- **Gregory (2.2):** processa **Search Console** direto (posição média das
  palavras base).
- **Decisão final:** mantém RN-105/RN-106/RN-64 como fonte primária — o
  **relatório mensal do MPI Plus** segue como fonte única de posicionamento
  (Hard Stop se ausente). Leitura adotada: o relatório mensal já é
  construído a partir do GSC internamente; o processamento descrito pelo
  Gregory (2.2) descreve como esse relatório é montado, não uma integração
  paralela do GM ao Search Console. Toca as Q27–Q30 — mantidas em aberto
  para confirmação técnica de como o relatório é gerado.

### 🟡 C6 — Palavra épica e crawl do estudo
- **Épica:** Gregory = "maior volume da categoria, ≤3 palavras"; nosso v3 =
  "maior volume entre **comercial/transacional**, fallback volume geral"
  ([[02-Fluxos/prompt-avaliacao-keywords]]). Nosso critério é mais refinado.
- **Crawl:** Gregory exclui `/informacoes` e `/artigos` no crawl do estudo;
  RN-69 diz "varre **todas** as páginas". Contextos diferentes (estudo ×
  briefing), mas vale explicitar para não conflitar.

---

## Parte 3 — Cruzamento com boas práticas + Google core updates

| Frente | Regra do Gregory | Leitura vs. boas práticas / core update |
|---|---|---|
| **Scaled content abuse** (política de spam de conteúdo em escala, core/spam updates recentes) | Concatenação palavra×região×tipo em escala (C3) | ⚠️ **Maior risco**: páginas geradas por concatenação mecânica entre ~2.500 clientes é exatamente o padrão que a política de "scaled content abuse" mira. O "ajuste semântico via IA" ajuda, mas é a mesma dor que nossa QA anti-concatenação já registrou. Não é bloqueador, é ponto de calibração fina |
| **Helpful Content (absorvido no core ranking)** | Estudo por intenção, filtro de navegacional, exclusão de termos irrelevantes | ✅ Alinhado — prioriza intenção comercial/transacional/informacional |
| **GEO / AI Overview** | robots.txt controla GPTBot/ClaudeBot/PerplexityBot/Google-Extended; schema por template | ✅ Avança a **prontidão agêntica** (permissão de crawler de IA) e a extração por schema. **Mas** o índice do Gregory é **100% SEO tradicional** (pos/tráf/leads) — **zero peso de GEO**, exatamente como diagnosticamos. Reforça a decisão F-28: **medição de GEO = Fase 2** |
| **Crawl budget** (SEO Lacuna 2) | robots bloqueia utm_/filter/sort/paginação; libera CSS/JS; sitemap | ✅ Avança o lado **declarado** do crawl budget (o que nossa Dim 7 já cobria) — ainda **não** é análise de log real, que continua sendo a lacuna |
| **Renderização** | Permitir `/*.css$` e `/*.js$` no robots | ✅ Boa prática — Google precisa renderizar; evita bloqueio acidental |
| **Dados estruturados como "API" para IA** | Base Organization+LocalBusiness em todas; entidade principal por template; Rich Results Test como CA | ✅ Forte alinhamento com a tendência de schema como fonte confiável de extração por IA |
| **E-E-A-T / YMYL** | Não tocado diretamente | Neutro — segue coberto pelos prompts de conteúdo do MPI Plus |

---

## Parte 4 — Impacto no nosso PRD v2 e no catálogo (proposto, não aplicado)
Se as decisões da Parte 2 forem confirmadas:
1. **Propagar 40/30/30** (C1) em RN-18, growth-machine.md, cheat-sheet,
   prep-reuniao, prd-v2-mvp (RF-11), principios-nucleo — mesma operação
   limpa que fizemos no <50%.
2. **Namespacar as regras do estudo do Gregory** (C2) como bloco próprio no
   catálogo, sem colidir com RN-01…122.
3. **Registrar como resolvidas**: Q23 (posicionamento esperado = maturidade),
   origem do ctr_estimado, origem/validação dos parâmetros (Tela 8).
4. **Incorporar ao PRD v2** os 4 sub-PRDs como fontes das dimensões: Fase 2
   (percepção), Dim 1 (estudo), Dim 6 (schema), Dim 7 (robots + IA crawler).
5. **Adicionar CAs** vindos direto do Gregory: validação de parâmetros
   (0–1, soma=100%, ordem lógica); JSON-LD válido no Rich Results Test;
   robots gerado correto por tipo Produto/Serviço.
6. **Abrir alinhamento** Gregory × QA anti-concatenação (C3) e × inversão de
   fluxo de keywords (C4).

---

## Parte 5 — Decisões (todas fechadas em 2026-07-10)
1. **C1 — Pesos: 35/20/45.** ✅ [[04-Decisões/adr-pesos-indice-performance-2026]]
2. **C2 — Numeração:** RNs novas seguem `RN-123+`; regras do Gregory viram
   `RN-EST-*`, sem colidir com o catálogo mestre. ✅
3. **C3 — Concatenação → cluster:** substituída pelo cluster aditivo via
   /informacoes. ✅ [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]
4. **C4 — Fluxo de keywords:** inversão AI-first prevalece. ✅
5. **C5 — Fonte de posicionamento:** relatório mensal MPI Plus é a fonte
   única. ✅

Tracker de execução destas decisões: [[03-Produtos/growth-machine/plano-fechamento-prd-v2]].

## Notas relacionadas
- [[04-Decisões/adr-pesos-indice-performance-2026]] — ADR da decisão C1
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] — ADR da decisão C3
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — tracker de execução
- [[03-Produtos/growth-machine/prd-v2-mvp]] — PRD que incorpora estas fontes
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — catálogo mestre de RN (alvo da reconciliação)
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] — auditoria de qualidade de RN
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] — frentes SEO/GEO/AEO
- [[03-Produtos/mpi-plus/historia-prompt-endurecimento-anti-concatenacao-geo]] — QA anti-concatenação (C3)
- [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] — inversão do fluxo (C4)
- [[02-Fluxos/prompt-avaliacao-keywords]] — prompt v3 (palavra épica, C6)
- [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
