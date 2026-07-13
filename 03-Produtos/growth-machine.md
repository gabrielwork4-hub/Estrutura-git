---
tipo: produto
status: em-desenvolvimento
criado: 2026-06-30
ultima-revisao: 2026-07-10
origem:
  - "Notion — transcrição @hoje 10:39 (BRT)"
  - "Drive — PRD_Growth_Machine_v1_9_14.md (16/06/2026)"
  - "Drive — REUNIÕES - AUTOMAÇÃO / Kickoff - Growth Machine"
tags: [produto, growth-machine, keywords, seo, prd]
---

# Growth Machine

## Visão geral
Plataforma interna de orquestração de SEO (Ideal Marketing · Busca Cliente ·
MPI Solutions) que automatiza o diagnóstico de ~2.500 projetos MPI de ponta
a ponta. Hoje cada analista gasta ~90h/mês diagnosticando manualmente
(Search Console, Excel, PageSpeed, SendGrid...). O método MPI funciona mas
vive na cabeça de especialistas sêniors — sem padronização nem escala.

**Pré-requisito (RN-108):** o GM só atende clientes presentes no **MPI Plus**.
Cliente fora do MPI Plus entra primeiro nele.

**O que NÃO faz (verbatim do PRD):**
> "O sistema não publica nada sozinho no site do cliente. O front-end de
> produção sempre executa manualmente. A automação para na geração da fila
> de ações. A execução técnica vive no Salesforce; o detalhe técnico
> permanece no Growth Machine."

**Separação obrigatória de papéis:**
- **Growth Machine** = diagnóstico, 100% interno. Não gera, não publica. Cliente não acessa.
- **MPI Plus** = geração de estudo/conteúdo/imagem + aprovação do cliente (portal-cliente).
- **Salesforce** = gestão de execução de atividades.

> **Posicionamento do MPI Plus (confirmado 2026-07-13):** o recorte acima
> descreve o papel do MPI Plus **dentro do fluxo do GM**, mas o produto em
> si é mais amplo — é o **sistema interno do Grupo**, que centraliza as
> informações do cliente desde o onboarding até a validação final. O GM é
> uma camada de diagnóstico que roda por cima de um cliente já dentro
> desse ciclo, não o dono do histórico do cliente. Ver
> [[03-Produtos/mpi-plus]] e [[03-Produtos/mpi-plus/mapa-funcionalidades-painel]].

---

## Impacto esperado

| Métrica | Hoje | Com Growth Machine |
|---|---|---|
| Horas de diagnóstico/analista/mês | ~90h | <10h |
| Cobertura da carteira | ~60 clientes/analista | 100% da carteira ativa |
| Consistência do método | Variável por analista | Padronizada pela fórmula MPI |
| Tempo para detectar lead zerado | Descoberto por acaso | <7 dias (alerta automático) |
| Briefings atualizados | <20% | >80% em 6 meses |
| Taxa de aceitação de ações sugeridas | N/A | >70% aceitas sem alteração |
| Capacidade equivalente liberada | — | ~10 analistas (sem contratar) |

---

## Como funciona — 4 fases

### Fase 1 — Entrada e Briefing

Três cenários de origem de dados:

| Cenário | Origem | Ação |
|---|---|---|
| A — Cliente no MPI Plus, dados completos | Briefing, estudo e histórico via API REST | Importação direta |
| B — Cliente no MPI Plus, briefing legado/incompleto (`customer_type='old'`) | MPI Plus + FireCrawl varre todas as páginas | Crawler enriquece; CS valida com cliente |
| C — Cliente fora do MPI Plus | N/A — fora de escopo (RN-108) | Encaminhar para MPI Plus |

**Fluxo de validação do briefing (conduzido pelo CS):**
```
Briefing pré-preenchido (crawler ou MPI Plus)
 → CS valida com cliente
 → CONFIRMADO → segue análise
 → AJUSTE NECESSÁRIO → CS ajusta (máx 2 iterações; 3ª rejeição → escala Gerente)
 → CLIENTE NÃO RESPONDE → sem prazo automático, fica pendente (RN-01)
```

**Régua de decisão do Estudo (Dim 1):**
- Score 80–100% → manter ou sugerir bonificação
- Score 50–79% → complementar ou reconciliar
- Score com briefing duvidoso → enviar pro CS
- Score <50% → reformular estudo (refazer no MPI Plus)

**Bonificação de palavras:** similaridade vetorial ≥70% via OpenAI embeddings.
Limitada a 50% do pacote contratado (RN-85). Anti-canibalização obrigatória.

**Briefing auto-incrementado (RN-80):** toda ação executada e validada no GM
incrementa automaticamente o briefing — nunca substitui o que foi aprovado.

---

### Fase 2 — Motor de Percepção (roda todo mês)

**Gatilho (RN-106):** chegada do relatório mensal do MPI Plus (~dia 1º/2)
dispara o ciclo para toda a carteira. Bright Data foi removido como integração
direta na v1.9.16 — o SPOF real é o próprio MPI Plus.

**6 etapas de coleta:**
1. Definir conjunto de palavras base (keywords contratadas)
2. Ler posicionamento real do relatório mensal MPI Plus
3. Filtrar só palavras do conjunto base
4. Calcular posição média
5. Converter posição em CTR: Top 3 → 20% / Top 10 → 5% / acima Top 10 → 1%
   (sem arredondamento — posição 10,5 = CTR 1%, RN-16) `[🔧 ajuste
   pendente]` curva única erra p/ Local Pack (mais achatada que orgânica) —
   segmentar via [[04-Decisões/adr-camada-calibracao-continua]]
6. Calcular `percentual_posicionamento_real`

**Tráfego de origem IA (RN-SGA-11, proposta, Fase 2):** segmentar no GA4 o
tráfego vindo de respostas de IA (ChatGPT, Perplexity), hoje invisível
neste motor.

**Curva de Maturidade (interpolação linear, RN-17):**

| Tempo no ar | Maturidade Base |
|---|---|
| 0–3 meses | 5% a 15% |
| 4–6 meses | 15% a 30% |
| 7–12 meses | 30% a 55% |
| 13–18 meses | 55% a 75% |
| 19–24 meses | 75% a 90% |
| Acima de 24 meses | 90% (fixo) |

**Teto de Crescimento:**

| Tempo total | Capacidade máxima |
|---|---|
| Até 12 meses | 60% |
| Até 24 meses | 90% |
| Acima de 36 meses | 100% |

**Fórmulas do Índice:**
```
trafego_potencial = volume_total × ctr_estimado
leads_potencial = trafego_potencial × taxa_conversao (default 5%)
maturidade_final = min(maturidade_base, teto)

indice_posicionamento = posicionamento_real / posicionamento_esperado
indice_trafego = trafego_real / trafego_esperado
indice_leads = leads_real / leads_esperados

indice_final = (indice_pos × 0.40) + (indice_traf × 0.40) + (indice_lead × 0.20)
```

**Pesos: 40 posicionamento / 40 tráfego / 20 leads** (configuráveis na Tela
8, RN-18). `[⚠️ sob revisão, 2026-07-10]` — diverge do documento original
do Gregory (40/30/30) e da ata da Reunião 05 ("lead é a principal
grandeza"), achado F-30. Mantido como vigente até calibração por dado real
(correlação peso×outcome de negócio da própria carteira), via a **Camada
de Calibração Contínua** — ver [[04-Decisões/adr-camada-calibracao-continua]].

**Classificação (thresholds inclusivos, RN-19):**

| Status | Índice Final | Cor | Cadência de análise |
|---|---|---|---|
| Ruim | < 0,60 | Vermelho | Mensal |
| Regular | 0,60–0,79 | Laranja | Mensal |
| Bom | 0,80–0,89 | Azul | Trimestral |
| Ótimo | ≥ 0,90 | Verde | Trimestral |

**Hard Stop (RN-64):** sem relatório mensal do MPI Plus → Motor não roda.

---

### Fase 3 — Auditoria em 10 Dimensões *(+ Dimensão 11, Fase 2 — ver abaixo)*

**Regra fundamental (RN-88):** a auditoria só é interrompida quando o problema
crítico está na **Dimensão 1 (Estudo)**. Se o Estudo está OK, as dimensões 2–10
são auditadas integralmente e geram ações simultâneas. A ordem MPI vale para
priorizar, não para interromper.

**Score de Saúde Técnica (determinístico, 0–100):**
```
Score = 100 − Σ(peso_dim × fator_severidade)
fator_severidade: OK=0 / aviso=0,4 / crítico=1,0
```

**Pesos por dimensão (default, soma=100):**

| Dim | Nome | Peso |
|---|---|---|
| 2 | Conteúdo / Imagem / GEO | 18 |
| 3 | Arquitetura MPI / Silo / Linkagem | 10 |
| 4 | W3C | 8 |
| 5 | PageSpeed | 15 |
| 6 | Schemas JSON-LD | 10 |
| 7 | Sitemap / Robots | 10 |
| 8 | Search Console / Sinais Externos | 14 |
| 9 | Servidor / TTFB / Infraestrutura | 7 |
| 10 | Captação / Entrega / Leads | 8 |

**Sub-dimensões 2D/2E não alteram o peso de Dim 2 (18):** são checagens
adicionais **dentro** do peso já alocado, não pontos extra — evita
desbalancear a soma=100 ao adicionar as sub-checks propostas (RN-SGA-01/02/03/04/07/08).

**Parecer Consolidado:** agente de IA lê Índice + Score + 10 dimensões +
Sentinela + histórico → diagnóstico executivo em linguagem natural. 1x por
análise completa. Os 3 indicadores são mantidos **separados** — sem score
único. `[nota futura]` quando a Dimensão 11 (GEO/Citação) for implementada,
o Parecer deve incorporá-la como 4º indicador citado, sem fundir no Score
de Saúde (RN-96 continua restrito às dimensões 2–10).

#### Dimensão 1 — Estudo / Auditoria MPI
Agente Auditor de Estudo MPI. Valida o estudo contra: briefing aprovado,
metodologia MPI Plus, pacote contratado, páginas MPI reais (FireCrawl),
relatório mensal + Search Console. Detecta: produtos sem cobertura,
canibalização, páginas órfãs, divergência keyword/title/H1/slug.

Score composto: Briefing↔Estudo (30%) / Estudo↔Páginas MPI (25%) /
Conformidade metodologia (25%) / Canibalização (10%) / Consistência com
pacote (10%).

DataForSEO e KeywordTools são **condicionais** — só quando a auditoria
indicar expansão/reformulação do estudo.

**O que a Dim 1 audita** vem construído fora do GM (RN-112: audita, não
gera) — as regras de **construção** do estudo (palavra épica, regiões,
tipos de produto/serviço) vivem em `RN-EST-01` a `RN-EST-06` no
[[03-Produtos/growth-machine/catalogo-regras-negocio]], origem Gregory/MPI
Plus, e no fluxo [[02-Fluxos/estudo-de-keywords]].

Quando crítico (score **<50%** **ou** canibalização crítica **ou** páginas
MPI fora do estudo **ou** briefing sem cobertura): **trava toda a auditoria**.

**Cluster via /informacoes (2026-07-10):** o estudo passa a mapear também
o **cluster de suporte** em `/informacoes` e `/artigos` — conteúdo
editorial fora do escopo contratado por keyword, que envelopa e eleva a
página MPI (pilar) sem alterar o contrato. Ver
[[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]].

**Portão de Diferenciação Real (RN-SGA-05, proposta, MVP — 2026-07-10,
validado externamente):** antes de gerar página/artigo (MPI ou cluster) por
combinação palavra×região×tipo,
checar sinais de diferenciação real (dado local específico, prova social da
combinação, resposta a pergunta real do contexto). Sem sinal suficiente:
página MPI não gera isolada — avalia cluster de suporte; artigo de cluster
não gera — incorpora como seção de outro artigo do mesmo cluster. Todo
gerado recebe `nivel_diferenciacao` (alto/médio/baixo) para auditoria.
Métrica: `taxa_diferenciacao_real` = páginas+artigos com nível alto/médio ÷
total — reportada no Score de Saúde (Dim 2) e como alerta de risco de
penalização.

> **Threshold reconciliado (2026-07-08):** o gate numérico é **<50%**, não
> <60% (resíduo de versões anteriores — achado F-03). O <50% alinha o
> travamento à banda de "reformular" da régua de decisão do Estudo (uma
> banda 50–79 "complementar" não deve travar toda a auditoria). Os 3
> gatilhos qualitativos permanecem como condições **OU** independentes do
> número — indispensáveis porque, por exemplo, canibalização pesa só 10% no
> score composto e sozinha jamais derrubaria o score abaixo de 50%. Ver
> [[03-Produtos/growth-machine/prd-v2-mvp]] Bloco 7.

#### Dimensão 2 — Conteúdo / Imagem / GEO
Agente Auditor de Conteúdo SERP. Pergunta central: *"esta página cobre a
intenção, tópicos, entidades e profundidade que o Google está premiando para
essa busca?"*

Fluxo: DataForSEO identifica concorrentes → crawler extrai conteúdo dos
concorrentes → monta padrão SERP → FireCrawl lê página do cliente → compara.

Subchecagens: 2A Conteúdo textual / 2B Imagens (WebP ≤200KB) / 2C GEO/AEO
(extrabilidade, **RN-SGA-01**, Fase 2) / **2D — AEO** (resposta única por
pergunta do nicho — **RN-SGA-02**, Fase 2; priorização por nicho —
**RN-SGA-04**, MVP) / **2E — E-E-A-T** (autor, página "sobre", fontes
citadas — **RN-SGA-07**, MVP). Também nesta dimensão: meta description
≤160/title ≤60 determinístico (**RN-SGA-03**, MVP) e sinal de conteúdo
original/information gain (**RN-SGA-08**, Fase 2). 2D e 2E propostas em
2026-07-10 — ver [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]].

Régua de decisão:
| Faixa | Score | Decisão |
|---|---|---|
| Excelente | 90–100% | Manter |
| Adequado | 80–89% | Ajuste pontual |
| Parcial | 60–79% | Complementar no MPI Plus |
| Crítico | <60% | Refazer no MPI Plus |
| Alterado há <60 dias | N/A | Aguardar maturação |

#### Dimensão 3 — Arquitetura MPI / Silo / Linkagem
Agente Auditor de Silo e Linkagem MPI. Fonte de verdade: estudo aprovado
no MPI Plus. FireCrawl mapeia a arquitetura real publicada.

Valida: papel de cada página (pilar, variação, lateral, indefinida, fora do
estudo), linkagem, âncoras, páginas órfãs, links quebrados, canonicals.

**Regra de direção MPI:** variações linkam entre si (lateral) e para o pilar
(para cima). O pilar **não** linka para variações (para baixo).

Crítico quando: variações sem link para pilar, páginas MPI órfãs, links
quebrados, ≥3 páginas fora da regra de linkagem.

**Linkagem do cluster (2026-07-10):** também audita se o conteúdo de
`/informacoes`/`/artigos` linka **para cima**, para a página MPI pilar —
é o mecanismo que eleva o ranqueamento do que foi contratado sem alterar o
contrato. Ver [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]].

**Canibalização entre subdomínios (RN-SGA-06, proposta, MVP):** estende a
auditoria a arquiteturas multi-subdomínio (ex: `www` × `loja`) — caso real
identificado no emtecorp, onde os dois competiam pela mesma keyword sem
nenhuma dimensão detectar.

**Auditoria retroativa de quase-duplicatas (validado externamente, alimenta
RN-SGA-05):** detecta páginas MPI existentes com estrutura/texto muito
parecidos, diferindo essencialmente na cidade ou tipo de negócio — sinal de
que um grupo deveria virar cluster ao redor de um pilar mais forte, em vez
de competir isoladamente. Ação hoje: só via aditiva (prioriza onde
construir cluster); consolidar as páginas fracas fica para Fase 2,
condicionado ao ajuste da RN-84. **Anti-canibalização dentro do próprio
cluster:** a mesma lógica de RN-15/RN-85 (bonificação) se estende à
cobertura de tópicos do cluster — não pode haver dois artigos respondendo
essencialmente à mesma pergunta.

#### Dimensão 4 — W3C / Validação Estrutural de HTML
Checagem **determinística**. W3C Validator self-hosted em Docker. A IA não
detecta — apenas traduz, agrupa e prioriza. Regra: erro repetido em várias
páginas = problema de template = macroatividade única.

#### Dimensão 5 — PageSpeed / Performance Front-end
Checagem **determinística por URL**. PageSpeed API/Lighthouse por URL,
separando mobile e desktop. Score ≥80 = régua operacional MPI. Problemas
de servidor/TTFB → encaminha para Dim 9. 400 req/dia de cota. `[📝 nota do
PO, 2026-07-13]` o score já dá direcionamento para os 3 pilares de CWV
(LCP/INP/CLS são componentes do próprio cálculo). `[🔧 ajuste pendente,
atenuado, RN-07]` falta formalizar os 3 valores individuais como critério
de gate, em vez de só o score agregado. **Pilares
agênticos (RN-SGA-15, proposta, Fase 2):** accessibility tree bem formada +
Cumulative Layout Shift — reaproveita a infraestrutura de PageSpeed já
existente aqui.

#### Dimensão 6 — Schemas JSON-LD / Dados Estruturados
Checagem **determinística**. Schemas mínimos por tipo de página (Organization
+ LocalBusiness em todas; Service+ItemPage+BreadcrumbList em landing pages
de serviço, etc.). **Regra anti-spam (RN-117):** reviews, ratings, preços, FAQ
só marcados quando existirem real e visivelmente na página. **Autoridade de
entidade (RN-SGA-14, proposta, Fase 2):** `sameAs` no schema + presença
fora do site.

#### Dimensão 7 — Sitemap / Robots / Indexabilidade Técnica
Checagem **determinística**. Não usa MPI Plus como fonte de verdade — usa
FireCrawl + parsers. Valida: sitemap acessível, robots sem bloqueio indevido,
canonical correto, noindex indevido, conflitos. Inclui checagem de LLM.txt e
AI Instructions (RN-82, `[🔧 ajuste pendente]` presença → qualidade).
**Controle de crawler de IA (RN-SGA-13, proposta, MVP):** GPTBot/ClaudeBot/
PerplexityBot/Google-Extended via robots.txt. **Refinamento validado
externamente:** distinguir bloqueio de treino (sem custo de GEO) de
bloqueio de citação ao vivo (custo real, principalmente Perplexity) —
matriz revisada trimestralmente. **Crawl-log real (RN-SGA-12, Fase 2):**
confirma se bots de IA/Googlebot de fato visitam, não só se têm permissão.
**Sinal PDF→HTML (RN-SGA-16, MVP):** conteúdo importante preso em PDF
sinaliza migração.

#### Dimensão 8 — Search Console / Presença no Google / Sinais Externos
Agente Tradutor de Presença no Google. 6 contas GSC `[🔧 teto de cobertura
identificado — 2.500 clientes/6 contas; expandir p/ 9-10 ou alocação
dinâmica, achado F-14/F-32]`. Não substitui o Motor de Percepção.
Subchecagens: 8A Indexação real / 8B Consultas e visibilidade / 8C Core Web
Vitals reais / 8D Backlinks tóxicos (SemRush). Disavow sempre com revisão
humana — nunca automático. **Ofensiva de autoridade (RN-SGA-09, proposta,
Fase 2):** 8D passa de reativa (só disavow) para propositiva (prospecção de
domínios/menções sem link ainda).

#### Dimensão 9 — Servidor / TTFB / Infraestrutura
GTmetrix por URL representativa. Não confundir com Dim 5 (performance
front-end). M3 (macroatividade de infra) não abre por medição isolada —
exige recorrência + evidência cruzada entre GTmetrix/PageSpeed/Sentinela.

#### Dimensão 10 — Captação, Entrega e Qualidade de Leads
Agente Auditor de Captação. Subchecagens: 10A Lead total multicanal /
10B Formulário / 10C SendGrid/DNS-MX / 10D WhatsApp e CTAs / 10E
Qualidade/spam. O sistema não bloqueia spam automaticamente — recomenda
CAPTCHA/honeypot. **Confirmação de entrega multicanal (RN-123/RN-124,
proposta, achado F-40):** 10D hoje só valida se o botão/link do WhatsApp
funciona — falta confirmação de entrega equivalente ao SendGrid
(delivered/bounce/read), via webhook da API WhatsApp Business (RN-123); e
10E precisa confirmar explicitamente que roda sobre o formato de mensagem
de cada canal, não só formulário (RN-124).

#### Dimensão 11 — GEO / Citação *(nova, Fase 2 — não implementada no MVP)*
Fecha o loop de mensuração que falta hoje: o GM prepara o site para ser
citável (Dim 2C/2D/RN-82), mas não mede se está sendo citado. Alimentada
pelo [[03-Produtos/ideal-tracker]] (Share of Voice em respostas de LLM) —
direção já confirmada pelo PO. RN-SGA-10. **Não entra na fórmula do Score
de Saúde Técnica (RN-96, restrita às dimensões estruturais 2–10)** — é um
sinal de mensuração separado, cujo peso no Índice Final (se algum) fica
para decisão futura. Ver
[[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]].

Cenários de alerta:
| Cenário | Condição | Ação |
|---|---|---|
| A — Lead total zerado, tem tráfego | Tráfego>0 E leads=0 | Alerta extremo |
| B — Lead salvo, não entregue | Lead no banco E evento SendGrid ausente/bounce | Alerta técnico |
| C — Lead total zerado ≥7 dias | Total multicanal=0 por 7 dias | Alerta EXTREMO |
| D — CTA WhatsApp quebrado | Botão/link ausente ou inválido | Corrigir CTA |

---

### Fase 4 — Workflow de Aprovação, Execução e Validação

```
Sistema gera fila de ações
 → Analista revisa e aprova
 → Ações aprovadas → exportadas como atividades no Salesforce (por área)
 → Execução técnica (Front-end) dá baixa no Salesforce
 → Conclusão no Salesforce → sincroniza status de volta ao GM
 → Analista aciona "Validar" no GM → ativa validação automática por IA (RN-81)
   → REPROVADO → volta para fila com notas
   → APROVADO (OK Final / Homologado) → registra data de validação
 → Início do bloqueio de maturação de 60 dias fixos (RN-27)
```

**RN-81:** ao acionar a validação, o sistema relê o site e confere se cada
ação foi realmente executada — compara estado anterior × atual.

**Boletim para o cliente (RN-50):** traduz ações em linguagem acessível.
Sempre "melhoria", nunca "problema".

---

## Módulo Sentinela

Módulo independente do ciclo de auditoria. Roda **diariamente, janela noturna
(00h–06h)**, cobrindo **100% dos sites** — inclusive projetos em maturação ou
bloqueados. Não usa APIs caras (sem Bright Data, DataForSEO, PageSpeed).
Fila via Laravel Horizon (Redis). Canal de alerta: E-mail + WhatsApp API.

**Checks diários:**
| Check | Severidade |
|---|---|
| Disponibilidade (uptime) | Crítica |
| SSL / HTTPS (alerta antecipado 30/15/7 dias, RN-95) | Crítica / Alta |
| DNS / MX | Alta |
| Redirecionamento | Média |
| robots.txt / sitemap.xml acessíveis | Média |
| Latência básica / TTFB simples | Média |
| AI Instructions / LLM.txt | Informativa |
| Mixed content | Baixa |

**Sobreposição ao bloqueio (RN-94):** site fora ≥3 dias ou SSL expirado =
alerta extremo e reabre análise mesmo em maturação.

---

## Agentes de IA

Modelo padrão: **GPT-5** (configurável por agente na Tela 9, RN-99).
Checagens determinísticas (Dim 4, 5, 6, 7, 9) não usam IA.
Embeddings: `text-embedding-3-small`.

| Agente | Dimensão | Objetivo |
|---|---|---|
| Auditor de Estudo MPI | Dim 1 | Auditar estudo contra briefing, metodologia, pacote e páginas reais |
| Auditor de Conteúdo SERP | Dim 2 | Extrair padrão SERP e comparar contra cada página MPI elegível |
| Auditor de Silo e Linkagem MPI | Dim 3 | Auditar se arquitetura real segue o estudo aprovado |
| Tradutor de Presença no Google | Dim 8 | Consolidar indexação, consultas, CWV e backlinks |
| Auditor de Captação e Entrega de Leads | Dim 10 | Cruzar volume multicanal, formulário, CTAs, entrega e spam |
| Tradutor de Infraestrutura / M3 | Dim 9 | Agrupar evidências de TTFB/infra e indicar escopo/recorrência |
| Camada de Tradução de Diagnóstico | Todas as dimensões | Converter diagnóstico técnico em ação localizada na linguagem do executor |
| Parecer Consolidado | Pós-auditoria | Diagnóstico executivo do projeto inteiro |

**Contrato obrigatório de prompt (esqueleto mínimo):**
```
[Identity] [Objetivo] [Entradas] [O que pode fazer] [O que não pode fazer]
[Regras vindas da Tela 8] [Critérios de confiança] [Quando escalar para humano]
[Quando não gerar ação] [Formato de saída JSON]
```

**Separação crítica (RN-100):** os agentes de Dim 1 e Dim 2 detectam o gap
— não geram. A geração ocorre no MPI Plus e só é acionada após clique do
analista. **Portão de Diferenciação Real (RN-SGA-05) entra exatamente
neste clique (Gate 1):** antes de a geração ser acionada, verifica sinais
de diferenciação real; sem sinal suficiente, a ação vira "recomendar
cluster de suporte" em vez de "gerar página isolada" — o gate não é um
mecanismo novo, é uma condição a mais dentro do Gate 1 já existente.

**Mecânica das entradas:** o orquestrador (context builder) coleta os dados
do projeto, monta um pacote JSON e injeta no prompt via placeholders
(`{{briefing}}`, `{{estudo_mpi_plus}}`, `{{serp_concorrentes}}` etc.).
O agente nunca busca dados sozinho.

---

## As 11 Telas

| Tela | Tipo | Objetivo |
|---|---|---|
| 1 — Painel de Carteira | Global | Lista priorizada por analista: status, Índice, Score, badge Sentinela, pendências |
| 2 — Painel Gerencial | Global | Visão consolidada das ~2.500 posições (Gerente/Supervisor) |
| 3 — Prontuário do Projeto | Projeto | Histórico imutável — Parecer + Score + Índice + timeline + métricas |
| 4 — Fila de Ações | Projeto | Revisar/aprovar ações e exportar ao Salesforce |
| 5 — Revisão de Conteúdo | Projeto | 4 colunas: Página atual / Padrão SERP / Diagnóstico / Conteúdo MPI Plus |
| 6 — Status de Execução | Global | Visão somente leitura do status sincronizado do Salesforce |
| 7 — Gestão de Perfis | Global | ACL, BUs, transferência de projetos |
| 8 — Parametrização do Modelo | Global | Calibrar pesos 40/40/20 (sob revisão), CTRs, thresholds, curva de maturidade, Score de Saúde — futuro lar da Camada de Calibração Contínua |
| 9 — Central de Agentes | Global | Configurar agentes, prompts, whitelists, schemas JSON, versionamento + rollback |
| 10 — Briefing e Estudo | Projeto | 3 colunas: Briefing / Estudo MPI Plus / Site real (FireCrawl) |
| 11 — Monitor Sentinela | Global | Saúde de infra diária de todos os sites |

**RN-98:** telas de projeto (3, 4, 5, 10) não ficam no menu — acessadas ao
selecionar um cliente no Painel de Carteira.

**Gap de amarração (2026-07-10):** nenhuma tela tem menção explícita de
onde `taxa_diferenciacao_real`/`nivel_diferenciacao` (Portão de
Diferenciação Real) ou o sinal da Dimensão 11 (GEO/Citação) aparecem para o
usuário — candidatos naturais são Tela 1 (badge) e Tela 3 (Prontuário),
mas isso não foi decidido, só apontado como lacuna a fechar antes do build
dessas features.

---

## Ferramentas externas integradas

| Ferramenta | Finalidade |
|---|---|
| **Relatório Mensal MPI Plus** | Fonte primária: posicionamento, tráfego orgânico e leads |
| **MPI Plus API** | Import de briefing/estudo + acionamento de geração (delegada) |
| **Salesforce** | Gestão de atividades (bidirecional — RN-74 a RN-78) |
| **FireCrawl** | Crawler completo do site do cliente (todas as páginas) |
| **Google Search Console** (6 contas) | Indexação, consultas, CWV reais, impressões |
| **GA4 do cliente** | Gatilho de queda abrupta de tráfego (≥30%/7d, RN-68) |
| **PageSpeed API / Lighthouse** | Performance por URL, mobile e desktop (Dim 5) |
| **GTmetrix** | TTFB/infraestrutura por URL representativa (Dim 9) |
| **DataForSEO** | SERP e concorrentes (Dim 2 principal; Dim 1 condicional) |
| **KeywordTools** | Volume de busca (condicional na Dim 1) |
| **OpenAI (GPT-5 + text-embedding-3-small)** | Agentes de IA + similaridade vetorial |
| **SendGrid** | Log de entrega de leads — pull diário obrigatório (RN-56) |
| **W3C Validator** (Docker self-hosted) | Validação HTML determinística (Dim 4) |
| **SemRush Business** | Backlinks tóxicos (Dim 8) |
| **DNS/MX checker** | SPF/DKIM/DMARC (Dim 10) |
| **HTTP checker** | Status, latência, CTAs (Dim 7, 9, 10, Sentinela) |
| **WhatsApp Business API** (webhook de status) | `[proposta, RN-123]` Confirmação de entrega multicanal — enviado/entregue/lido/falhou (Dim 10). Distinto do WhatsApp API de notificação (RN-51) |

---

## Decisões técnicas

- **Stack:** PHP/Laravel + Laravel Horizon (Redis) para filas
- **Modelo de dados:** instância única, base compartilhada (não multi-tenant
  isolado, v1.9.17). As 3 empresas compartilham base; partição lógica por
  `empresa` + `bu` com row-level access
- **Autenticação:** SSO integrado com MPI Plus (GM não armazena senhas)
- **Integração MPI Plus (RN-101):** padrão assíncrono — request →
  `IntegrationJob` → webhook assinado / importação de status
- **Integração Salesforce:** bidirecional resiliente a falhas (retry +
  reconciliação). Só título e escopo da atividade trafegam — sem conteúdo
  técnico (RN-78)
- **RN-104:** cliente nunca acessa o GM. Acessa só o MPI Plus.

---

## Regras de negócio chave
Subconjunto das mais citadas. Catálogo completo (RN-01 a RN-122) em
[[03-Produtos/growth-machine/catalogo-regras-negocio]].

- **RN-01:** análise não avança sem validação ativa do cliente/CS — sem prazo automático.
- **RN-02:** cadência Ruim/Regular = mensal; Bom/Ótimo = trimestral.
- **RN-16:** sem arredondamento de CTR — posição 10,5 = CTR 1%.
- **RN-18:** pesos configuráveis, soma=100%. Default: **40/40/20** (posição/tráfego/leads) — `[⚠️ sob revisão]`, calibração pendente via Camada de Calibração Contínua.
- **RN-27:** janela de maturação = 60 dias fixos.
- **RN-40:** site fora do ar: 3 tentativas falhas em dias diferentes = alerta.
- **RN-47:** aprovação humana obrigatória — nada publicado automaticamente.
- **RN-50:** boletim para cliente sempre como "melhoria", nunca "problema".
- **RN-59:** após 1º ajuste de conteúdo, Dim 2 só reavaliada em 6 meses (salvo força do analista).
- **RN-64:** sem relatório mensal do MPI Plus → Hard Stop completo do Motor.
- **RN-68:** sem reprocessamento com ações pendentes, exceto críticas (lead zerado ≥7d, site fora ≥3d, queda ≥30% em 7d).
- **RN-73:** proibido armazenar/exibir métricas financeiras, custo por token ou precificação de APIs na interface ou logs públicos.
- **RN-80:** briefing auto-incrementado — nunca substitui o aprovado.
- **RN-81:** validação automática por IA pós-execução relê o site e confere cada ação.
- **RN-82:** sistema valida presença de AI Instructions e LLM.txt.
- **RN-85:** bonificação limitada a 50% do pacote contratado.
- **RN-86:** `trafego_real` = apenas tráfego orgânico (exclui pago).
- **RN-88:** auditoria só travada quando Dim 1 for crítica. Se Estudo OK, Dim 2–10 rodam em paralelo.
- **RN-95:** alerta antecipado SSL: 30/15/7 dias antes do vencimento.
- **RN-99:** modelo padrão dos agentes = GPT-5. Configurável por agente.
- **RN-100:** GM detecta o gap; geração ocorre no MPI Plus, após clique do analista.
- **RN-104:** GM é exclusivamente interno — cliente não acessa.
- **RN-106:** relatório mensal (~dia 1º/2) é o único gatilho de calendário.
- **RN-107:** `leads_real` = total multicanal (formulário + WhatsApp + demais canais).
- **RN-108:** estar no MPI Plus é pré-requisito para ser monitorado pelo GM.
- **RN-122:** toda execução de agente deve registrar `prompt_version_id`, `ruleset_version_id`, entradas, ferramentas, saída JSON, confiança e auditoria.

---

## Questões em aberto (não encerradas)

| ID | O que falta definir |
|---|---|
| Q9 | SLA de revisão/geração de conteúdo — a definir com a área |
| Q17 | Origem do conteúdo dos concorrentes na Dim 2 (FireCrawl ou outra camada) |
| Q18–Q21 | Mapeamento GM↔Salesforce (objeto, direção do sync, relatório como nota ou só no GM) |
| Q23 | Régua de posicionamento por período (análoga à curva de tráfego) |
| Q24 | Limite de tentativas de ajuste de conteúdo antes de escalar ao gestor |
| Q25–Q26 | Escopo exato do Sentinela por projeto + infraestrutura do cron |
| Q27–Q30 | Autenticação GM→API MPI Plus, reconciliação de assets gerados, publicação WordPress, idempotência de geração |

**Ponto mais crítico do PRD:**
> *"A casa é entregue vazia; os móveis são os prompts"* — o conteúdo fino
> dos prompts dos agentes ainda precisa ser montado com os especialistas de Growth.

---

## Status atual (10:39 — Notion, 2026-06-30)
- Conectar **Wiki Data ao fluxo** e definir os principais indicadores.
- Estudar a documentação da Growth Machine (PRD v1.9.14) para identificar melhorias.
- O **briefing preenchido** será a base de toda a estratégia.
- Implementação de blog (implementação + relatório).
- Trabalhar com o **conteúdo MPI Plus**.

## Responsáveis
_A preencher — PO ainda mapeando stakeholders (ver [[00-Painel-Estado]])._

## Funcionalidades
- [ ] Conectar Wiki Data ao fluxo
- [ ] Definir principais indicadores (pesos posicionamento/tráfego/leads)
- [ ] Estruturar briefing como base da estratégia (validação via CS)
- [ ] Implementar blog (implementação + relatório)
- [ ] Integrar conteúdo MPI Plus
- [ ] Exportação de fila de ações para Salesforce
- [ ] Montar prompts dos agentes com especialistas de Growth (Q abertas)
- [ ] Resolver questões em aberto Q18–Q21 (mapeamento Salesforce)
- [ ] Resolver questões em aberto Q27–Q30 (integração MPI Plus)

---

## Avaliação crítica (revisão fase a fase)
A revisão crítica ponto a ponto do fluxo (pontos fortes, riscos e observações
candidatas a backlog, fase por fase) está sendo construída em paralelo em
[[03-Produtos/growth-machine/avaliacao-fluxo]].

## Cheat sheet
Resumo de 1 página com só os números/regras que valem memorizar (pesos,
thresholds, ordem das fases/dimensões, os 5 padrões de risco recorrentes)
em [[03-Produtos/growth-machine/cheat-sheet]].

## PRD final
A estrutura final do PRD (13 blocos, RFs, User Stories/CA, checagem de
aderência a boas práticas Google 2026 cruzada com RN/Dimensão) está
consolidada em [[PRDFINAL]] (2026-07-10) — cópia de leitura para build,
substitui [[03-Produtos/growth-machine/prd-v2-mvp]] (mantido como histórico
da consolidação).

## Aderência à documentação ideal (base da v2)
Avaliação da documentação atual contra a estrutura de PRD ideal (13 blocos)
e auditoria das 122 RNs contra critérios de qualidade, cruzando vault +
Drive — com o esqueleto proposto da nova documentação e o checklist "pronto
para dev": [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]].

## Comparativo de maturidade SEO vs. GEO/AEO
Nota evolutiva, atualizada conforme houver progresso real: score atual
(SEO ~75-80% / GEO/AEO ~25-30% / combinado ~55-60%, leitura de
2026-07-03) e histórico de leituras em
[[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]. Versão
consolidada com os princípios-núcleo transversais aos 3 pilares e a fila
única de prioridade (cruzando SEO/GEO/AEO em vez de 3 filas separadas) em
[[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]].

## Preparação de reunião
Nota de preparo para reuniões com o responsável pelos POs — RNs mais
prováveis de aparecer por tema, números-chave e as perguntas de
confirmação (sem reabrir debate técnico já mapeado) em
[[03-Produtos/growth-machine/prep-reuniao-po-lead]].

## Cruzamento com outras notas
- A implementação de blog e o conteúdo MPI Plus dependem diretamente de
  [[02-Fluxos/estudo-de-keywords]] (clusterização, anti-canibalização,
  variações locais) — a Dimensão 1 da auditoria (Estudo/Auditoria MPI) é
  exatamente onde isso se aplica.
- O prompt de avaliação e arquitetura de keywords (v2) alimenta diretamente
  a Dimensão 2 (Conteúdo/Imagem/GEO) e a lógica de pilar/cluster das páginas
  MPI — ver [[02-Fluxos/prompt-avaliacao-keywords]].
- Faz parte do processo geral descrito em [[02-Fluxos/processo-kickoff-discovery]].
- Depende do **MPI Plus** como pré-requisito de carteira — ver [[03-Produtos/mpi-plus]].

## Decisões relacionadas
- [[PRDFINAL]] (2026-07-10) — PRD final consolidado, com checagem de aderência a boas práticas Google 2026.
- [[04-Decisões/migracao-prompt-keywords-v2]] — migração do prompt de keywords
  (v1→v2) impacta diretamente a Dim 1 (Estudo) e Dim 2 (Conteúdo) do GM.
- [[04-Decisões/adr-camada-calibracao-continua]] (2026-07-10) — RN-18 mantida em 40/40/20 sob revisão; calibração por dado real via Camada de Calibração Contínua (substitui a tentativa inicial 35/20/45, [[04-Decisões/adr-pesos-indice-performance-2026]], superada).
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] (2026-07-10) — cluster via /informacoes/artigos como camada de ranqueamento aditiva, sem alterar o contrato por keyword; validada externamente e enriquecida com o Portão de Diferenciação Real.

## Ideias relacionadas
-
