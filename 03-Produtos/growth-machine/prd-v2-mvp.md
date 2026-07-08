---
tipo: produto
status: rascunho
criado: 2026-07-08
ultima-revisao: 2026-07-08
versao-doc: "v2.0-mvp (consolidação do cofre)"
consolida:
  - "Drive — PRD_Growth_Machine_v1_9_14.md"
  - "Drive — revisao-critica-prd-growth-machine.md (29 achados, Will)"
  - "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
  - "[[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]]"
tags: [growth-machine, prd, v2, mvp, requisitos-funcionais, user-story, rn, seo, geo, aeo]
---

# PRD Growth Machine — v2.0 (MVP)

> **O que é esta nota:** a consolidação do cofre do PRD do Growth Machine no
> formato de PRD ideal (13 blocos), reconciliando o PRD v1.9.14 do Drive, a
> revisão crítica do Will (29 achados) e toda a análise já feita no cofre —
> pronta para iniciar um MVP. **Não é a fonte de verdade formal fora do
> cofre** (o PRD oficial vive no Drive); é a elaboração do PO para chegar a
> uma documentação aderente e sem lacunas antes do build.
>
> **Base e plano:** [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]].
> **RNs (fonte única):** [[03-Produtos/growth-machine/catalogo-regras-negocio]].
> **Padrão de User Story/CA:** [[04-Decisões/padrao-historia-jira]].

## Como ler este documento (anti-canibalização documental)
Para que RN e PRD **não se canibalizem**, cada tipo de conteúdo tem uma
única casa:

| Artefato | Diz | Mora em | Aqui no PRD |
|---|---|---|---|
| **RF** | O quê o sistema faz | Este PRD (Bloco 5) | Definido |
| **RN** | A restrição/lógica que governa | [[03-Produtos/growth-machine/catalogo-regras-negocio]] | Só **referenciado** por ID |
| **NFR** | Quão bem | Este PRD (Bloco 6) | Definido |
| **CA** | Como se testa | Este PRD (Bloco 8) | Amarra CA→RN |

Regra de ouro: **RF ≠ RN ≠ NFR ≠ CA**. Se um parágrafo estiver fazendo
dois papéis, ele está no lugar errado.

## Tabela de versões
| Versão | Data | Autor | Mudança |
|---|---|---|---|
| v2.0-mvp (cofre) | 2026-07-08 | PO (via cofre) | Consolidação nos 13 blocos + RF numerados + User Stories/CA + reconciliação de RNs. **Pendência: confirmar numeração oficial (v1.0 vs. v1.9.14) com quem gerencia o PRD do Drive** — ver [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]]. |

---

## Bloco 1 — Contexto / Problema
2.500 clientes ativos em 3 empresas (Ideal Marketing · Busca Cliente · MPI
Solutions). Cada analista de Growth gasta **~90h/mês** diagnosticando no
olho (Search Console, Excel, PageSpeed, SendGrid, um a um). O método MPI é
eficaz mas vive na cabeça de sêniors — some quando o sênior sai, erra com
analista novo, e não há headcount para diagnosticar todo mês.

**Consequências hoje:** briefing desatualizado (<20% da carteira), lead
zerado descoberto por acaso (cliente liga furioso), upsell perdido,
~10 analistas de capacidade parados em triagem manual.

## Bloco 2 — Objetivo + Métricas de sucesso
**North Star (proposta):** **% da carteira ativa diagnosticada dentro da
cadência correta, com fila de ações aprovada** — captura o valor central
(cobertura + ação, não só análise). *Confirmar com o PO.*

**Métricas de apoio (do PRD I.3):**
| Métrica | Hoje | Meta MVP |
|---|---|---|
| Horas de diagnóstico/analista/mês | ~90h | <10h |
| Cobertura da carteira | ~60 clientes/analista | 100% da carteira ativa |
| Tempo para detectar lead zerado | por acaso | <7 dias (alerta) |
| Taxa de ações aceitas sem alteração | N/A | >70% |
| Briefings atualizados | <20% | >80% em 6 meses |

> Lacuna herdada: as frentes GEO/AEO **não têm meta numérica** — coerente
> com o MVP (medição de GEO = Fase 2, ver Bloco 3).

## Bloco 3 — Escopo (dentro / fora)

**Dentro do MVP:**
- Fases 1–4 completas + Módulo Sentinela.
- As 10 dimensões de auditoria (ver Bloco 9 para faseamento interno proposto).
- Governança humana (RN-47) e dois gates de geração delegada (RN-100).
- GEO/AEO **como checklist técnico/semântico** (Dim 2C, RN-82, schemas).

**Fora do MVP (decisão explícita):**
- **Medição real de GEO/AEO** (citação em LLM, Share of Voice, "sou a
  resposta escolhida") → **Fase 2** — decisão do PO formalizada no achado
  **F-28** ([[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]]).
- Cliente fora do MPI Plus (RN-108) — entra no MPI Plus primeiro.
- Site fora do padrão MPI (RN-36).
- GM **não publica nada** no site do cliente; a automação para na geração
  da fila de ações. Execução é manual, via Salesforce.
- Os 11 itens da fila SEO/GEO/AEO ([[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]])
  são **roadmap pós-MVP**, exceto onde já são princípio (Bloco 4).

## Bloco 4 — Personas / público
| Persona | Papel no fluxo | Acesso |
|---|---|---|
| **Analista de Growth** | Aprova a fila de ações e valida a execução (RN-49 — acumula os dois papéis; persona "Revisor" extinta) | GM interno |
| **CS (Customer Success)** | Valida o briefing com o cliente (RN-01) | GM interno |
| **Gerente / Supervisor** | Recebe escalonamentos (RN-06, RN-45) e visão consolidada (Tela 2) | GM interno |
| **Front-end (executor)** | Executa as ações e dá baixa no Salesforce | Salesforce |
| **Cliente** | Aprova estudo/conteúdo/imagem **no MPI Plus**, nunca no GM (RN-104) | MPI Plus |

> Lacuna herdada (backlog): o CS não tem tela/visão própria mapeada
> (fila de briefings pendentes) — [[03-Produtos/growth-machine/avaliacao-fluxo]].

## Bloco 5 — Requisitos Funcionais (RF)
Cada RF é uma capacidade; a coluna RN aponta a restrição que o governa
(a regra mora no catálogo). Coluna **MVP**: ✅ dentro · 🕒 fast-follow ·
⏭️ Fase 2.

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
| **RF-09** | Converter posição média em CTR por faixa, sem arredondamento | RN-16 | ✅ |
| **RF-10** | Calcular maturidade por interpolação linear e aplicar teto de crescimento | RN-17 | ✅ |
| **RF-11** | Calcular o Índice de Performance com pesos parametrizáveis (default 40/40/20) | RN-18 | ✅ |
| **RF-12** | Classificar em Ruim/Regular/Bom/Ótimo (thresholds inclusivos) e definir cadência | RN-19, RN-02 | ✅ |
| **RF-13** | Usar `trafego_real` só orgânico e `leads_real` multicanal | RN-86, RN-107, RN-110 | ✅ |
| **RF-14** | Alertar "sem estudo válido" quando `volume_total = 0` | RN-20 | ✅ |

### Fase 3 — Auditoria em 10 Dimensões
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-15** | Interromper a auditoria **apenas** quando a Dim 1 for crítica; senão, rodar 2–10 em paralelo | RN-88 | ✅ |
| **RF-16** | Calcular o Score de Saúde Técnica determinístico (0–100) | RN-96 | ✅ |
| **RF-17** | Rodar Dim 4, 5, 6, 7, 9 como checagem determinística, sem IA | RN-99, RN-115–120 | ✅ |
| **RF-18** | Dim 1 — auditar o estudo contra briefing/metodologia/pacote/páginas reais | RN-112 | ✅ |
| **RF-19** | Dim 2 — extrair padrão SERP e comparar cobertura por página MPI (inclui 2C GEO/AEO) | RN-113 | 🕒 |
| **RF-20** | Dim 3 — auditar silo/linkagem contra o estudo aprovado | RN-114 | 🕒 |
| **RF-21** | Dim 6 — validar schemas e **bloquear** schema fabricado (reviews/preços/FAQ não verificáveis) | RN-117 | ✅ |
| **RF-22** | Dim 7 — validar sitemap/robots + presença de AI Instructions/LLM.txt | RN-118, RN-82 | ✅ |
| **RF-23** | Dim 8 — consolidar GSC + backlinks; disavow sempre com revisão humana | RN-119 | 🕒 |
| **RF-24** | Dim 10 — auditar captação/entrega/qualidade de leads e disparar alertas A/B/C/D | RN-121, RN-107, RN-109 | ✅ |
| **RF-25** | Gerar o Parecer Consolidado por IA (1x/análise), mantendo Índice + Score + dimensões separados | RN-97 | ✅ |
| **RF-26** | Rodar a Camada de Tradução de Diagnóstico (traduz/enriquece, não detecta) | RN-89 | ✅ |

### Fase 4 — Aprovação, Execução e Validação
| RF | O sistema deve… | RN | MVP |
|---|---|---|---|
| **RF-27** | Priorizar e apresentar a fila de ações para aprovação do analista | RN-44, RN-47 | ✅ |
| **RF-28** | Acionar a geração no MPI Plus só após clique (Gate 1) + revisar o asset (Gate 2) | RN-100 | ✅ |
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
Catalogados a partir do PRD (Parte III) — antes só citados, agora fixados:
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

## Bloco 7 — Regras de Negócio (RN) — referência + reconciliação
As 122 RNs **não são recopiadas aqui** (fonte única no catálogo). Este bloco
registra só o que a v2 **muda/reconcilia** para eliminar canibalização:

| Ação de reconciliação | RNs | Origem do achado |
|---|---|---|
| **Marcar `[SUPERSEDIDA]`** — lead só formulário → multicanal | RN-21, RN-22, RN-23 → RN-107/RN-121 | F-05 (Will) |
| **Marcar `[SUPERSEDIDA]`** — contradiz réguas por dimensão | RN-29 | F-05 |
| **Marcar `[SUPERSEDIDA]`** — contradiz travamento condicional | RN-32 → RN-88 | F-05 |
| **Resolver ambiguidade de threshold Dim 1** — adotar **<50%** (régua detalhada) como default único; corrigir a tabela | RN-88 (gate) | F-03 |
| **Remover resíduo Bright Data** — posicionamento vem só do relatório mensal | RN-64, RN-105 | F-01 |
| **Adicionar colunas Origem + Prioridade** ao catálogo | todas | [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] |
| **Tirar o "como" de RN de implementação** (ex: RN-99 não deve fixar GPT-5 no texto, já que é parametrizável) | RN-93, RN-99 | idem |

> Estas mudanças devem ser aplicadas **no catálogo**, não duplicadas aqui —
> este bloco é só o registro da decisão.

## Bloco 8 — User Stories + Critérios de Aceite
Padrão Dado/Quando/Então; cada CA amarra a uma RN. Abaixo, as histórias
dos **fluxos críticos do MVP** (formato validado em
[[03-Produtos/growth-machine/documentacao-v2-rf-e-user-stories]]). As demais
RF seguem o mesmo padrão, 1 US por RF — a expandir na próxima rodada.

### US-01 — Validação de briefing pelo CS *(RF-03)*
> **Como** CS, **quero** validar o briefing antes de a análise seguir,
> **para** que nenhum diagnóstico rode sobre dado não confirmado.
1. **CA-01.1** — *Dado* briefing pré-preenchido, *Quando* o CS marca
   "Confirmado", *Então* a análise avança. → **RN-01**
2. **CA-01.2** — *Dado* briefing pendente, *Quando* o cliente não responde,
   *Então* a análise **não** avança (sem prazo automático). → **RN-01**
3. **CA-01.3** — *Dado* 2 rejeições prévias, *Quando* ocorre a 3ª, *Então*
   escala ao Gerente. → **RN-06**

### US-02 — Classificação de performance *(RF-11, RF-12)*
> **Como** analista, **quero** classificação por fórmula auditável, **para**
> priorizar a carteira sem julgamento manual.
1. **CA-02.1** — *Dado* índice **0,80**, *Então* status **Bom**. → **RN-19**
2. **CA-02.2** — *Dado* posição **10,5**, *Então* CTR **1%** (sem
   arredondar). → **RN-16**
3. **CA-02.3** — *Dado* status **Bom**, *Então* cadência **trimestral**. → **RN-02**

### US-03 — Travamento condicional da auditoria *(RF-15)*
> **Como** analista, **quero** que só um estudo crítico trave a auditoria,
> **para** não segurar 9 dimensões independentes.
1. **CA-03.1** — *Dado* Dim 1 crítica (score **<50%**), *Então* 2–10
   **bloqueadas**. → **RN-88** *(threshold reconciliado, Bloco 7)*
2. **CA-03.2** — *Dado* Dim 1 OK e Dim 5 crítica, *Então* 2–10 rodam em
   **paralelo**. → **RN-88**

### US-04 — Alerta de lead zerado *(RF-24)*
> **Como** analista, **quero** ser alertado quando um cliente com tráfego
> para de gerar leads, **para** agir antes de o cliente reclamar.
1. **CA-04.1** — *Dado* tráfego>0 e leads=0, *Então* **alerta extremo**
   imediato. → **RN-21** *(nota: RN-21 supersedida em texto por RN-107
   multicanal — o alerta usa o total multicanal, Bloco 7)*
2. **CA-04.2** — *Dado* total multicanal=0 por **7 dias**, *Então* alerta
   EXTREMO. → **RN-107**
3. **CA-04.3** — *Dado* projeto **sem formulário**, *Quando* checa cenário
   de falha de formulário, *Então* **não** dispara (condicionado à
   existência). → **RN-109**

### US-05 — Exportação para o Salesforce *(RF-28, RF-29)*
> **Como** analista, **quero** exportar só o que aprovei, **para** o
> Salesforce ser fonte única de execução sem vazar detalhe técnico.
1. **CA-05.1** — *Dado* ação **não aprovada**, *Então* **não** é exportada.
   → **RN-75**
2. **CA-05.2** — *Dado* ação aprovada, *Então* trafega **só título e
   escopo**, agrupada por área. → **RN-76, RN-78**
3. **CA-05.3** — *Dado* geração de conteúdo necessária, *Quando* o analista
   não clicou "Gerar", *Então* nada é gerado no MPI Plus (Gate 1). → **RN-100**

### US-06 — Validação automática pós-execução *(RF-31, RF-32)*
> **Como** analista, **quero** que o sistema confira a execução relendo o
> site, **para** não confiar cegamente no "concluído" do Salesforce.
1. **CA-06.1** — *Dado* ação marcada concluída, *Quando* aciono "Validar",
   *Então* o sistema relê o site e compara estado anterior×atual. → **RN-81**
2. **CA-06.2** — *Dado* validação **reprovada**, *Então* volta à fila com
   notas. → **RN-81**
3. **CA-06.3** — *Dado* validação **aprovada (OK Final)**, *Então* inicia a
   maturação de **60 dias**. → **RN-27, RN-79**

> ⚠️ **Gaps expostos ao escrever os CA** (viram decisão/backlog, não
> surpresa em produção): (a) sem CA de "briefing/validação parada há X
> dias" — falta regra de envelhecimento
> ([[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]]);
> (b) sem CA de desempate quando duas dimensões recomendam ações
> conflitantes ([[05-Backlog/gm-criterio-desempate-fronteiras-componentes]]);
> (c) sem CA de desempate quando IA e analista divergem na validação.

## Bloco 9 — Fluxos (happy path + exceções)
Fluxo macro (reusa o funcionamento validado):
```
RF-00 elegibilidade → Fase 1 briefing (CS valida) → Fase 2 Motor (índice/
status) → Fase 3 Auditoria (Dim 1 gate → 2–10 paralelas) → Parecer →
Fase 4 fila → aprovação → Salesforce → execução → validação IA → maturação
```
**Faseamento interno da Auditoria proposto para o MVP** (mitiga o risco "casa
vazia — os prompts"): lançar com **Dim 1 + todas as determinísticas (4,5,6,7,9)
+ Dim 10 (leads)** já no MVP (✅), e **Dim 2, 3, 8** como **fast-follow (🕒)**
assim que os prompts tiverem golden-set validado. Assim o MVP não fica
refém dos 9 prompts finos ao mesmo tempo. *Decisão a confirmar com o PO.*

Exceções já mapeadas: Hard Stop (RN-64), retry de site fora (RN-39/40),
sobreposição do Sentinela ao bloqueio (RN-94), execução parcial (RN-46).
*Gap:* faltam **máquinas de estado** formais (F-21/F-22 do Will).

## Bloco 10 — Dependências / integrações
16 ferramentas externas + Salesforce + MPI Plus, com divisão de papéis
explícita (ver [[03-Produtos/growth-machine]] › Ferramentas externas).
**Bloqueadores de build (fechar antes de codar):**
- **7 questões de integração** — Q18-21 (Salesforce) e Q27-30 (MPI Plus) →
  [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]].
- **Cotas não dimensionadas** — PageSpeed 400/dia, 6 contas GSC, SemRush →
  [[05-Backlog/gm-dimensionamento-cotas-ferramentas-externas]].
- MPI Plus é **SPOF** reconhecido — sem fallback além de aguardar relatório.

## Bloco 11 — Premissas e Riscos
| Premissa / Risco | Prob. | Mitigação | Pendência |
|---|---|---|---|
| Números de negócio (70%, 50%, 40/40/20, 5%) por julgamento de especialista | Alta | Registrar como premissa explícita, calibrar depois | [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]] |
| "Casa vazia — os prompts" (conteúdo fino dos agentes) | Alta | Faseamento da auditoria (Bloco 9) + golden-set antes de produção | [[05-Backlog/gm-desenho-fino-prompts-agentes]] |
| Dado legado (Scout/Kaique) | Alta | Força-tarefa | **sem prazo — definir** |
| MPI Plus indisponível | Média | Cache + ações pendentes | **duração máx. de cache indefinida** |
| Concentração de papéis (CS sozinho; Analista aprova+valida) | Média | Reavaliar segregação | [[05-Backlog/gm-segregacao-funcoes-pontos-controle]] |

## Bloco 12 — Rollout / Go-to-market (proposto)
1. **Piloto** com 1 BU / subconjunto da carteira, com a automação em modo
   parametrizável por cliente (RN-66) e avanço sem validação exigindo
   aprovação admin.
2. **Fast-follow** das dimensões de IA (2, 3, 8) conforme os prompts passam
   no golden-set.
3. **Expansão** para 100% da carteira após estabilizar cota de ferramentas
   e a integração Salesforce/MPI Plus.
4. Comunicação interna (analistas/CS/gerência) — *a definir*.

> Bloco **novo** (ausente no PRD atual). Faseamento e critérios de saída de
> cada etapa a fechar com o PO.

## Bloco 13 — Glossário / Anexos
- **Glossário:** [[00-Glossario]] (RN, NFR, SPOF, GEO/AEO, silo, M3, Gate 1/2…).
- **Anexos a produzir:** protótipos das 11 telas; contrato de prompt +
  schema JSON dos agentes; ERD e máquinas de estado (F-21–F-24).

---

## Onde entram SEO / GEO / AEO neste PRD (e o que fica para a sequência)
**Já incorporado ao MVP como princípio/checklist** (não é medição):
- **6 princípios-núcleo** transversais guiam o desenho (intenção real,
  anti-canibalização, E-E-A-T, governança humana, loop de mensuração,
  alinhamento a sistemas do Google) —
  [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]].
- GEO/AEO técnico: Dim 2C, RN-82 (AI Instructions/LLM.txt), schemas (Dim 6).

**Fica para a sequência (as "estruturações e divisões" que você citou):**
inserir as frentes SEO/GEO/AEO em profundidade — as divisões por pilar
dentro de cada dimensão, a fila única de 11 oportunidades e a decisão de
GEO virar ou não pilar de primeira classe (peso próprio no Índice). Base
pronta em [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]]
e [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]].

## Checklist "pronto para dev" — estado do MVP
- [x] RF numerados (Bloco 5) — **feito**
- [~] Cada RN com CA — **fluxos críticos feitos**; expandir 1 US por RF
- [x] Escopo dentro/fora explícito (Bloco 3)
- [~] Métricas — North Star **proposta**, confirmar
- [x] Fluxos de exceção mapeados
- [ ] Dependências — **7 questões de integração abertas** (bloqueador)
- [ ] Prompts dos agentes com golden-set (bloqueador — mitigado pelo faseamento)

## Notas relacionadas
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] — plano dos 13 blocos e auditoria de RN
- [[03-Produtos/growth-machine/documentacao-v2-rf-e-user-stories]] — demonstração de formato (absorvida aqui)
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — fonte única das RNs
- [[03-Produtos/growth-machine/avaliacao-fluxo]] — crítica fase a fase
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] — frente SEO/GEO/AEO (sequência)
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — 6 princípios + fila única
- [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]] — reconciliação (F-01/03/05/28)
- [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
