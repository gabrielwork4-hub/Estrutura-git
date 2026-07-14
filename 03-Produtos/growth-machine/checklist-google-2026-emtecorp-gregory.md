---
tipo: produto
status: vivo
criado: 2026-07-08
ultima-revisao: 2026-07-08
tags: [growth-machine, checklist, seo, geo, aeo, google-2026, core-update, emtecorp, gregory, benchmark]
---

# Checklist — Boas práticas Google 2026 × emtecorp (real) × regras Gregory × Growth Machine

> Cruzamento de 4 fontes para **visualizar os pontos que a GM ainda repete**
> e onde há oportunidade de sanar. Fontes: (1) estrutura real do
> **emtecorp.com.br** (dados Ahrefs, 2026-07-08 — ver
> [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] e a análise de
> maturidade [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]);
> (2) os **4 sub-PRDs do Gregory** (percepção, estudo, schema, robots);
> (3) o **Growth Machine** (122 RNs, 10 dimensões); (4) **boas práticas
> Google 2026**.

## Contexto Google 2026 (o que mudou e por que pesa)
- **Core updates de março e maio/2026:** miram diretamente *scaled content
  abuse* — sites com centenas/milhares de páginas em massa sem edição
  humana caíram **50–80%**. Não é sobre "ser IA", é sobre **valor real +
  camada editorial humana**.
- **AI Overview:** CTR da posição 1 caiu de **~27% → ~11%** onde há AI
  Overview; marca citada ganha **+35% de cliques**. → medir GEO deixou de
  ser "futuro" e virou receita.
- **Reforço de E-E-A-T:** autor transparente, fonte crível, marca forte,
  insight original passam a decidir core updates.

## Dados reais do emtecorp que ancoram a checklist
DR **6** · **171 keywords / 73 no Top 3** · ~**413 visitas/mês** · quase
**0 backlinks** por página · padrão de **LPs por modificador**
(`empresa-`/`fornecedores-`/`fabrica-`/`revenda-` sobre o mesmo produto) ·
**www × loja** (dois domínios competindo) · **catálogos em PDF rankeando**
como ativos primários.

Legenda: ✅ coberto · ⚠️ parcial / risco · 🔴 ausente · ❓ não verificável (WAF)

---

## Bloco A — SEO

| # | Boa prática Google 2026 | emtecorp (real) | Regra Gregory | Cobertura GM | Oportunidade de sanar |
|---|---|---|---|---|---|
| A1 | Intenção de busca correta (1 intenção/página) | ✅ 73/171 Top 3 | ✅ classificação por intenção | ✅ Dim 1/2, RN-113 | — (ponto forte) |
| A2 | **Não-canibalização** entre páginas/domínios | ⚠️ www × loja disputam ("microesfera de vidro" nos dois) | ⚠️ concatenação gera variações | 🟡 RN-15/85 só no **estudo**, não entre subdomínios | 🔴 **NOVO** — GM não audita canibalização www × loja |
| A3 | **Anti-doorway / scaled content** (core 2026) | 🔴 LPs por modificador em escala | 🔴 **prescreve** concatenação (palavra×tipo×região) | 🔴 sem check anti-doorway | 🔴 **RECORRENTE #1** — C3; core update 2026 pune isto |
| A4 | Poda/consolidação de conteúdo fraco | ⚠️ PDFs/páginas finas rankeando | 🟡 plano de ação prevê "remoção de termos" | 🔴 **RN-84 proíbe** sugerir remoção | 🔴 **RECORRENTE** (ajuste RN-84, já na fila #1) |
| A5 | **Autoridade / backlinks** (fator forte) | 🔴 DR 6, ~0 refdomains | ❌ não trata | 🔴 Dim 8 só disavow (defensivo) | 🔴 **RECORRENTE** — sem ofensiva de autoridade (SEO Lacuna 3) |
| A6 | Conteúdo útil / **insight original** (Helpful/core 2026) | 🟡 blog bom, LP template | 🟡 padrão SERP (risco de clonar concorrente) | 🟡 Dim 2 mede cobertura, não ineditismo | 🔴 **RECORRENTE** — sinal de conteúdo original ([[05-Backlog/gm-sinal-conteudo-original]]) |
| A7 | **E-E-A-T on-page** (autor, sobre, confiança) | ❓ sem autor visível aparente | ❌ não trata | 🟡 princípio nos prompts, sem checagem | 🔴 **NOVO** — auditar sinais E-E-A-T (autor/fontes/sobre) |
| A8 | Schema por template | ❓ | ✅ PRD schema completo | ✅ Dim 6, RN-117 | — (regras fortes) |
| A9 | robots + crawl budget + CSS/JS liberado | ❓ | ✅ PRD robots (bloqueia params, libera CSS/JS) | 🟡 Dim 7 checa robots, **não** crawl budget real | ⚠️ incorporar regras do Gregory à Dim 7 |
| A10 | **Core Web Vitals reais** (LCP/INP/CLS) | ❓ | ❌ não trata | ⚠️ Dim 5 usa **PageSpeed Score ≥80**, não CWV | 🔴 **RECORRENTE** — RN-07 (proxy ≠ métrica real) |
| A11 | Log de crawler real (indexação de fato) | ❓ | ❌ | 🔴 só sitemap declarado | 🔴 **RECORRENTE** — SEO Lacuna 2 |
| A12 | Conteúdo importante **em HTML, não PDF** | 🔴 catálogos PDF entre top pages | ❌ | 🔴 sem sinal | 🔴 **NOVO** — flag "ativo preso em PDF → migrar p/ HTML" |
| A13 | Canonical / parâmetros / duplicados | ❓ | ✅ robots bloqueia utm/filter/sort | 🟡 Dim 7 canonical | ⚠️ estratégia canonical www × loja |

## Bloco B — GEO (Generative Engine Optimization)

| # | Boa prática Google 2026 | emtecorp | Regra Gregory | Cobertura GM | Oportunidade de sanar |
|---|---|---|---|---|---|
| B1 | Conteúdo **extraível / answer-first** (bloco autocontido) | ❓ | ❌ | 🔴 pensa página, não bloco | 🔴 **RECORRENTE** — GEO Lacuna 1 (fila #4) |
| B2 | Controle de crawler de IA (GPTBot/ClaudeBot/Perplexity/Google-Extended) | ❓ | ✅ **PRD robots cobre** | 🟡 RN-82 só presença de llms.txt | ⚠️ **incorporar o robots-IA do Gregory** à GM (avanço barato) |
| B3 | Qualidade do llms.txt / AI Instructions (não só existir) | ❓ | 🟡 só presença | 🟡 RN-82 só sim/não | 🔴 **RECORRENTE** ([[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]]) |
| B4 | **Medir citação em LLM / SoV** (AI Overview vale receita) | 🔴 não medido | ❌ | 🔴 métrica isolada no Ideal Tracker | 🔴 **RECORRENTE** — F-28 (Fase 2); core 2026 aumenta a urgência |
| B5 | Autoridade de **entidade** (Knowledge Graph, sameAs, Wikidata) | 🔴 | 🟡 Organization schema (base, sem sameAs/entity) | 🔴 | 🔴 **RECORRENTE** ([[05-Backlog/gm-checagem-presenca-entidade]]) |
| B6 | Presença **off-site** (Reddit/fóruns/reviews) | ❓ | ❌ | 🔴 só audita o site | 🔴 **RECORRENTE** — GEO Lacuna 3 |
| B7 | Tráfego de **origem IA** segmentado (GA4) | ❓ | ❌ | 🔴 GA4 só orgânico | 🔴 **RECORRENTE** ([[05-Backlog/gm-segmentar-trafego-origem-ia]]) |
| B8 | Pilares agênticos (accessibility tree, CLS, WebMCP) | ❓ | ⚠️ CLS via robots? não | 🔴 5 de 6 ausentes | 🔴 **RECORRENTE** ([[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]) |

## Bloco C — AEO (Answer Engine Optimization)

| # | Boa prática Google 2026 | emtecorp | Regra Gregory | Cobertura GM | Oportunidade de sanar |
|---|---|---|---|---|---|
| C1 | **Resposta única, inequívoca** (1 frase por pergunta) | ❓ | ❌ | 🔴 | 🔴 **RECORRENTE** — AEO Lacuna 1 |
| C2 | FAQ **real** marcada (não fabricada) | ❓ | 🟡 FAQPage = Fase 2 (não fabrica) | 🟡 RN-117 anti-spam | ⚠️ gerar FAQ **real** + schema (oportunidade positiva) |
| C3 | Meta description ≤160 / title ≤60 (snippet) | ❓ | ❌ | 🟡 não determinístico | ⚠️ checagem determinística (fila #3) |
| C4 | Priorização de AEO **por nicho** | 🔴 régua única p/ todos | ❌ | 🔴 | 🔴 **RECORRENTE** — fila #2 (barato: reusa nicho do briefing) |
| C5 | Medir "sou a resposta escolhida" | 🔴 | ❌ | 🔴 | 🔴 **RECORRENTE** — AEO Lacuna 2 (especulativo) |

---

## Os padrões que a GM ainda REPETE (oportunidades de sanar), priorizados

> Consolidação do que aparece marcado 🔴 **RECORRENTE** acima — separado em
> "já mapeado" (tem backlog/decisão) e "NOVO" (o caso real do emtecorp
> revelou e ainda não existe no cofre).

### 🔴 Alta — reforçadas pelo core update 2026 e visíveis no emtecorp
1. **Anti-doorway / scaled content (A3)** — as LPs por modificador do
   emtecorp são o padrão que março/maio-2026 pune com −50/−80%. A GM não tem
   check anti-doorway e o Gregory ainda *prescreve* concatenação (C3).
   *Sanar:* regra de "camada editorial + limite de variação por intenção".
2. **Autoridade / backlinks (A5)** — DR 6 do emtecorp prova o custo. GM só
   faz disavow. *Sanar:* Dim 8 passa de reativa a propositiva (prospecção).
3. **Medição de GEO / citação em LLM (B4)** — AI Overview derruba clique
   orgânico; sem medir, não há loop. *Sanar:* plugar Ideal Tracker (direção
   já confirmada). Core 2026 muda o custo/benefício de esperar a Fase 2.
4. **Poda de conteúdo / RN-84 (A4)** — emtecorp tem PDFs/páginas finas
   rankeando; RN-84 impede sugerir remoção. *Sanar:* ajuste já na fila #1.

### 🟡 Média — recorrentes já mapeadas
5. CWV real vs. PageSpeed Score (A10 / RN-07).
6. Crawl budget / log real (A11 / SEO Lacuna 2).
7. Extrabilidade answer-first (B1 / AEO C1 — mesma frente).
8. Entidade (B5), off-site (B6), tráfego IA (B7), pilares agênticos (B8).
9. Qualidade do llms.txt (B3), FAQ real (C2), meta/title determinístico
   (C3), priorização AEO por nicho (C4), conteúdo original (A6).

### 🆕 NOVO — o caso emtecorp revelou, ainda sem item no cofre
10. **Canibalização entre subdomínios www × loja (A2)** — RN-15/85 só olham
    o estudo, não a arquitetura multi-domínio.
11. **Conteúdo preso em PDF (A12)** — catálogos rankeando como PDF; falta
    sinal "migrar ativo importante de PDF para HTML".
12. **Sinais E-E-A-T on-page (A7)** — autor/sobre/fontes não são checados
    por dimensão nenhuma; core 2026 os torna decisivos.
13. **Incorporar o robots-IA do Gregory (B2)** — avanço barato de GEO que já
    existe na entrega do Gregory e a GM ainda não absorveu.

## Próximo passo sugerido
Transformar os itens **10–13 (NOVO)** em itens de [[05-Backlog]] e elevar
**1–3** na fila de prioridade à luz do core update 2026 — antes de fechar
o escopo SEO/GEO/AEO do PRD v2. Aguardando seu ok para abrir esses backlogs.

## Notas relacionadas
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] — scores e lacunas por pilar
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — regras do Gregory + dados Ahrefs do emtecorp
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] — RNs contra boas práticas do Google
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — fila única de oportunidades
- [[01-Ideias/anti-praticas-seo-growth-excellence]] — anti-práticas de referência
- [[03-Produtos/growth-machine/prd-v2-mvp]] · [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
