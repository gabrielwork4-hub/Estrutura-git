---
tipo: produto
status: vivo
criado: 2026-07-10
ultima-revisao: 2026-07-10
tags: [growth-machine, validacao, fluxos, principios, seo, geo, aeo, auditoria]
---

# Validação de Fluxos × Princípios — Growth Machine

> Diferente da auditoria de rastreabilidade anterior ("está mencionado em
> algum lugar?"), esta nota percorre as **5 correntes operacionais** de
> ponta a ponta (Fase 1→4 + Sentinela) e cruza cada uma contra os **6
> princípios-núcleo** ([[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]),
> checando se a lógica realmente fecha — não só se os nomes aparecem juntos.
> Resultado: 3 correções aplicadas em [[03-Produtos/growth-machine]], 1
> documento reescrito ([[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]),
> e 2 lacunas registradas para decisão do PO.

## Os 6 princípios (referência rápida)
1. Intenção real > palavra isolada
2. Anti-canibalização como regra estrutural
3. E-E-A-T como filtro de qualidade
4. Governança humana em toda ação automatizada
5. Medir → ajustar → remedir (loop fechado)
6. Alinhamento com sistemas do Google nomeados

---

## Fluxo A — Fase 1: Entrada e Briefing

```
Cliente entra no MPI Plus → RF-01 importa (completo) OU RF-02 FireCrawl
(legado) → RF-03 CS valida (RN-01/06) → RF-04 score de aderência →
[NOVO] Dim 1 mapeia cluster de suporte (/informacoes) → RN-EST-01–06
governam a construção do estudo em si (Gregory/MPI Plus)
```

| Princípio | Confere? | Evidência / achado |
|---|---|---|
| 1. Intenção real | ✅ | RN-EST-02 (palavra épica por volume/categoria) + cluster mapeia intenção informacional que a página comercial não serve |
| 2. Anti-canibalização | ✅ | RN-15/85 (bonificação) + RN-EST-06 (exclusão /informacoes do crawl) evita que o cluster e a página MPI disputem a mesma keyword |
| 3. E-E-A-T | 🟡 | Só entra em Fase 3 (RN-SGA-07), não na construção do briefing — aceitável, E-E-A-T é atributo de conteúdo, não de briefing |
| 4. Governança | ✅ | RN-01 trava avanço sem validação ativa do cliente |
| 5. Loop de medição | 🟡 | Score de aderência do estudo existe, mas sem histórico/tendência entre ciclos — não é um gap novo, é herdado |
| 6. Alinhamento Google | ✅ | RN-EST-06/cluster nasce diretamente do antídoto ao scaled content abuse |

**Achado:** nenhuma contradição. Único ponto fraco (Fase 1 não mede
E-E-A-T) é esperado — não é defeito.

---

## Fluxo B — Fase 2: Motor de Percepção

```
RN-106 gatilho mensal → RN-64 Hard Stop check → RN-16 CTR por faixa →
RN-17 maturidade → RN-18 Índice (40/40/20, sob revisão) → RN-19 status →
RN-02 cadência
```

| Princípio | Confere? | Evidência / achado |
|---|---|---|
| 1. Intenção real | N/A | Fase numérica, não se aplica diretamente |
| 2. Anti-canibalização | N/A | — |
| 3. E-E-A-T | N/A | — |
| 4. Governança | ✅ | Camada de Calibração Contínua propõe, Gerente/Admin aprova — nada recalibra sozinho ([[04-Decisões/adr-camada-calibracao-continua]]) |
| 5. Loop de medição | ✅ **fortalecido** | Antes: fórmula fixa, sem mecanismo de atualização. Agora: Camada de Calibração Contínua fecha o loop também para os *parâmetros* da fórmula, não só para o resultado |
| 6. Alinhamento Google | 🟡 | RN-SGA-11 (tráfego origem IA) é só segmentação de **relatório**, não altera `trafego_real` (RN-86 continua "só orgânico") — confirmado, sem conflito, mas vale deixar explícito para não haver ambiguidade futura |

**Achado corrigido nesta rodada:** confirmado que RN-SGA-11 é aditivo
(reporting), não modifica RN-86 — nenhuma edição necessária, já estava
correto, só não estava dito explicitamente. Adicionado ao texto da Fase 2.

---

## Fluxo C — Fase 3: Auditoria em 10 Dimensões (+ Dim 11)

```
RN-88 gate: Dim 1 crítica (<50% OU 3 gatilhos) → trava tudo
Senão → Dim 2–10 rodam em paralelo → Score de Saúde (RN-96, só 2-10) →
Parecer Consolidado (10 dimensões + Índice + Score + Sentinela)
Dim 11 roda à parte, Fase 2 futura, fora do Score
```

| Princípio | Confere? | Evidência / achado |
|---|---|---|
| 1. Intenção real | ✅ | 2D/2E/RN-SGA-02/04/07 todas checam conformidade de intenção, sem inflar o peso de Dim 2 (confirmado: 18 inalterado) |
| 2. Anti-canibalização | ✅ | RN-SGA-06 (subdomínios) + anti-canibalização dentro do cluster, ambas amarradas à Dim 3 |
| 3. E-E-A-T | ✅ | RN-SGA-07 (2E) — **mas ver correção abaixo, princípio estava descrito como "já pronto"** |
| 4. Governança | ✅ | Nenhum sub-check novo (2D/2E/Dim11) publica sozinho — segue RN-89 (traduz, não decide) → RN-47 (aprovação) |
| 5. Loop de medição | ⚠️ **gap real, sem correção ainda** | Dim 11 é o loop fechado para GEO, mas está Fase 2/não implementada — o gap que o princípio 5 descreve como "o mais repetido" **continua aberto**, só documentado com mais precisão agora |
| 6. Alinhamento Google | ✅ | RN-SGA-05 (Portão) é o antídoto direto ao scaled content abuse; RN-SGA-13/refinamento treino×citação alinha à distinção real que motores de IA fazem |

**Achado crítico confirmado, não nosso — já registrado no F-39 da vault
externa:** o princípio 5 (loop fechado) segue sendo o gargalo real do
produto. Nada nesta rodada de reconciliação resolve isso de fato — só
melhora a qualidade do diagnóstico. **Isso não é um erro nosso, é o estado
real do produto.**

---

## Fluxo D — Fase 4: Aprovação, Execução e Validação

```
Fila de ações → Analista aprova → [conteúdo? Gate 1: clique Gerar,
RN-SGA-05 checa antes] → MPI Plus gera → Gate 2 revisão → Salesforce →
execução → validação IA (RN-81) → maturação 60d (RN-27)
```

| Princípio | Confere? | Evidência / achado |
|---|---|---|
| 1. Intenção real | ✅ | Herdado da Fase 3, nada muda na execução |
| 2. Anti-canibalização | ✅ | Bloqueada na origem (Fase 1/3), não precisa reverificar na execução |
| 3. E-E-A-T | ✅ | Conteúdo gerado no MPI Plus já carrega os sinais checados em 2E antes de chegar aqui |
| 4. Governança | ✅ **confirmado, era suposição** | [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] já dizia "mesmo fluxo Gate 1/Gate 2" — confirmado agora que o Portão de Diferenciação Real (achado desta rodada) se encaixa **dentro** do Gate 1 existente, não cria um gate paralelo |
| 5. Loop de medição | ✅ | RN-123/RN-124 (proposta) fecham exatamente o mesmo tipo de loop que RN-81 já faz para SendGrid — agora também para WhatsApp |
| 6. Alinhamento Google | N/A | Fase de execução, não de estratégia de conteúdo |

**Achado:** nenhuma contradição nova. A única confirmação que faltava
(Gate 1 acomoda o Portão sem gate paralelo) foi verificada e documentada
nesta rodada.

---

## Fluxo E — Módulo Sentinela

```
Diário, independente do ciclo mensal, 100% dos sites, sem APIs caras →
RN-92 checks (uptime/SSL/DNS/robots/AI Instructions) → RN-94 sobreposição
ao bloqueio em incidente crítico
```

| Princípio | Confere? | Evidência / achado |
|---|---|---|
| 1. Intenção real | N/A | Módulo de infra, não de conteúdo |
| 2. Anti-canibalização | N/A | — |
| 3. E-E-A-T | N/A | — |
| 4. Governança | ✅ | Alertas, não ações automáticas — mesma régua |
| 5. Loop de medição | ✅ | Checagem diária é, por natureza, o loop mais rápido do produto |
| 6. Alinhamento Google | ⚠️ **duas velocidades, agora explícitas** | RN-SGA-13 (checar robots.txt hoje) é diário/Sentinela; a matriz treino×citação que ele consulta é **revisada trimestralmente** pela Camada de Calibração Contínua — duas cadências diferentes que precisavam ficar claras para não confundir "checar" com "decidir o que checar" |

**Correção aplicada:** nenhuma neste fluxo — a distinção de cadência já
estava correta na Camada de Calibração Contínua, só não estava cruzada
explicitamente com o Sentinela. Registrada aqui para referência; não
exigiu edição de arquivo (a informação já existe nos dois lugares certos).

---

## Síntese — o que a validação confirma

- **Nenhuma contradição lógica real** foi encontrada entre as adições desta
  sessão (Cluster Wrapping, Camada de Calibração Contínua, Portão de
  Diferenciação Real, RN-SGA-*, RN-EST-*, RN-123/124) e o fluxo operacional
  já existente. Tudo se encaixa em gates/mecanismos que já existiam
  (RN-88, RN-100 Gate 1, RN-96, RN-89, RN-47), sem criar caminhos
  paralelos.
- **1 gap real permanece, e não é desta rodada:** o princípio 5 (loop
  fechado) segue quebrado para GEO/AEO — Dim 11 resolve no papel, mas está
  Fase 2. Nenhuma quantidade de reconciliação documental fecha isso; só
  implementação fecha.
- **1 documento estava desatualizado a ponto de esconder o achado mais
  crítico do projeto:** [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]
  (parado em 2026-07-06) não tinha o Cluster Wrapping/anti-doorway na fila
  de prioridade — reescrito nesta rodada, ver abaixo.

## O que foi corrigido em growth-machine.md nesta validação
1. Portão de Diferenciação Real amarrado explicitamente ao Gate 1 (RN-100).
2. Confirmado por escrito que sub-dimensões 2D/2E não alteram o peso de
   Dim 2 (continua 18).
3. Nota futura no Parecer Consolidado sobre incorporar Dim 11 quando
   implementada, sem fundir no Score de Saúde.

## Notas relacionadas
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — reescrito nesta rodada
- [[03-Produtos/growth-machine]] — 3 correções de fluxo aplicadas
- [[04-Decisões/adr-camada-calibracao-continua]] · [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]
- [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]]
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]]
- [[00-Painel-Estado]] · [[00-Cerebro]]
