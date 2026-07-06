---
tipo: produto
status: vivo
criado: 2026-07-06
ultima-revisao: 2026-07-06
tags: [growth-machine, seo, geo, aeo, roadmap, rn, versao-final]
---

# Versão final — Diagnóstico x Recomendação de Desenvolvimento (SEO/GEO/AEO)

> Documento de fechamento da fase de diagnóstico. Consolida em formato
> único (hoje x oportunidades, por frente) tudo o que foi construído em
> [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] e
> [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]], e adiciona
> a seção de RNs que hoje vão contra boas práticas reconhecidas do Google
> — para servir de base de validação final antes de virar backlog formal.
> Estrutura: **diagnóstico** (o que já existe) x **recomendação de
> desenvolvimento** (oportunidades identificadas).

## SEO tradicional (score atual: 75-80%)

| O que temos hoje | Oportunidades |
|---|---|
| Auditoria técnica em 10 dimensões (conteúdo, arquitetura, performance, schemas, indexabilidade, sinais externos, infra, leads) | Ajuste de RN-84: poda de conteúdo como sugestão ao analista (scoring de candidata: baixo tráfego + baixa relevância + sem backlink) — 2-3 sprints |
| Anti-canibalização + arquitetura em silo semântico (RN-15, RN-85) | Log de crawler real — confirmar via log de servidor que o Googlebot rastreia o que o site declara — 1-2 trimestres |
| E-E-A-T como princípio explícito nos prompts de conteúdo | Ofensiva de autoridade/backlink — Dimensão 8 passa de reativa (só disavow) para propositiva (prospecção de domínios/menções) — 2-3 trimestres |
| Governança rastreável (RN-47 aprovação humana, RN-81 validação IA pós-execução, RN-122 versionamento) | — |
| Dados estruturados com regra anti-spam (RN-117, Dimensão 6) | — |

## GEO (score atual: 20-25%)

| O que temos hoje | Oportunidades |
|---|---|
| Dimensão 2C estrutura conteúdo para mecanismos generativos (FAQ, headings, resumo, entidades) | Integração Ideal Tracker → aba GEO do projeto — direção já confirmada pelo PO (ver [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]) |
| Cluster GEO local no prompt de keywords (variação geográfica real, não sprawl genérico) | Accessibility tree + Cumulative Layout Shift — reaproveita Core Web Vitals já existente (Dimensão 5), 2 de 6 pilares agênticos |
| Verificação de presença de AI Instructions/llms.txt (RN-82) | WebMCP (form coverage, tools registered, schemas válidos) — capability nova, depende do site do cliente implementar o protocolo (ver [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]) |
| Métrica de citação em LLM já existe, isolada no Ideal Tracker | Confirmação real de crawler de IA (GPTBot, ClaudeBot, PerplexityBot) via log de servidor |
| — | Auditoria de presença off-site (Reddit, fóruns, reviews) — mudança de escopo mais estrutural, 2-3 trimestres |

## AEO (não medido formalmente ainda)

| O que temos hoje | Oportunidades |
|---|---|
| Segmentação de nicho já coletada no briefing (Fase 1) | Priorização formal de AEO por nicho (local/prático vs. B2B complexo) — 1 sprint, reaproveita dado já coletado |
| Base de conteúdo da Dimensão 2C reaproveitável | Extrabilidade/resposta única — cada bloco responde sozinho, sem ambiguidade — combinável com a mesma frente de GEO, 1 trimestre |
| Regra de meta description ≤160 / title ≤60 já validada (Growth Excellence) | Checagem determinística da regra de meta/title dentro da Dimensão 2C |
| — | Medir "sou a resposta escolhida" em assistente de voz — especulativo, 3+ trimestres, sem viabilidade técnica confirmada — **não priorizar agora** |

---

## RNs que hoje vão contra boas práticas reconhecidas do Google

> Varredura crítica das 122 RNs do catálogo (ver
> [[03-Produtos/growth-machine/catalogo-regras-negocio]]) cruzada com
> sistemas/práticas do Google já nomeados no cofre (Helpful Content
> System, E-E-A-T, Core Web Vitals). Classificação por confiança.

### 🔴 Confirmado

| RN | Redação | Prática que infringe | Ação recomendada |
|---|---|---|---|
| **RN-84** | "O sistema nunca sugere remover páginas, exceto quando o CS informa pedido explícito do cliente." | Helpful Content System — poda de conteúdo fraco/desatualizado é prática reconhecida; conteúdo ruim acumulado arrasta a qualidade percebida do domínio inteiro | Ajustar de bloqueio total para sugestão de candidata (ver tabela SEO acima) |

### 🟡 Candidato de risco — não confirmado

| RN | Redação | Risco potencial | Por que não é infração confirmada |
|---|---|---|---|
| **RN-14** + pipeline de conteúdo em escala | Geração de texto baseada no padrão da SERP, aplicada a ~2.500 clientes | Se o padrão virar template repetido mecanicamente entre clientes do mesmo nicho, esbarra no red-flag "conteúdo com template direto pra rankear" (Growth Excellence) e em "scaled content abuse" | Ainda é hipótese, não validada — não priorizar como backlog até virar achado confirmado |
| **RN-59** | Conteúdo só reavaliado a cada 6 meses (salvo força do analista) | Cadência pode ser lenta frente a sinais de degradação que o Google capta mais rápido | Já mapeado como gap de calibração no backlog ([[05-Backlog/gm-calibracao-thresholds-numeros-negocio]]) — é velocidade, não direção errada |
| **RN-07** | PageSpeed Score ≥80 como régua operacional MPI | Google não rankeia por "PageSpeed Score" diretamente — os fatores reais são Core Web Vitals (LCP/INP/CLS); se o threshold de 80 não foi validado contra esses 3 valores reais, pode aprovar página que falha em CWV real | Sem evidência no cofre de que isso já aconteceu — risco de descolamento entre métrica proxy e métrica real, ainda sem item de backlog próprio |

### 🟢 Verificado e descartado
- **RN-13** (Menu Header e Footer: mesmos itens) — fala de consistência de menu, não de estratégia de linkagem interna; não conflita com a prática de "cards substituem header/footer como linkagem" do Growth Excellence.
- **RN-50** (Boletim ao cliente sempre em tom de "melhoria") — comunicação com cliente final, fora do escopo de práticas técnicas de SEO/GEO.

### Leitura consolidada
De 122 RNs, **1 confirmada contra prática nomeada do Google** (RN-84), **3 candidatas de risco não confirmadas** (nenhuma delas pronta para virar item de backlog ainda), **2 verificadas e descartadas**. Proporção baixa — o produto está estruturalmente alinhado, com uma exceção clara e já endereçada na tabela de oportunidades acima.

## Notas relacionadas
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]
- [[03-Produtos/growth-machine/catalogo-regras-negocio]]
- [[03-Produtos/growth-machine]]
- [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]
- [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]]
- [[00-Cerebro]]
