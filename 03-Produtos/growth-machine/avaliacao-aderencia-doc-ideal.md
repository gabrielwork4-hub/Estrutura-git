---
tipo: produto
status: vivo
criado: 2026-07-08
ultima-revisao: 2026-07-08
tags: [growth-machine, prd, avaliacao, aderencia, rn, user-story, documentacao-ideal]
---

# Avaliação de Aderência à Documentação Ideal — Growth Machine

> Documento-ponte entre a análise crítica já feita ([[03-Produtos/growth-machine/avaliacao-fluxo]])
> e a **nova documentação** que queremos projetar (aderente e mais próxima
> do produto ideal). Aqui a lente é diferente das notas anteriores: não é
> "o fluxo está certo?", é **"a documentação que temos hoje cobre os 13
> blocos de um PRD ideal, e as 122 RNs passam nos critérios de qualidade
> de uma boa RN?"**. Cruza toda a vault + os arquivos-padrão do fluxo no
> Drive, para nada se perder. Serve de base direta para escrever a v2 do
> PRD com o PO.

## Método e escopo do cruzamento
Foram cruzadas **todas** as fontes existentes, em dois lugares:

- **Vault (cofre):** [[03-Produtos/growth-machine]] (produto + RNs-chave),
  [[03-Produtos/growth-machine/catalogo-regras-negocio]] (122 RNs),
  [[03-Produtos/growth-machine/avaliacao-fluxo]] (crítica fase a fase),
  [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]],
  [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]],
  [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]],
  [[03-Produtos/growth-machine/briefing-lideranca-seo-geo-aeo]],
  [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]],
  [[03-Produtos/growth-machine/cheat-sheet]] e
  [[03-Produtos/growth-machine/prep-reuniao-po-lead]].
- **Drive (pasta do projeto Growth Machine):** `PRD_Growth_Machine_v1_9_14.md`
  (fonte primária, 238 KB), `revisao-critica-prd-growth-machine.md` (29
  achados F-01 a F-29, com decisões do PO), `Kickoff - Growth Machine` e
  `REUNIÕES - AUTOMAÇÃO` (transcrições de origem, mar/2026), e a subpasta
  **ADRs** (hoje **vazia** — decisões de arquitetura ainda não formalizadas).

**Nada foi encontrado fora disso** para o Growth Machine: as 13 outras
pastas de projeto do Drive não têm material de GM (ver
[[03-Produtos/mapa-dependencia-produtos]]). O que segue é a leitura
consolidada dessas fontes contra o padrão de PRD ideal.

---

## Parte 1 — Aderência aos 13 blocos do PRD ideal

Legenda de status: 🟢 Completo · 🟡 Parcial (existe, mas espalhado ou com
lacuna) · 🔴 Ausente como bloco formal.

| # | Bloco | Onde está hoje | Status | Principal gap para a v2 |
|---|---|---|---|---|
| 1 | **Contexto / Problema** | PRD Parte I.1 (90h/mês manuais, método na cabeça de sêniors, <20% briefings atualizados, lead zerado descoberto por acaso). Reforçado nas reuniões de origem no Drive | 🟢 | Nenhum — é o bloco mais maduro. Só trazer para o topo da v2 |
| 2 | **Objetivo + Métricas de sucesso** | Tabela de impacto (PRD I.3): <10h/analista, 100% carteira, >70% ações aceitas, <7d p/ lead zerado | 🟡 | **Falta North Star explícita** (nomear 1 métrica-alvo). Metas são de eficiência operacional; GEO/AEO não tem meta numérica ([[03-Produtos/growth-machine/briefing-lideranca-seo-geo-aeo]] §2.5). Definir métrica-alvo + 2-3 de apoio |
| 3 | **Escopo (dentro / fora)** | "O que NÃO faz" (verbatim), RN-108 (fora = cliente fora do MPI Plus), RN-36 (site fora do padrão MPI = fora do V1), F-28 (medição de GEO = Fase 2) | 🟡 | Existe, mas **disperso**. Consolidar uma lista única "fora de escopo v1" — hoje o leitor precisa garimpar. F-28 é a decisão de escopo mais importante e não está no PRD ainda |
| 4 | **Personas / público** | Analista, CS, Gerente/Supervisor, Front-end (executor), cliente (só MPI Plus, RN-104). Persona "Revisor" extinta (RN-49) | 🟡 | **Sem seção dedicada de personas.** Aparecem diluídas nas telas/RNs. CS é peça central da Fase 1 mas não tem tela/visão própria mapeada (gap já em [[03-Produtos/growth-machine/avaliacao-fluxo]]) |
| 5 | **Requisitos Funcionais (RF)** | Implícitos nas 4 fases + 11 telas + 10 dimensões | 🔴 | **Não existe lista de RF numerada** (RF-01…) separada das RNs. O PRD narra o "o quê" dentro da prosa das fases. É o gap estrutural nº 1: sem RF explícito, não dá para amarrar RN→RF→CA |
| 6 | **Requisitos Não-Funcionais (RNF)** | NFR-01 a NFR-24 no PRD Parte III (99,5% disponibilidade comercial, LGPD, retenção Sentinela 90d, credenciais nunca no front) | 🟡 | Existe no PRD, **não catalogado no cofre**. Lacunas: sem NFR fora do horário comercial (Sentinela roda 24/7), retenção LGPD de diagnóstico/briefing vaga |
| 7 | **Regras de Negócio (RN)** | 122 RNs catalogadas ([[03-Produtos/growth-machine/catalogo-regras-negocio]]) | 🟡 | Completo em **quantidade**, com dívidas de **qualidade** — ver Parte 2. Faltam colunas Origem e Prioridade; 5 RNs supersedidas sem marcação; várias não-atômicas |
| 8 | **User Stories + Critérios de Aceite** | — | 🔴 | **Ausência total para o GM.** O cofre já tem o padrão (`template-historia-jira`, com CA em Gherkin) e o usa no MPI Plus, mas o GM não tem nenhuma história nem CA amarrado às RNs. **É o gap nº 1 para "pronto para dev"** |
| 9 | **Fluxos (happy path + exceções)** | Fluxo de validação de briefing, 4 fases, cenários de alerta de leads A/B/C/D, Sentinela, workflow de aprovação | 🟢/🟡 | Narrativa forte. Falta **formalização** em máquinas de estado / diagramas (F-21/F-22 do Will apontam ERD e state machines ausentes) |
| 10 | **Dependências / integrações** | 16 ferramentas externas mapeadas + Salesforce + MPI Plus, com divisão de papéis explícita | 🟡 | **7 questões de integração em aberto** (Q18-21 Salesforce, Q27-30 MPI Plus) — o ponto mais crítico. Cotas não dimensionadas (PageSpeed 400/dia, GSC 6 contas, SemRush) |
| 11 | **Premissas e Riscos** | Tabela de riscos com probabilidade/mitigação (PRD I.8) | 🟡 | Boa, mas **premissas dos números não explícitas** (por que 70%, 50%, 40/40/20, 5%). Cache do MPI Plus sem duração máxima. Força-tarefa de dado legado (Scout/Kaique) sem prazo |
| 12 | **Rollout / Go-to-market** | RN-66 (automação parametrizável global/por cliente) | 🔴 | **Sem plano de faseamento / feature flag / comunicação / piloto.** Não há sequência de liberação para as ~2.500 contas. Ausente como bloco |
| 13 | **Glossário / Anexos** | [[00-Glossario]] (cofre) + glossário no PRD | 🟢 | Cobertura boa. Anexar protótipos das 11 telas e os contratos de prompt/schema JSON quando existirem |

### Leitura do bloco 1
A documentação atual é **forte em "o quê" (blocos 1, 3, 7, 9, 10, 13) e
sistematicamente fraca em "quem/quando/como validar"** — exatamente os
blocos que transformam um PRD descritivo num PRD executável: **RF numerado
(5), User Story + CA (8), métrica-alvo (2) e rollout (12)**. Isso confirma,
por outra lente, o que a `avaliacao-fluxo` já dizia ("o PRD descreve bem o
o quê, é fraco em quem e quando"). Para a nova doc, os 4 blocos vermelhos/
amarelos-críticos acima são a maior parte do trabalho novo.

---

## Parte 2 — Auditoria das 122 RNs contra os critérios de uma boa RN

Critérios aplicados: **atômica · testável · independente de implementação ·
rastreável · sem ambiguidade**. Além da cobertura pelos 4 tipos de RN
(validação/restrição · cálculo/derivação · gatilho/processo · autorização).

### 2.1 O que já está bom
- **Rastreabilidade por ID: 🟢 forte.** Toda regra tem `RN-xx` fixo, citado
  de forma consistente em todo o cofre. Esse é o critério mais bem atendido.
- **Testabilidade das RNs determinísticas: 🟢 boa.** CTR sem arredondamento
  (RN-16), pesos que somam 100 (RN-18), thresholds de status (RN-19),
  maturação 60d (RN-27), Score de Saúde (RN-96) — todas verificáveis por
  cálculo.
- **Cobertura por tipo de RN:** validação/restrição e cálculo/derivação e
  gatilho/processo estão **bem cobertos**. Ver 2.3.

### 2.2 Dívidas de qualidade (o que corrigir na v2)

| Critério | Diagnóstico | Exemplos |
|---|---|---|
| **Atômica** (1 regra por linha) | 🟡 Várias RNs empacotam 2+ regras | RN-02 (cadência + "motor roda mensal p/ todos"); RN-100 (parágrafo inteiro com Gate 1 + Gate 2 + retorno via API); RN-122 (parametrização + agentes + log, 3 regras numa) |
| **Testável** | 🟡 As qualitativas não têm critério objetivo | Régua da Dim 2 ("cobre intenção/tópicos/entidades?") depende de veredito de IA, sem amostragem/golden-set definido |
| **Independente de implementação** | 🟡 Algumas hardcodam o "como" | RN-99 fixa **GPT-5** (modelo é implementação, deveria ser parametrizável — e a própria RN-99 diz que é configurável, contradizendo o texto); RN-93 nomeia **Laravel Horizon**; várias citam FireCrawl como se fosse regra, não ferramenta |
| **Rastreável (origem)** | 🔴 Falta a coluna Origem | O formato ideal tem `ID / Regra / Descrição / Origem / Prioridade`. O catálogo tem só ID + descrição fundida. Sem Origem, não se sabe **com quem validar** cada regra 6 meses depois (Comercial? Jurídico? Compliance? Growth?) |
| **Sem ambiguidade** | 🔴 Divergências reais entre RNs | F-03: threshold crítico da Dim 1 diverge (<60% na tabela vs. <50% na régua) — e é o gate da RN-88, muda o comportamento do sistema. F-04: gap da Dim 2 achata 3 faixas numa. "Sem prazo automático" (RN-01/06) sem alerta de envelhecimento |

### 2.3 Cobertura pelos 4 tipos de RN

| Tipo | Cobertura | Observação |
|---|---|---|
| **Validação / Restrição** | 🟢 Forte | RN-16, RN-85 (trava 50%), RN-108, RN-117 (anti-spam schema), RN-84 |
| **Cálculo / Derivação** | 🟢 Forte | RN-17 (maturidade), RN-18 (pesos), Índice de Performance, RN-96 (Score) |
| **Gatilho / Processo** | 🟢 Forte | RN-106 (gatilho mensal), RN-04/RN-28 (alertas), RN-64 (Hard Stop), RN-94 |
| **Autorização (quem pode o quê)** | 🟡 Mais fraco | RN-47 (aprovação humana), RN-53 (ACL), RN-104 (cliente não acessa) existem, mas **não há matriz de autorização por ação/papel**. E há concentração de poder num só ponto (CS sozinho valida briefing; Analista acumula aprovação + validação, RN-49) — flag já em [[05-Backlog/gm-segregacao-funcoes-pontos-controle]] |

### 2.4 RNs que precisam de marcação/decisão explícita na v2
- **Supersedidas sem flag** (F-05 do Will): RN-21/22/23 (lead só formulário →
  substituídas por RN-107/RN-121 multicanal), RN-29 (contradiz réguas por
  dimensão), RN-32 (contradiz RN-88). O catálogo do cofre ainda as mantém
  sem `[SUPERSEDIDA]` — pendência registrada em
  [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]].
- **RN contra prática do Google:** RN-84 (bloqueia poda de conteúdo) é a
  **única confirmada** contra o Helpful Content System; RN-14, RN-59, RN-07
  são candidatas de risco não confirmadas
  ([[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]]).
- **RN "changelog" em vez de regra:** RN-05 ("resolvido na v1.7") descreve
  histórico, não comportamento — na v2 vira nota de versão, não RN.

---

## Parte 3 — Consolidação única dos gaps (deduplicada)

Todos os furos apontados nas várias notas, agrupados sem repetição, para
não perder nenhum ao reescrever. Cada um já tem (ou deveria ter) um item de
backlog.

**Bloqueadores de início de build (fechar antes de codar):**
1. **7 questões de integração** Salesforce/MPI Plus sem resposta (Q18-21,
   Q27-30) → [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]].
2. **Desenho fino dos prompts dos agentes** ("a casa é entregue vazia; os
   móveis são os prompts") — sem dono, prazo ou golden-set →
   [[05-Backlog/gm-desenho-fino-prompts-agentes]].
3. **17 questões em aberto sem dono/prazo** →
   [[05-Backlog/gm-atribuir-dono-prazo-questoes-abertas]].

**Dívidas de documentação (o que a v2 precisa criar):**
4. Lista de **RF numerada** separada das RNs (bloco 5) — não existe.
5. **User Stories + CA em Gherkin** amarrados às RNs (bloco 8) — não existe.
6. **North Star + métricas** (bloco 2) e **plano de rollout** (bloco 12).
7. **Coluna Origem + Prioridade** no catálogo de RN; marcar supersedidas.
8. **Artefatos de engenharia**: ERD, máquinas de estado, contratos de API
   (F-21 a F-24 do Will) — hoje o dev reinterpreta o PRD.

**Padrões de risco recorrentes (governança do PRD):**
9. "Sem prazo automático" sem alerta de envelhecimento →
   [[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]].
10. Números de negócio sem origem/calibração →
    [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]].
11. Concentração de responsabilidade em pontos de controle →
    [[05-Backlog/gm-segregacao-funcoes-pontos-controle]].
12. Fronteiras entre componentes sem critério de desempate →
    [[05-Backlog/gm-criterio-desempate-fronteiras-componentes]].

**Frente SEO/GEO/AEO (produto ideal, não só doc):** os 11 itens da fila
única em [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] +
[[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]] (alta, direção
já confirmada) e [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]].

---

## Parte 4 — Esqueleto proposto da nova documentação (v2)

Estrutura dos 13 blocos, já indicando o que **reusar** do que existe e o
que **criar do zero**. É o mapa para as próximas solicitações.

1. **Contexto/Problema** — reusar PRD I.1 quase integral.
2. **Objetivo + Métricas** — *criar*: eleger North Star + 2-3 de apoio a
   partir da tabela de impacto.
3. **Escopo dentro/fora** — *consolidar*: lista única, incorporar F-28.
4. **Personas** — *criar seção*: Analista, CS, Gerente, Front-end, cliente;
   contexto e edge case de cada.
5. **Requisitos Funcionais (RF-01…)** — *criar*: extrair das 4 fases + 10
   dimensões + 11 telas os "o quê" como RF numerados.
6. **RNF (NFR-01…)** — reusar do PRD, catalogar no cofre, fechar lacunas.
7. **Regras de Negócio** — reusar as 122, aplicar Parte 2 (atomizar, coluna
   Origem/Prioridade, marcar supersedidas, tirar o "como").
8. **User Stories + CA** — *criar*: uma história por RF, cada CA em Gherkin
   amarrado a uma RN (RN→CA rastreável). Usar `template-historia-jira`.
9. **Fluxos** — reusar narrativa + *criar* máquinas de estado.
10. **Dependências/integrações** — reusar matriz + resolver as 7 questões.
11. **Premissas e Riscos** — reusar tabela + *tornar explícitas* as
    premissas dos números.
12. **Rollout** — *criar*: faseamento, feature flag (RN-66), piloto, comms.
13. **Glossário/Anexos** — reusar [[00-Glossario]] + anexar telas e schemas.

> **Demonstração de formato dos blocos 5 e 8** (RF numerado + User Stories
> com CA em Gherkin amarrado a RN) já rascunhada e aprovada em formato pelo
> PO: [[03-Produtos/growth-machine/documentacao-v2-rf-e-user-stories]].

### Checklist "pronto para dev" aplicado ao GM hoje
- [ ] Cada RF tem RN associada? — **não** (não há RF numerado)
- [ ] Cada RN tem CA que a testa? — **não** (não há CA)
- [ ] Escopo-fora explícito? — **parcial** (disperso)
- [ ] Métricas definidas? — **parcial** (sem North Star)
- [ ] Fluxo de exceção mapeado? — **sim** (ponto forte)
- [ ] Dependências listadas? — **sim, mas 7 questões abertas**

Enquanto os "não/parcial" acima existirem, pela própria régua do
framework a documentação **ainda não está pronta para dev** — mesmo o
fluxo estando maduro.

---

## Próximos passos (aguardando decisão do PO)
1. Confirmar **por qual bloco começar** a v2 — recomendação: bloco 5 (RF) +
   bloco 8 (User Stories/CA), porque destravam o "pronto para dev" e todo o
   resto se amarra neles.
2. Confirmar a **numeração de versão** oficial (v1.0 vs. v1.9.14) antes de
   propagar — pendência de
   [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]].
3. Decidir se a v2 já incorpora a frente **SEO/GEO/AEO** (fila única) ou
   mantém como Fase 2 (respaldado por F-28).

## Notas relacionadas
- [[03-Produtos/growth-machine]] — nota-mãe do produto e do PRD
- [[03-Produtos/growth-machine/avaliacao-fluxo]] — crítica fase a fase (lente complementar a esta)
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — as 122 RNs auditadas aqui
- [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]] — 29 achados do Will (Drive)
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] — diagnóstico SEO/GEO/AEO
- [[04-Decisões/padrao-historia-jira]] — padrão de User Story/CA a usar no bloco 8
- [[00-Painel-Estado]]
- [[00-Cerebro]]
