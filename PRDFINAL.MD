---
tipo: produto
status: vivo
criado: 2026-07-10
ultima-revisao: 2026-07-10
versao-doc: "PRD Final v1.0 — estrutura consolidada, pendências explícitas"
consolida:
  - "[[03-Produtos/growth-machine/prd-v2-mvp]]"
  - "[[03-Produtos/growth-machine/catalogo-regras-negocio]]"
  - "[[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]"
  - "[[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]]"
  - "[[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]]"
  - "[[03-Produtos/growth-machine/validacao-fluxos-principios]]"
  - "[[03-Produtos/growth-machine/plano-fechamento-prd-v2]]"
  - "[[04-Decisões/adr-camada-calibracao-continua]]"
  - "[[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]"
tags: [growth-machine, prd, final, mvp, seo, geo, aeo, google-2026, rn, build]
---

# PRD Final — Growth Machine (v1.0)

> **O que é este arquivo:** a estrutura final do PRD do Growth Machine —
> os 13 blocos consolidados, com **todas as reconciliações já fechadas no
> cofre aplicadas como texto principal** (não como nota à margem), mais uma
> checagem explícita de aderência a boas práticas Google 2026 cruzada com a
> estrutura interna (RNs/Dimensões). Substitui
> [[03-Produtos/growth-machine/prd-v2-mvp]] como **cópia de leitura para
> build** — aquele documento fica preservado como o rascunho de
> consolidação que originou este (histórico, não apagado).
>
> **Honestidade obrigatória (regra do cofre):** este arquivo não declara o
> produto "pronto para codar". Ele estrutura tudo que **já está decidido**
> e sinaliza explicitamente (`⚠️`/`🔴`/`🕒`) tudo que **ainda não está** —
> ver "Estado de fechamento" no final. Nenhuma pendência foi escondida para
> este documento parecer mais fechado do que está.
>
> **RNs (fonte única, não recopiadas aqui):** [[03-Produtos/growth-machine/catalogo-regras-negocio]]
> (146 RNs: 122 oficiais + RN-123/RN-124 propostas + 6 `RN-EST-*` + 16 `RN-SGA-*`).
> **Padrão de User Story/CA:** [[04-Decisões/padrao-historia-jira]].

## Como ler este documento (anti-canibalização documental)
Para que RN e PRD **não se canibalizem**, cada tipo de conteúdo tem uma
única casa:

| Artefato | Diz | Mora em | Aqui no PRD Final |
|---|---|---|---|
| **RF** | O quê o sistema faz | Este PRD (Bloco 5) | Definido |
| **RN** | A restrição/lógica que governa | [[03-Produtos/growth-machine/catalogo-regras-negocio]] | Só **referenciado** por ID |
| **NFR** | Quão bem | Este PRD (Bloco 6) | Definido |
| **CA** | Como se testa | Este PRD (Bloco 8) | Amarra CA→RN |

Regra de ouro: **RF ≠ RN ≠ NFR ≠ CA**. Se um parágrafo estiver fazendo
dois papéis, ele está no lugar errado.

## Tabela de versões
| Versão | Data | Mudança |
|---|---|---|
| v2.0-mvp (cofre) | 2026-07-08 | [[03-Produtos/growth-machine/prd-v2-mvp]] — consolidação inicial nos 13 blocos |
| **v1.0-final (este arquivo)** | 2026-07-10 | Reconciliações aplicadas como texto principal (pesos 40/40/20 sob revisão, Cluster Wrapping, Portão de Diferenciação Real, RN-SGA/RN-EST/RN-123-124); **8 RFs novas** (RF-47 a RF-54) formalizando itens que só existiam em prosa; seção dedicada de aderência a boas práticas Google 2026 |

---

## Bloco 1 — Contexto / Problema
2.500 clientes ativos em 3 empresas (Ideal Marketing · Busca Cliente · MPI
Solutions). Cada analista de Growth gasta **~90h/mês** diagnosticando no
olho (Search Console, Excel, PageSpeed, SendGrid, um a um). O método MPI é
eficaz mas vive na cabeça de sêniors — some quando o sênior sai, erra com
analista novo, e não há headcount para diagnosticar todo mês.

**Consequências hoje:** briefing desatualizado (<20% da carteira), lead
zerado descoberto por acaso (cliente liga furioso), upsell perdido, ~10
analistas de capacidade parados em triagem manual, e — achado mais recente
— um risco ativo de penalização por doorway/scaled content nos core
updates de 2026 (ver "Alinhamento com boas práticas Google 2026" abaixo).

## Bloco 2 — Objetivo + Métricas de sucesso
**North Star (proposta, a confirmar com o PO):** **% da carteira ativa
diagnosticada dentro da cadência correta, com fila de ações aprovada.**

| Métrica | Hoje | Meta MVP |
|---|---|---|
| Horas de diagnóstico/analista/mês | ~90h | <10h |
| Cobertura da carteira | ~60 clientes/analista | 100% da carteira ativa |
| Tempo para detectar lead zerado | por acaso | <7 dias (alerta) |
| Taxa de ações aceitas sem alteração | N/A | >70% |
| Briefings atualizados | <20% | >80% em 6 meses |
| `taxa_diferenciacao_real` (novo — antídoto doorway) | não medido | reportada no Score de Saúde, sem meta numérica ainda (calibra após Frente Z1) |

> As frentes GEO/AEO **não têm meta numérica** no MVP — coerente com a
> decisão de manter a medição real de GEO (Dimensão 11) fora do MVP.

## Bloco 3 — Escopo (dentro / fora)

**Dentro do MVP:**
- Fases 1–4 completas + Módulo Sentinela.
- As 10 dimensões de auditoria (faseamento interno no Bloco 9).
- Governança humana (RN-47) e dois gates de geração delegada (RN-100).
- GEO/AEO **como checklist técnico/semântico determinístico** (Dim 2C/2D/2E,
  RN-82, schemas) — não como medição de citação (isso é Fase 2).
- **Cluster Wrapping** — `/informacoes` e `/artigos` como camada aditiva de
  cluster ao redor do pilar contratado, **sem alterar o contrato por
  keyword** (RF-47, RF-51) — [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]].
- **Portão de Diferenciação Real** — condição do Gate 1 antes de gerar
  página/artigo por combinação palavra×região×tipo (RF-54) — antídoto
  direto ao achado F-39 (doorway/scaled content abuse), hoje o item de
  maior prioridade do produto inteiro.
- Sub-checks determinísticas novas em Dim 2 (meta/title, priorização AEO
  por nicho, E-E-A-T on-page) e Dim 7 (crawler de IA, PDF→HTML) — RF-48 a
  RF-53, todas baratas e sem dependência de golden-set de prompt.

**Fora do MVP (decisão explícita):**
- **Medição real de GEO/AEO** (citação em LLM, Share of Voice, "sou a
  resposta escolhida") — **Dimensão 11, Fase 2** (achado F-28).
- Itens `RN-SGA-*` marcados Fase 2 no catálogo: extrabilidade (01),
  resposta única AEO (02), conteúdo original/information gain (08),
  ofensiva de backlink (09), tráfego de origem IA (11), crawl-log real
  (12), autoridade de entidade/`sameAs` (14), pilares agênticos (15).
- **RN-123/RN-124** (confirmação de entrega multicanal WhatsApp, paridade
  de spam por canal) — seguem **propostas**, implementação é item de Track
  F, não deste PRD.
- Consolidar/remover páginas-doorway **já existentes** na carteira —
  depende do ajuste da RN-84 (bloqueio → sugestão de poda), decisão
  posterior por escopo do ADR de cluster.
- Cliente fora do MPI Plus (RN-108); site fora do padrão MPI (RN-36).
- GM **não publica nada** no site do cliente — a automação para na fila de
  ações; execução é manual, via Salesforce.

## Bloco 4 — Personas / público
| Persona | Papel no fluxo | Acesso |
|---|---|---|
| **Analista de Growth** | Aprova a fila de ações e valida a execução (RN-49) | GM interno |
| **CS (Customer Success)** | Valida o briefing com o cliente (RN-01) | GM interno |
| **Gerente / Supervisor** | Recebe escalonamentos (RN-06, RN-45) e visão consolidada (Tela 2) | GM interno |
| **Front-end (executor)** | Executa as ações e dá baixa no Salesforce | Salesforce |
| **Cliente** | Aprova estudo/conteúdo/imagem **no MPI Plus**, nunca no GM (RN-104) | MPI Plus |

> Lacuna herdada (backlog): o CS não tem tela/visão própria mapeada (fila
> de briefings pendentes).

## Bloco 5 — Requisitos Funcionais (RF)
Coluna **MVP**: ✅ dentro · 🕒 fast-follow · ⏭️ Fase 2. **RF-47 a RF-54 são
novas nesta consolidação** — formalizam itens que já estavam decididos
(ADRs, catálogo RN-SGA marcado "✅ MVP") mas só existiam em prosa no PRD
anterior, sem número de RF próprio.

### Elegibilidade e Fase 1 — Entrada e Briefing
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-00** | Admitir apenas clientes presentes no MPI Plus; encaminhar os demais | RN-108 | ✅ |
| **RF-01** | Importar briefing/estudo/histórico via API do MPI Plus (dados completos) | RN-101, RN-102 | ✅ |
| **RF-02** | Varrer todas as páginas via FireCrawl e pré-preencher briefing legado (`customer_type='old'`) | RN-69, RN-102 | ✅ |
| **RF-03** | Conduzir a validação do briefing pelo CS, bloqueando o avanço até validação ativa | RN-01, RN-06 | ✅ |
| **RF-04** | Calcular score de aderência do estudo e aplicar a régua de decisão | RN-04 | ✅ |
| **RF-05** | Sugerir bonificação por similaridade vetorial, limitada a 50% do pacote, sem canibalização | RN-15, RN-85 | ✅ |
| **RF-06** | Incrementar o briefing a cada ação validada, sem substituir o aprovado | RN-80 | ✅ |

### Fase 2 — Motor de Percepção
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-07** | Disparar o ciclo para toda a carteira na chegada do relatório mensal | RN-106 | ✅ |
| **RF-08** | Hard Stop total quando o relatório mensal estiver ausente | RN-64 | ✅ |
| **RF-09** | Converter posição média em CTR por faixa, sem arredondamento [⚠️ pendente: segmentação Local Pack × orgânica, Track F] | RN-16 | ✅ |
| **RF-10** | Calcular maturidade por interpolação linear e aplicar teto de crescimento | RN-17 | ✅ |
| **RF-11** | Calcular o Índice de Performance com pesos parametrizáveis (default **40/40/20**, ⚠️ sob revisão — Camada de Calibração Contínua) | RN-18 | ✅ |
| **RF-12** | Classificar em Ruim/Regular/Bom/Ótimo (thresholds inclusivos) e definir cadência | RN-19, RN-02 | ✅ |
| **RF-13** | Usar `trafego_real` só orgânico e `leads_real` multicanal [⚠️ pendente: emenda RN-107 enumerando "demais canais", Track F] | RN-86, RN-107, RN-110 | ✅ |
| **RF-14** | Alertar "sem estudo válido" quando `volume_total = 0` | RN-20 | ✅ |

### Fase 3 — Auditoria em 10 Dimensões (+ Dimensão 11 fora do MVP)
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-15** | Interromper a auditoria **apenas** quando a Dim 1 for crítica; senão, rodar 2–10 em paralelo | RN-88 | ✅ |
| **RF-16** | Calcular o Score de Saúde Técnica determinístico (0–100), restrito às dimensões 2–10 | RN-96 | ✅ |
| **RF-17** | Rodar Dim 4, 5, 6, 7, 9 como checagem determinística, sem IA | RN-99, RN-115–120 | ✅ |
| **RF-18** | Dim 1 — auditar o estudo contra briefing/metodologia/pacote/páginas reais | RN-112 | ✅ |
| **RF-47** | **[NOVO]** Dim 1 — mapear o **cluster de suporte** (`/informacoes`, `/artigos`) ao redor do pilar contratado, sem alterar o contrato por keyword | RN-SGA-05 (parte), RN-EST-06 | ✅ |
| **RF-19** | Dim 2 — extrair padrão SERP e comparar cobertura por página MPI (IA, depende de golden-set) | RN-113 | 🕒 |
| **RF-48** | **[NOVO]** Dim 2 — checagem **determinística** de meta description ≤160 / title ≤60 (independe de golden-set) | RN-SGA-03 | ✅ |
| **RF-49** | **[NOVO]** Dim 2 (2D) — priorizar AEO por nicho, reaproveitando a segmentação já coletada no briefing | RN-SGA-04 | ✅ |
| **RF-50** | **[NOVO]** Dim 2 (2E) — auditar sinais de E-E-A-T on-page: autor, página "sobre", fontes citadas | RN-SGA-07 | ✅ |
| **RF-20** | Dim 3 — auditar silo/linkagem contra o estudo aprovado | RN-114 | 🕒 |
| **RF-51** | **[NOVO]** Dim 3 — auditar linkagem cluster→pilar e canibalização entre subdomínios (ex: `www` × `loja`) | RN-SGA-06 | ✅ |
| **RF-21** | Dim 6 — validar schemas e **bloquear** schema fabricado (reviews/preços/FAQ não verificáveis) | RN-117 | ✅ |
| **RF-22** | Dim 7 — validar sitemap/robots + presença de AI Instructions/LLM.txt | RN-118, RN-82 | ✅ |
| **RF-52** | **[NOVO]** Dim 7 — controlar crawlers de IA (GPTBot/ClaudeBot/PerplexityBot/Google-Extended) via robots.txt, distinguindo bloqueio de treino × bloqueio de citação ao vivo | RN-SGA-13 | ✅ |
| **RF-53** | **[NOVO]** Dim 2 + Dim 7 — sinalizar conteúdo importante preso em PDF, sugerindo migração para HTML | RN-SGA-16 | ✅ |
| **RF-23** | Dim 8 — consolidar GSC + backlinks; disavow sempre com revisão humana | RN-119 | 🕒 |
| **RF-24** | Dim 10 — auditar captação/entrega/qualidade de leads e disparar alertas A/B/C/D [⚠️ pendente: incorporar RN-123/RN-124 quando implementadas, Track F] | RN-121, RN-107, RN-109 | ✅ |
| **RF-25** | Gerar o Parecer Consolidado por IA (1x/análise), mantendo Índice + Score + dimensões separados | RN-97 | ✅ |
| **RF-26** | Rodar a Camada de Tradução de Diagnóstico (traduz/enriquece, não detecta) | RN-89 | ✅ |

> **Nota de estruturação:** RF-19/20/23 seguem 🕒 (fast-follow) porque
> dependem do golden-set dos prompts (risco "casa vazia" do Bloco 11). As
> RFs novas 47–53 foram deliberadamente separadas por serem **checagens
> determinísticas ou baseadas em dado já coletado** — não herdam o mesmo
> bloqueio e por isso entram ✅ desde o MVP.

### Fase 4 — Aprovação, Execução e Validação
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-27** | Priorizar e apresentar a fila de ações para aprovação do analista | RN-44, RN-47 | ✅ |
| **RF-28** | Acionar a geração no MPI Plus só após clique (Gate 1) + revisar o asset (Gate 2) | RN-100 | ✅ |
| **RF-54** | **[NOVO]** Gate 1 — aplicar o **Portão de Diferenciação Real** antes de acionar a geração de página/artigo por combinação: checar dado local específico, prova social da combinação, resposta a pergunta real; sem sinal suficiente, recomendar cluster de suporte em vez de página isolada; registrar `nivel_diferenciacao` | RN-SGA-05 (parte) | ✅ |
| **RF-29** | Exportar ao Salesforce só ações aprovadas, agrupadas por área, só título e escopo | RN-75, RN-76, RN-78 | ✅ |
| **RF-30** | Sincronizar de volta o status quando a atividade é concluída no Salesforce | RN-77 | ✅ |
| **RF-31** | Reler o site na validação e conferir cada ação executada (validação por IA) | RN-81 | ✅ |
| **RF-32** | Iniciar a maturação de 60 dias só após o OK final do analista | RN-27, RN-79 | ✅ |
| **RF-33** | Tratar execução parcial ("2 de 6") reintroduzindo o restante no ciclo seguinte | RN-46 | ✅ |
| **RF-34** | Registrar motivo e escalar ao Supervisor/Líder quando uma ação é desconsiderada | RN-45 | ✅ |
| **RF-35** | Alertar o gerente quando uma ação gerada não é executada em 28 dias | RN-04, RN-28 | ✅ |
| **RF-36** | Gerar o boletim ao cliente sempre como "melhoria", nunca "problema" | RN-50 | ✅ |

### Módulo Sentinela
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-37** | Rodar checagens diárias leves em 100% dos sites, inclusive bloqueados/em maturação | RN-90, RN-91, RN-93 | ✅ |
| **RF-38** | Emitir alerta antecipado de SSL em 30/15/7 dias | RN-95 | ✅ |
| **RF-39** | Reabrir análise mesmo em maturação diante de incidente crítico (site fora ≥3d, SSL expirado) | RN-94 | ✅ |
| **RF-40** | Notificar por E-mail + WhatsApp API | RN-51 | ✅ |

### Transversais (governança, telas, agentes)
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-41** | Registrar em todo log `prompt_version_id`, `ruleset_version_id`, entradas, saída JSON, confiança | RN-122 | ✅ |
| **RF-42** | Nunca expor métricas financeiras/custo por token na interface ou logs públicos | RN-73 | ✅ |
| **RF-43** | Parametrizar pesos/CTRs/thresholds/curva na Tela 8 (nenhum prompt hardcoda regra parametrizável) | RN-18, RN-122 | ✅ |
| **RF-44** | Gerir agentes/prompts/whitelists/schemas com versionamento e rollback na Tela 9 | RN-99, RN-122 | ✅ |
| **RF-45** | Controlar acesso por perfil/BU com row-level access (Tela 7) | RN-53, RN-54 | ✅ |
| **RF-46** | Exibir telas de projeto (3,4,5,10) só via seleção de cliente, não no menu | RN-98 | ✅ |

## Bloco 6 — Requisitos Não-Funcionais (NFR)
- **NFR-01 Disponibilidade:** ≥99,5% em horário comercial. *Gap a fechar:*
  definir alvo fora do horário comercial (Sentinela roda 24/7, RN-94).
- **NFR-02 Segurança:** credenciais de API nunca no front; sem custo/token
  na interface (RN-73); row-level access entre empresas (alto blast radius
  — exige teste de escopo).
- **NFR-03 LGPD/Retenção:** Sentinela ≥90 dias; SendGrid local ≥3 meses
  (RN-56). *Gap a fechar:* prazo de retenção de diagnóstico/briefing/histórico.
- **NFR-04 Integração assíncrona:** MPI Plus via `IntegrationJob` + webhook
  assinado (RN-101); Salesforce bidirecional resiliente (retry + reconciliação).
- **NFR-05 Stack:** PHP/Laravel + Laravel Horizon (Redis) para filas.
- **NFR-06 Auth:** SSO com MPI Plus (GM não guarda senha). *Risco:* SPOF de
  login se o MPI Plus cair.
- **NFR-07 Degradação:** Hard Stop só no cenário sem posicionamento (RN-64);
  demais falhas degradam graciosamente.
- **NFR-08 [NOVO] Auditabilidade da calibração contínua:** toda proposta de
  recalibração (pesos, CTR, curvas, thresholds) roda como job periódico que
  **gera proposta, nunca aplica direto**; requer aprovação humana (Gerente/
  Admin) na Tela 8/9; log imutável com valor anterior, novo, fonte,
  aprovador e data. Ver [[04-Decisões/adr-camada-calibracao-continua]].

## Bloco 7 — Regras de Negócio (RN) — referência + reconciliação
As RNs **não são recopiadas aqui** (fonte única no catálogo). Reconciliações
já aplicadas ao catálogo:

| Ação de reconciliação | RNs | Origem do achado |
|---|---|---|
| **Pesos mantidos em 40/40/20, sob revisão** — calibração real via Camada de Calibração Contínua (C3/C4), não decreto | RN-18 | [[04-Decisões/adr-camada-calibracao-continua]] |
| **Marcadas `[SUPERSEDIDA]`** — lead só formulário → multicanal | RN-21, RN-22, RN-23 → RN-107/RN-121 | F-05 |
| **Marcada `[SUPERSEDIDA]`** — contradiz réguas por dimensão | RN-29 | F-05 |
| **Marcada `[SUPERSEDIDA]`** — contradiz travamento condicional | RN-32 → RN-88 | F-05 |
| **Threshold Dim 1 fixado em <50%** | RN-88 | F-03 |
| **Resíduo Bright Data removido** — posicionamento vem só do relatório mensal | RN-64, RN-105 | F-01 |
| **Blocos novos** `RN-EST-01–06` (Gregory) e `RN-SGA-01–16` (proposta SEO/GEO/AEO) | novo | [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] |
| **RN-123/RN-124 reais** (confirmação de entrega multicanal, vault externa) — propostas, não oficiais | novo | F-40 |

> **RFs do PRD atualizadas quando Track F fechar** — 3 dependências não
> resolvidas ainda alteram RFs deste documento quando as RNs mudarem:
> RN-123/RN-124 → `RF-24`; emenda RN-107 → `RF-13`; segmentação RN-16 →
> `RF-09`. Rastreado em [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] §5.

## Bloco 8 — User Stories + Critérios de Aceite
Padrão Dado/Quando/Então; cada CA amarra a uma RN.

### US-01 — Validação de briefing pelo CS *(RF-03)*
1. **CA-01.1** — *Dado* briefing pré-preenchido, *Quando* o CS marca
   "Confirmado", *Então* a análise avança. → **RN-01**
2. **CA-01.2** — *Dado* briefing pendente, *Quando* o cliente não responde,
   *Então* a análise **não** avança (sem prazo automático). → **RN-01**
3. **CA-01.3** — *Dado* 2 rejeições prévias, *Quando* ocorre a 3ª, *Então*
   escala ao Gerente. → **RN-06**

### US-02 — Classificação de performance *(RF-11, RF-12)*
1. **CA-02.1** — *Dado* índice **0,80**, *Então* status **Bom**. → **RN-19**
2. **CA-02.2** — *Dado* posição **10,5**, *Então* CTR **1%** (sem
   arredondar). → **RN-16**
3. **CA-02.3** — *Dado* status **Bom**, *Então* cadência **trimestral**. → **RN-02**

### US-03 — Travamento condicional da auditoria *(RF-15)*
1. **CA-03.1** — *Dado* Dim 1 crítica (score **<50%**), *Então* 2–10
   **bloqueadas**. → **RN-88**
2. **CA-03.2** — *Dado* Dim 1 OK e Dim 5 crítica, *Então* 2–10 rodam em
   **paralelo**. → **RN-88**

### US-04 — Alerta de lead zerado *(RF-24)*
1. **CA-04.1** — *Dado* tráfego>0 e leads=0, *Então* **alerta extremo**
   imediato. → **RN-107** *(usa o total multicanal)*
2. **CA-04.2** — *Dado* total multicanal=0 por **7 dias**, *Então* alerta
   EXTREMO. → **RN-107**
3. **CA-04.3** — *Dado* projeto **sem formulário**, *Então* o cenário de
   falha de formulário **não** dispara. → **RN-109**

### US-05 — Exportação para o Salesforce *(RF-28, RF-29)*
1. **CA-05.1** — *Dado* ação **não aprovada**, *Então* **não** é exportada.
   → **RN-75**
2. **CA-05.2** — *Dado* ação aprovada, *Então* trafega **só título e
   escopo**, agrupada por área. → **RN-76, RN-78**
3. **CA-05.3** — *Dado* geração de conteúdo necessária, *Quando* o analista
   não clicou "Gerar", *Então* nada é gerado no MPI Plus (Gate 1). → **RN-100**

### US-06 — Validação automática pós-execução *(RF-31, RF-32)*
1. **CA-06.1** — *Dado* ação marcada concluída, *Quando* aciono "Validar",
   *Então* o sistema relê o site e compara estado anterior×atual. → **RN-81**
2. **CA-06.2** — *Dado* validação **reprovada**, *Então* volta à fila com
   notas. → **RN-81**
3. **CA-06.3** — *Dado* validação **aprovada (OK Final)**, *Então* inicia a
   maturação de **60 dias**. → **RN-27, RN-79**

### US-07 — [NOVO] Portão de Diferenciação Real *(RF-54)*
> **Como** sistema de geração de conteúdo, **quero** checar sinais de
> diferenciação real antes de gerar página/artigo por combinação, **para**
> não produzir o padrão de doorway page punido pelos core updates 2026.
1. **CA-07.1** — *Dado* combinação palavra×região×tipo sem dado local
   específico, prova social ou resposta a pergunta real, *Quando* o Gate 1
   é avaliado, *Então* a ação vira "recomendar cluster de suporte" em vez
   de "gerar página isolada". → **RN-SGA-05**
2. **CA-07.2** — *Dado* geração aprovada (página ou artigo), *Então* o
   asset recebe `nivel_diferenciacao` (alto/médio/baixo). → **RN-SGA-05**
3. **CA-07.3** — *Dado* `taxa_diferenciacao_real` abaixo do esperado,
   *Então* é reportada como alerta de risco no Score de Saúde (Dim 2). →
   **RN-SGA-05**

> ⚠️ **Gaps expostos ao escrever os CA** (viram decisão/backlog, não
> surpresa em produção): (a) sem CA de "briefing/validação parada há X
> dias" — falta regra de envelhecimento; (b) sem CA de desempate quando
> duas dimensões recomendam ações conflitantes; (c) sem CA de desempate
> quando IA e analista divergem na validação; (d) demais RF (07–10, 13–26,
> 33–53) seguem o mesmo padrão, mas ainda não têm US/CA escritos — 1 US por
> RF é trabalho da próxima rodada.

## Bloco 9 — Fluxos (happy path + exceções)
```
RF-00 elegibilidade → Fase 1 briefing (CS valida) + mapeia cluster (RF-47)
 → Fase 2 Motor (índice/status)
 → Fase 3 Auditoria (Dim 1 gate → 2–10 paralelas, incl. RF-48–53)
 → Parecer
 → Fase 4 fila → aprovação → [conteúdo? Gate 1: Portão de Diferenciação
   Real, RF-54, checa antes de acionar] → Salesforce → execução →
   validação IA → maturação
```
**Faseamento interno da Auditoria (mitiga o risco "casa vazia — os
prompts"):** lançar com **Dim 1 + todas as determinísticas (4,5,6,7,9) +
Dim 10 (leads) + as sub-checks novas RF-47–53** já no MVP (✅), e **Dim 2
(comparação SERP por IA), 3, 8** como **fast-follow (🕒)** assim que os
prompts tiverem golden-set validado.

Exceções já mapeadas: Hard Stop (RN-64), retry de site fora (RN-39/40),
sobreposição do Sentinela ao bloqueio (RN-94), execução parcial (RN-46).
*Gap:* faltam **máquinas de estado** formais.

## Bloco 10 — Dependências / integrações
16 ferramentas externas + Salesforce + MPI Plus, com divisão de papéis
explícita.

**Bloqueadores de build (fechar antes de codar):**
- **7 questões de integração** — Q18-21 (Salesforce) e Q27-30 (MPI Plus) →
  [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]].
- **Cotas não dimensionadas** — PageSpeed 400/dia, 6 contas GSC (teto real
  de cobertura para ~2.500 clientes, achado F-14/F-32), SemRush →
  [[05-Backlog/gm-dimensionamento-cotas-ferramentas-externas]].
- MPI Plus é **SPOF** reconhecido — sem fallback além de aguardar relatório.
- **WhatsApp Business API (webhook de status)** — necessária para
  RN-123/RN-124; hoje só existe o WhatsApp API de notificação (RN-51),
  distinto. Não implementada — proposta.

## Bloco 11 — Premissas e Riscos
| Premissa / Risco | Prob. | Mitigação | Pendência |
|---|---|---|---|
| Números de negócio (70%, 50%, 40/40/20, 5%) por julgamento de especialista | Alta | Registrar como premissa explícita, calibrar depois | [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]] |
| **Doorway/scaled content ativo na carteira atual (F-39)** | Alta — risco já materializado nos core updates 2026, caso real (emtecorp) | Cluster Wrapping + Portão de Diferenciação Real já desenhados (RF-47/51/54) | Falta auditoria retroativa da carteira — Frente Z1, [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] Track F, sem dependência, pode rodar já |
| "Casa vazia — os prompts" (conteúdo fino dos agentes) | Alta | Faseamento da auditoria (Bloco 9) + golden-set antes de produção | [[05-Backlog/gm-desenho-fino-prompts-agentes]] |
| Circularidade do `ctr_estimado` (F-08/F-31) — índice de tráfego pode melhorar no mês em que o SEO piora | Média | Baseline defasada (janela saudável trimestral) | [[04-Decisões/adr-camada-calibracao-continua]] |
| Dado legado (Scout/Kaique) | Alta | Força-tarefa | sem prazo — definir |
| MPI Plus indisponível | Média | Cache + ações pendentes | duração máx. de cache indefinida |
| Concentração de papéis (CS sozinho; Analista aprova+valida) | Média | Reavaliar segregação | [[05-Backlog/gm-segregacao-funcoes-pontos-controle]] |

## Bloco 12 — Rollout / Go-to-market (proposto)
1. **Frente Z1** (auditoria de quase-duplicatas na carteira atual, zero
   dependência) — recomendado rodar **antes ou em paralelo** ao piloto,
   dado que é o risco de maior probabilidade×impacto do produto.
2. **Piloto** com 1 BU / subconjunto da carteira, automação parametrizável
   por cliente (RN-66), avanço sem validação exigindo aprovação admin.
3. **Fast-follow** das dimensões de IA (2, 3, 8) conforme os prompts passam
   no golden-set.
4. **Expansão** para 100% da carteira após estabilizar cota de ferramentas
   e a integração Salesforce/MPI Plus.
5. Comunicação interna (analistas/CS/gerência) — *a definir*.

## Bloco 13 — Glossário / Anexos
- **Glossário:** [[00-Glossario]] (RN, NFR, SPOF, GEO/AEO, silo, M3, Gate
  1/2, Cluster Wrapping, Portão de Diferenciação Real, Camada de
  Calibração Contínua…).
- **Anexos a produzir:** protótipos das 11 telas (incl. onde
  `taxa_diferenciacao_real`/Dim 11 aparecem — gap ainda não decidido, ver
  [[03-Produtos/growth-machine]] › "Gap de amarração"); contrato de prompt
  + schema JSON dos agentes; ERD e máquinas de estado.

---

## Alinhamento com boas práticas do Google (2026) × estrutura interna

> Checagem explícita pedida ao estruturar este PRD: cruza os **sistemas do
> Google nomeados explicitamente** (princípio 6 de
> [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]) e a análise
> completa por dimensão em
> [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]]
> contra a estrutura de RN/Dimensão deste PRD — não é só "está mencionado?",
> é "o mecanismo interno de fato produz o comportamento que o Google
> recompensa/pune?".

### Os 3 sistemas nomeados — veredito por sistema

| Sistema Google | O que exige | Situação no GM hoje | Mecanismo interno | Veredito |
|---|---|---|---|---|
| **Helpful Content System** | Qualidade do domínio inteiro é avaliada, não só página a página; conteúdo fraco acumulado arrasta o resto | RN-84 **proibia** sugerir remoção — contradição direta identificada e já na fila #2 de correção | Ajuste RN-84 (bloqueio → sugestão de poda com scoring) | 🟡 **Em correção** — decisão tomada, implementação pendente |
| **E-E-A-T (reforçado em YMYL)** | Autor transparente, fonte crível, marca forte, insight original | Só existe **no prompt de geração** (MPI Plus); auditoria estrutural on-page não existia até esta rodada | **RF-50 / RN-SGA-07** (Dim 2E) — nesta consolidação, formalizada como RF ✅ MVP | 🟡 **Desenhado e no MVP**, falta build |
| **Scaled Content Abuse / Doorway Pages** | Não gerar página em massa por combinação palavra×região×tipo sem valor/diferenciação real; sites flagrados perdem 50–80% de tráfego em semanas | **O método de geração do produto era, textualmente, o exemplo que o Google usa para definir o padrão punido** (achado F-39, confirmado por 2 análises independentes) | **RF-47/51/54 (Cluster Wrapping + Portão de Diferenciação Real)** — antídoto desenhado nesta rodada | 🔴→🟡 **Risco real mitigado no desenho, não confirmado em produção** — falta a auditoria retroativa da carteira (Frente Z1) para saber a exposição real hoje |

**Leitura direta:** dos 3 sistemas nomeados, o produto está **desenhado**
para os 3, mas **implementado** para nenhum ainda — os 3 dependem de RFs
que entraram nesta consolidação (RF-50, RF-47/51/54) ou de um ajuste ainda
não feito (RN-84). O item de maior urgência é o terceiro: é risco ativo já
em produção, não só lacuna de auditoria.

### Cobertura por pilar (condensado de
[[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]])

| Pilar | Itens ✅ cobertos | Itens 🟡 parciais/desenhados nesta rodada | Itens 🔴 ainda sem RN/mecanismo |
|---|---|---|---|
| **SEO** | Intenção de busca (Dim 1/2), schema por template (Dim 6, RN-117) | Anti-doorway (RF-47/51/54), poda (RN-84 ajuste), E-E-A-T on-page (RF-50), meta/title (RF-48), PDF→HTML (RF-53), CWV real (RN-07 ajuste) | Autoridade/backlink propositiva (RN-SGA-09, Fase 2), conteúdo original/information gain (RN-SGA-08, Fase 2), log de crawler real (RN-SGA-12, Fase 2) |
| **GEO** | Controle de crawler de IA (RF-52) | — | Medição de citação/SoV (Dimensão 11, Fase 2), entidade/`sameAs` (RN-SGA-14, Fase 2), presença off-site (sem RN ainda), tráfego de origem IA (RN-SGA-11, Fase 2), pilares agênticos (RN-SGA-15, Fase 2) |
| **AEO** | — | Priorização por nicho (RF-49) | Resposta única/inequívoca (RN-SGA-02, Fase 2), extrabilidade (RN-SGA-01, Fase 2), medir "resposta escolhida" em voz (sem RN, especulativo) |

**Leitura direta:** SEO é o pilar mais coberto (esperado — é onde o
produto nasceu), GEO tem 1 item novo coberto (crawler de IA) mas a peça
central (medição/Dimensão 11) segue Fase 2, e AEO é o pilar mais atrasado
dos três — só 1 item endereçado nesta consolidação.

### Veredito final desta checagem
1. **Nenhuma contradição nova** foi introduzida ao estruturar este PRD — os
   mecanismos novos (Cluster Wrapping, Portão de Diferenciação Real,
   RN-SGA-*) se encaixam nos gates já existentes (RN-88, RN-100 Gate 1,
   RN-96), confirmado em [[03-Produtos/growth-machine/validacao-fluxos-principios]].
2. **O risco mais grave (doorway) está desenhado, não resolvido** — o
   antídoto existe no PRD (RF-47/51/54) mas ninguém ainda mediu quantas
   páginas da carteira atual já se encaixam no padrão punido. Frente Z1 é
   pré-requisito para saber o tamanho real do problema antes do piloto.
3. **O loop de medição para GEO/AEO (princípio 5) continua quebrado** até a
   Dimensão 11 sair da Fase 2 — nenhuma reestruturação documental resolve
   isso; só a integração com o [[03-Produtos/ideal-tracker]] resolve.
4. Estrutura interna (RN/Dimensão) está **pronta para receber** as 16
   `RN-SGA-*` conforme forem implementadas — não há mais nenhuma capability
   Google-relevante sem um lugar definido no catálogo/dimensão.

---

## Estado de fechamento deste PRD
> Honestidade explícita — não é uma "declaração de pronto".

**✅ Fechado:**
- Decisões-gate G1–G9 (pesos, numeração RN, cluster×concatenação, fluxo de
  keywords, fonte de posicionamento, North Star, faseamento, ADR cluster,
  numeração do PRD).
- Catálogo de RN reconciliado, sem canibalização (146 RNs, `RN-EST-*`/
  `RN-SGA-*` com Origem/Prioridade).
- Estrutura SEO/GEO/AEO incorporada às dimensões, com RF própria por item
  MVP (RF-47 a RF-54, nesta consolidação).
- Validação de fluxo × princípios sem contradição lógica
  ([[03-Produtos/growth-machine/validacao-fluxos-principios]]).
- Checagem de aderência a boas práticas Google 2026 (seção acima).

**🕒 Aberto — não bloqueia leitura deste PRD, bloqueia codar:**
- 13 blocos: faltam Bloco 2 (North Star confirmado com PO), Bloco 4
  (persona CS dedicada), Bloco 6 (gaps de NFR), 1 US+CA por RF (hoje só
  fluxos críticos), Bloco 9 (máquinas de estado formais).
- **7 questões de integração** Salesforce/MPI Plus (Bloco 10).
- **Golden-set dos prompts** dos agentes de IA (risco "casa vazia").
- **ERD** + contratos de API.
- **Frente Z1** — auditoria da carteira atual por doorway/quase-duplicatas
  (recomendado antes do piloto, sem dependência técnica).
- Track F completo — ver [[03-Produtos/growth-machine/plano-fechamento-prd-v2]].

## Notas relacionadas
- [[03-Produtos/growth-machine/prd-v2-mvp]] — rascunho de consolidação que originou este arquivo
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — fonte única das RNs
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — 6 princípios + fila de prioridade SEO/GEO/AEO
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] — origem das RN-SGA-*
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] — origem da checagem Google 2026
- [[03-Produtos/growth-machine/validacao-fluxos-principios]] — validação de fluxo × princípios
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — tracker de fechamento (Track A-F)
- [[04-Decisões/adr-camada-calibracao-continua]] · [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]
- [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
