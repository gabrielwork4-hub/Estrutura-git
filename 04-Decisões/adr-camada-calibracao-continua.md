---
tipo: decisao
status: aceita
criado: 2026-07-10
tags: [growth-machine, indice-performance, rn-18, rn-122, calibracao-continua, gregory, vault-externa, governanca]
---

# Camada de Calibração Contínua — pesos ficam 40/40/20 "sob revisão", calibrados por dado real

## Contexto
Três fontes davam três respostas incompatíveis para o mesmo peso do
Índice de Performance (achado **F-30**, identificado de forma independente
tanto neste cofre quanto na vault externa "Vault PRD GROWTH MACHINE
MODIFICADO", autoria Lucas Bevilacqua/Gabriel Santos):

| Fonte | Posição | Tráfego | Leads |
|---|---:|---:|---:|
| PRD oficial v1.9.19 (RN-18) | 40% | 40% | **20%** |
| Documento original do Gregory | 40% | 30% | 30% |
| Ata da Reunião 05 (24/03) | "pesos diferentes, **lead é a principal**" | — | — |

O peso vigente hoje dá ao lead o **menor** peso dos três — o oposto do que
a ata registrou como intenção original.

Neste cofre, avaliamos a mesma contradição e propusemos **35/20/45**,
fundamentado no consenso de mercado 2026 sobre zero-click/AI Overview (ver
[[04-Decisões/adr-pesos-indice-performance-2026]], agora superada). A vault
externa chegou a uma resposta **mais rigorosa**: em vez de escolher um
número por leitura de mercado, tratar o peso como **parâmetro calibrável
por correlação real** com o outcome de negócio da própria carteira — dado
que a Ideal Trends já rastreia (renovação de contrato, aceite de upsell,
churn), não estatística de mercado genérica.

## Decisão
1. **Manter RN-18 em 40/40/20** — é a decisão mais recente documentada —
   mas com **flag explícita**: *"peso do lead sob revisão — diverge do
   método original (Gregory) e da ata de decisão (Reunião 05)"*. Não
   silenciar a contradição enquanto ela não é resolvida com dado.
2. **Adotar a Camada de Calibração Contínua** como mecanismo formal de
   recalibração — extensão do padrão que já existe no PRD (`ruleset_version_id`,
   versionamento + rollback na Tela 8/9). Hoje esse padrão registra *quando
   um humano mudou algo manualmente*; a Camada adiciona *quando o sistema
   propõe uma mudança, com base em quê, e quem aprova antes dela valer*.
   Aplica-se, no mínimo, a: `ctr_estimado`, curva de benchmark de CTR
   (fallback), curva de `posicionamento_esperado`, pesos do índice final,
   radar de prioridade de schema, matriz treino×citação de bots de IA,
   threshold de cobertura semântica (Dim 2).
3. **Fluxo de recalibração** (mesmo princípio da RN-47 — aprovação humana
   obrigatória — aplicado à calibração, não só à execução):
   ```
   Job periódico calcula → gera PROPOSTA (não aplica direto) → Tela 8/9
   mostra valor atual × proposto + fonte/metodologia + amostra + impacto
   estimado → Gerente/Admin aprova, ajusta ou rejeita → só então vira
   ruleset_version_id vigente → log imutável (valor anterior, novo, fonte,
   quem aprovou, quando)
   ```
4. **Fallback sem dado suficiente**: mantém o valor anterior e sinaliza
   "sem dado suficiente para recalibração" — nunca gera número não
   confiável só para preencher o campo.
5. **Dois quick wins, sem dependência de nenhuma decisão** (podem rodar já,
   sobre dado que a operação já tem):
   - **C3** — backtest da curva de `posicionamento_esperado`: hoje é uma
     suposição (`= maturidade_final`); selecionar projetos Bom/Ótimo,
     reconstruir série histórica de `percentual_posicionamento_real` por
     mês-no-ar, calcular mediana por faixa — vira a curva real.
   - **C4** — correlação (Pearson, por segmento) entre cada índice
     individual (posição/tráfego/leads) e outcome de negócio real
     (renovação/upsell/churn) — alimenta diretamente a decisão de peso.

**Nosso racional de zero-click/AI Overview (ADR superada) não é
descartado** — vira um dos insumos de leitura de mercado que compõe a
análise, ao lado do dado interno de C3/C4, não o substituto dele.

### Refinamentos adicionais da vault externa incorporados
- **`ctr_estimado` tem problema de circularidade** (achado F-08/F-31): se a
  posição de um cliente despenca, o "potencial" calculado despenca junto —
  o índice de tráfego pode *melhorar* no mês em que o SEO piorou, porque a
  régua caiu com ele. Proposta: baseline defasada (últimos 6 meses,
  usando só os meses com `indice_posicionamento ≥ 0.90` — "janela
  saudável"; se `≥2` meses saudáveis, CTR = cliques/impressões desses
  meses; senão, benchmark externo segmentado), recalibrada **trimestral**,
  não mensal.
- **Curva de CTR fallback não pode ser única**: negócio local (Local Pack)
  tem curva muito mais achatada que busca orgânica clássica (cair de #1
  pra #3 no mapa custa ~2,5pp; na busca orgânica custa ~30pp). A tabela
  genérica Top3/Top10/>10 erra sistematicamente pra metade da carteira
  (clientes locais/regionais). Segmentar em 2 curvas (Local Pack ×
  orgânica clássica), escolhidas pelo tipo de projeto (RN-09) + sinal de
  atuação regional do briefing.
- **Cobertura de GSC é o teto real por trás da migração de fonte** (achado
  F-32): a fonte de posicionamento migrou de GSC direto (Gregory) para o
  relatório mensal do MPI Plus (PRD) — provavelmente pelo teto de
  cobertura do GSC com só 6 contas para ~2.500 clientes. Confirma a
  decisão C5 já tomada ([[03-Produtos/growth-machine/reconciliacao-regras-gregory]])
  com o motivo real, não só a suposição. Mitigação: expandir para 9-10
  contas/service accounts, ou implementar alocação dinâmica enquanto isso
  não sai.

## Alternativas consideradas
- **Manter nossa ADR (35/20/45)** — descartada: é leitura de mercado, não
  dado da própria operação; a vault externa propõe algo estritamente mais
  rigoroso e rastreável.
- **Adotar 40/30/30 do Gregory diretamente** — descartada: mesma objeção,
  nenhuma das três fontes tem base empírica própria da carteira.
- **Resolver por decreto agora** (qualquer um dos três números) —
  descartada: silenciaria a contradição (F-30) sem resolvê-la; a Camada de
  Calibração Contínua é o mecanismo que evita esse padrão se repetir daqui
  a um ano com outro número.

## Consequências
- **Positivo**: transforma "descoberta acidental" (alguém tropeça num
  benchmark datado numa auditoria) em "revisão agendada" — mesmo que a
  resposta seja "nada mudou", vira registro deliberado.
- **Positivo**: decisão de peso passa a ser informada por dado real da
  carteira Ideal Trends, não por debate ou leitura de mercado isolada.
- **Positivo**: resolve também `ctr_estimado` (circularidade) e a curva de
  CTR única (Local Pack × orgânica) — problemas que nenhuma das duas ADRs
  de peso, isoladamente, atacava.
- **Negativo / ação necessária**: C3 e C4 precisam rodar antes de qualquer
  novo peso ser proposto — não há atalho para "resolver agora".
- **Negativo / ação necessária**: exige nova capability (job periódico +
  tela de proposta/aprovação) — não é só mudar um número na Tela 8, é
  construir o mecanismo. Ver Frente C em
  [[03-Produtos/growth-machine/plano-fechamento-prd-v2]].

## Relacionados
- [[04-Decisões/adr-pesos-indice-performance-2026]] — ADR superada por esta
- RN-18 (pesos do índice): [[03-Produtos/growth-machine/catalogo-regras-negocio]]
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — conflito C1
- [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] — episódio completo
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — Frente C (quick wins C3/C4)
- [[03-Produtos/growth-machine]] · [[00-Cerebro]]
