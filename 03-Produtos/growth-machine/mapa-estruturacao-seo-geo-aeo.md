---
tipo: produto
status: vivo
criado: 2026-07-08
ultima-revisao: 2026-07-10
tags: [growth-machine, estruturacao, seo, geo, aeo, principios, rn, dimensoes, roadmap]
---

# Mapa de estruturação SEO/GEO/AEO — Princípio → RN → Dimensão → Ação

> Traduz as oportunidades da
> [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] numa
> estrutura acionável: cada oportunidade é ligada ao **princípio-núcleo**
> que serve ([[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]),
> à **RN** e à **Dimensão** que já a contemplam (ou à lacuna), e à **ação de
> estruturação** (ajustar RN existente · criar RN nova · nova sub-dimensão).
> É a base para inserir as 3 frentes no PRD v2 sem canibalizar o que já
> existe. RNs no [[03-Produtos/growth-machine/catalogo-regras-negocio]].

Legenda de estado: 🟢 tem RN **e** Dim (só ajustar) · 🟡 tem Dim, **falta
RN** · 🔴 **sem RN e sem Dim** (capability nova). RNs novas propostas
seguem a sequência do catálogo mestre (**RN-SGA-01+**), para não colidir com a
numeração local do Gregory (ver C2 em
[[03-Produtos/growth-machine/reconciliacao-regras-gregory]]).

---

## Princípio 1 — Intenção real > palavra isolada
| Oportunidade | RN atual | Dim atual | Estado | Ação de estruturação | Fase |
|---|---|---|---|---|---|
| Extrabilidade / answer-first (bloco autocontido) | — | Dim 2 (2C) | 🟡 | Criar **RN-SGA-01** (extrabilidade) + subcheck em 2C | Fase 2 |
| Resposta única/inequívoca (AEO) | — | Dim 2 (2C) | 🔴 | Nova sub-dimensão **2D–AEO** + RN-SGA-02 | Fase 2 |
| Meta description ≤160 / title ≤60 | — | Dim 2 | 🟡 | Checagem **determinística** em Dim 2 + RN-SGA-03 | MVP (barato) |
| Priorização de AEO por nicho | — (usa briefing) | Dim 2/2D | 🔴 | Regra de priorização por nicho (reusa briefing) + RN-SGA-04 | MVP (barato) |

## Princípio 2 — Anti-canibalização como regra estrutural
| Oportunidade | RN atual | Dim atual | Estado | Ação | Fase |
|---|---|---|---|---|---|
| **Anti-doorway / scaled content** (core 2026) | RN-14, RN-15, RN-85 (só no estudo) | Dim 1 + Dim 3 | 🟡 | Nova **RN-SGA-05**: limite de variação por intenção + camada editorial + **Portão de Diferenciação Real** (validado externamente: dado local, prova social, resposta a pergunta real; sem sinal → cluster em vez de página isolada; métrica `taxa_diferenciacao_real`) | MVP (risco alto — Frente Z1 da vault externa é o item mais urgente: auditar carteira já) |
| Canibalização **www × loja** (subdomínios) | RN-15/85 (só estudo) | Dim 3 | 🟡→🔴 | Estender **Dim 3** para arquitetura multi-subdomínio + RN-SGA-06 | MVP |
| Poda / consolidação de conteúdo fraco | **RN-84 revisada** (2026-07-13) | Dim 2 | 🟢 | Formalizada como **RF-55** — scoring objetivo + consolidar/melhorar/remover | MVP (fila #2) |

## Princípio 3 — E-E-A-T como filtro de qualidade
| Oportunidade | RN atual | Dim atual | Estado | Ação | Fase |
|---|---|---|---|---|---|
| Sinais **E-E-A-T on-page** (autor/sobre/fontes) | — | Dim 2 | 🔴 | Nova subcheck **2E** (E-E-A-T) + RN-SGA-07 | MVP (core 2026) |
| Conteúdo **original / information gain** | RN-14 (padrão SERP = risco) | Dim 2 | 🟡 | Sinal de ineditismo em Dim 2 + RN-SGA-08 ([[05-Backlog/gm-sinal-conteudo-original]]) | Fase 2 |
| Autoridade / **ofensiva de backlink** | — (Dim 8 só disavow) | Dim 8 | 🟡 | Estender **Dim 8** reativa→propositiva + RN-SGA-09 | Fase 2 |

## Princípio 4 — Governança humana em toda ação automatizada
| Oportunidade | RN atual | Dim atual | Estado | Ação | Fase |
|---|---|---|---|---|---|
| **Camada editorial reforçada** p/ conteúdo em escala (resposta ao core 2026) | RN-47, RN-89, RN-100 | Transversal | 🟢 | Fortalecer o gate: nenhuma página em escala publica sem revisão editorial humana (liga ao anti-doorway) | MVP |

## Princípio 5 — Medir → ajustar → remedir (loop fechado)
| Oportunidade | RN atual | Dim atual | Estado | Ação | Fase |
|---|---|---|---|---|---|
| **Medição de citação em LLM / SoV** (AI Overview) | — | 2C (isolada no Ideal Tracker) | 🔴 | **Nova Dimensão 11 — GEO/Citação** alimentada pelo Ideal Tracker + RN-SGA-10 ([[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]) | Fase 2 |
| **CWV real** (LCP/INP/CLS) vs. PageSpeed Score | **RN-07** | Dim 5 | 🟢 | **Ajustar RN-07**: régua passa a exigir os 3 CWV reais, não só Score ≥80 | MVP |
| Tráfego de **origem IA** (GA4 segmentado) | — | Motor / Dim 8 | 🟡 | Segmentar origem IA no Motor de Percepção + RN-SGA-11 ([[05-Backlog/gm-segmentar-trafego-origem-ia]]) | Fase 2 |
| Crawl **log real** (indexação de fato) | — | Dim 7/9 | 🔴 | Nova subcheck de log de servidor em Dim 7 + RN-SGA-12 | Fase 2 |
| Medir "sou a resposta escolhida" (AEO) | — | — | 🔴 | Capability nova (Dim 2D/11), especulativa | Pós-Fase 2 |

## Princípio 6 — Alinhamento com sistemas do Google nomeados
| Oportunidade | RN atual | Dim atual | Estado | Ação | Fase |
|---|---|---|---|---|---|
| **Controle de crawler de IA** (GPTBot/ClaudeBot/Perplexity/Google-Extended) | RN-82 (só llms.txt) | Dim 7 + Sentinela | 🟡 | **Incorporar o PRD robots do Gregory** à Dim 7/Sentinela + RN-SGA-13. **Refinamento validado externamente:** não tratar bloqueio de bots de IA como binário — distinguir "bloqueio de treino" (sem custo de GEO) de "bloqueio de citação ao vivo" (custo real, principalmente Perplexity); matriz treino×citação revisada trimestralmente | MVP (barato, já existe no Gregory) |
| Qualidade do **llms.txt / AI Instructions** | **RN-82** (só presença) | Dim 7 | 🟢 | **Evoluir RN-82**: presença → qualidade/eficácia ([[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]]) | Fase 2 |
| Autoridade de **entidade** (sameAs/Knowledge Graph) | RN-117 (schema base) | Dim 6 + Dim 8 | 🟡 | `sameAs` no schema (Dim 6) + presença de entidade (Dim 8) + RN-SGA-14 ([[05-Backlog/gm-checagem-presenca-entidade]]) | Fase 2 |
| Presença **off-site** (Reddit/fóruns/reviews) | — | — | 🔴 | Capability nova (Dim 8 estendida ou Dim 12) | Fase 2/3 |
| **Pilares agênticos** (accessibility tree, CLS, WebMCP) | RN-82 (1 de 6) | Dim 5 + Dim 7 | 🔴 | CLS/accessibility em Dim 5; WebMCP nova checagem + RN-SGA-15 ([[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]) | Fase 2 |
| Conteúdo importante **preso em PDF** | — | Dim 2/7 | 🔴 | Sinal "migrar ativo de PDF→HTML" + RN-SGA-16 | MVP (barato) |
| Schema por template | RN-117 | Dim 6 | 🟢 | Já coberto (PRD schema do Gregory) | MVP |

---

## Estrutura-alvo consolidada (para onde cada Dimensão evolui)
Resumo de como as 10 dimensões absorvem as frentes — o desenho que vai para
a "estruturação e divisão" do PRD v2:

| Dimensão | O que ganha | Frentes |
|---|---|---|
| **Dim 2 — Conteúdo** (maior expansão) | 2C extrabilidade · **2D–AEO** (resposta única, nicho) · **2E–E-E-A-T** (autor/fontes) · meta/title determinístico · scoring de poda · conteúdo original · PDF→HTML | SEO + GEO + AEO |
| **Dim 3 — Arquitetura** | Anti-doorway/scaled + canibalização multi-subdomínio (www × loja) | SEO |
| **Dim 5 — PageSpeed** | RN-07 → **CWV real**; + accessibility tree / CLS (agêntico) | SEO + GEO |
| **Dim 6 — Schemas** | `sameAs` / entidade | GEO |
| **Dim 7 — Robots/Indexação** | Controle de crawler de IA (Gregory) · llms.txt qualidade · crawl-log real | SEO + GEO |
| **Dim 8 — Sinais externos** | Reativa→propositiva (ofensiva de backlink) · presença de entidade / off-site · tráfego origem IA | SEO + GEO |
| **Dim 11 — GEO/Citação (NOVA)** | Loop de mensuração via Ideal Tracker (SoV em LLM) | GEO |
| **Governança (transversal)** | Camada editorial humana reforçada p/ conteúdo em escala | Todos |

**Contagem de estruturação:** ~3 ajustes de RN existente (RN-07, RN-82,
RN-84) · ~16 RNs novas propostas (RN-SGA-01 a RN-SGA-16) · 2 sub-dimensões novas
em Dim 2 (2D–AEO, 2E–E-E-A-T) · 1 dimensão nova (Dim 11 GEO/Citação) ·
expansão de escopo em Dim 3, 5, 7, 8.

## Priorização (à luz do core update 2026)
- **MVP / agora:** ajuste RN-84 (poda), RN-07 (CWV real), anti-doorway
  (RN-SGA-05) + camada editorial, controle de crawler de IA (RN-SGA-13, barato),
  meta/title (RN-SGA-03), priorização AEO por nicho (RN-SGA-04), PDF→HTML (RN-SGA-16).
- **Fase 2:** Dim 11 (medição GEO), extrabilidade/AEO (RN-SGA-01/RN-SGA-02),
  entidade (RN-SGA-14), pilares agênticos (RN-SGA-15), ofensiva de backlink
  (RN-SGA-09), crawl-log (RN-SGA-12), tráfego IA (RN-SGA-11), off-site.

## Próximo passo
Com este mapa, dá para (a) abrir os itens **NOVO** (RN-SGA-05/06/07/13/16)
em [[05-Backlog]] e (b) usar a "Estrutura-alvo" acima como a **divisão das
dimensões** ao inserir SEO/GEO/AEO no PRD v2. Aguardando seu ok para abrir
os backlogs novos e/ou começar a redividir as dimensões no PRD.

## Notas relacionadas
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] — origem das oportunidades
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — os 6 princípios
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — RNs atuais (alvo dos ajustes/novas)
- [[03-Produtos/growth-machine/prd-v2-mvp]] — PRD onde a estrutura-alvo será dividida
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] · [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
- [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
