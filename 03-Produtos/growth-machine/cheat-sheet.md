---
tipo: produto
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-14
tags: [growth-machine, cheat-sheet, resumo]
---

# Cheat Sheet — Growth Machine

> Uma página. Só o que você citaria de cabeça numa reunião, sem abrir nada.
> Reflete o [[PRDFINAL]] (v1.2). Para contexto/explicação completa, ver
> [[03-Produtos/growth-machine]].

## O produto em 1 frase
Orquestração de SEO/GEO/AEO que diagnostica ~2.500 clientes MPI
automaticamente (hoje ~90h/analista/mês manual) e gera fila de ações
priorizada — não publica nada sozinho, quem executa é o Front-end via
Salesforce.

## Pré-requisito
**RN-108** — só atende cliente já no **MPI Plus**. Fora do MPI Plus →
entra lá primeiro. **MPI Plus é o sistema interno do Grupo** (centraliza
o cliente do onboarding à validação final) — o GM roda por cima dele
como camada de diagnóstico, não é o dono do histórico do cliente.

## Números que valem de cabeça

| O quê | Valor |
|---|---|
| Pesos do Índice de Performance | **40 posicionamento / 40 tráfego / 20 leads** — ⚠️ sob revisão (Camada de Calibração Contínua) |
| Thresholds de status | Ruim **&lt;0,60** · Regular **0,60–0,79** · Bom **0,80–0,89** · Ótimo **≥0,90** |
| Cadência de análise | Ruim/Regular → **mensal** · Bom/Ótimo → **trimestral** |
| Janela de maturação | **60 dias fixos**, começa só após OK do analista |
| CTR por posição | Top 3 → **20%** · Top 10 → **5%** · abaixo → **1%** (sem arredondar; ⚠️ segmentação Local Pack × orgânica ainda pendente) |
| Escala | **~2.500 clientes**, 3 empresas (Ideal Marketing / Busca Cliente / MPI Solutions) |
| Gatilho do ciclo | Relatório mensal MPI Plus, **~dia 1º/2**, **automático** |
| Retry site fora do ar | **3 tentativas**, dias diferentes, antes de alertar |
| Alerta lead zerado | **7 dias** consecutivos sem lead = alerta extremo |
| Alerta SSL | **30 / 15 / 7 dias** antes de expirar |
| Tamanho do PRD | **146 RNs** · **55 RFs** · 8 User Stories · 10+1 dimensões · 11 telas |

## As 4 fases (ordem)
**1. Briefing → 2. Motor de Percepção (mensal) → 3. Auditoria (10 dimensões + Dim 11 fase seguinte) → 4. Aprovação/Execução/Validação**

## As 10 dimensões (ordem de prioridade MPI)
1. Estudo (+ mapeia cluster de suporte) · 2. Conteúdo/GEO/AEO (+ sub-checks
de meta/title, E-E-A-T, priorização por nicho) · 3. Arquitetura/Silo (+
canibalização entre subdomínios) · 4. W3C · 5. PageSpeed · 6. Schemas ·
7. Sitemap/Robots (+ controle de crawler de IA) · 8. Search Console ·
9. Servidor/TTFB · 10. Leads · **11. GEO/Citação (fase seguinte, fora do
Score de Saúde)**

**Regra de ouro (RN-88):** só a Dimensão 1 (Estudo) trava a auditoria
inteira. As outras rodam em paralelo.

## 3 sistemas, 3 papéis — nunca se misturam
- **Growth Machine** = diagnostica. 100% interno. Cliente nunca acessa.
- **MPI Plus** = sistema do Grupo, gera conteúdo/estudo + aprovação do cliente + publica no WordPress.
- **Salesforce** = CRM global, gestão de demanda/execução. Pooling **mensal**: registra todo cliente todo mês; só volta a acionar o fluxo do GM quando o ciclo classifica como **"Ruim"**.

## Módulo Sentinela (diferente das 10 dimensões)
Roda **todo dia**, à noite, em **100% dos sites** (até os bloqueados/em
maturação) — checa só uptime/SSL/DNS, nada caro. Se site cai ≥3 dias ou
SSL expira → reabre análise mesmo com maturação em curso.

## Agentes de IA
Configurável por agente. Detectam e recomendam — **nunca publicam**.
Toda ação passa por aprovação humana (RN-47) e dois gates antes de
chegar ao cliente (Gate 1: aciona geração · Gate 2: revisão do resultado).

## Os 2 riscos que mais importam
1. **"A casa é entregue vazia; os móveis são os prompts."** Arquitetura
   pronta, conjunto de validação dos prompts dos agentes ainda não —
   maior risco de execução.
2. **Doorway / conteúdo gerado em escala sem diferenciação real.** É o
   exemplo textual que o Google usa pra definir o padrão punido nos core
   updates 2026 (queda de 50-80% de tráfego). **Antídoto já desenhado:**
   Cluster Wrapping (páginas de suporte aditivas, sem tocar contrato) +
   Portão de Diferenciação Real (checa dado local/prova social/pergunta
   real antes de gerar). **Falta:** medir a exposição real na carteira
   atual (Frente Z1) — recomendado antes do piloto, sem dependência técnica.

## Os 3 sistemas do Google — antídoto de cada um
| Sistema | Antídoto no produto | Status |
|---|---|---|
| Helpful Content (conteúdo fraco acumulado) | Poda por scoring — RF-55 | Especificado, falta construir |
| E-E-A-T (autor/fonte/confiança) | Auditoria on-page — RF-50 | Especificado, falta construir |
| Scaled Content Abuse / Doorway | Cluster Wrapping + Portão — RF-47/51/54 | Desenhado, risco real ainda não medido |

## Fechado nesta última rodada (não é mais bloqueador)
As **7 questões de integração Salesforce/MPI Plus** — eram o maior
bloqueador de build do PRD, todas endereçadas.

## 5 padrões recorrentes de risco (aplicar em qualquer PRD, não só este)
1. "Sem prazo automático" sem alerta de envelhecimento
2. Números de negócio sem origem documentada
3. Concentração de responsabilidade num único ponto de controle
4. Fronteiras entre componentes sem critério de desempate
5. Questões em aberto sem dono/prazo

## O que ainda está genuinamente aberto
- **Golden-set dos prompts** dos agentes de IA — maior risco de execução.
- **Frente Z1** — auditoria da carteira atual por doorway, ainda não rodou.
- **Cotas de ferramentas** (PageSpeed/GSC/SemRush) não dimensionadas.
- **ERD** + máquinas de estado formais.
- **~15 questões do PRD original nunca transcritas** para o cofre (fora
  das que já foram endereçadas).

## Notas relacionadas
- [[PRDFINAL]] — o PRD que este resumo reflete
- [[03-Produtos/growth-machine]] — nota completa
- [[03-Produtos/growth-machine/avaliacao-fluxo]] — avaliação crítica
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — todas as 146 RNs
- [[04-Decisões/adr-camada-calibracao-continua]] · [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]
- [[00-Painel-Estado]]
- [[00-Glossario]]
