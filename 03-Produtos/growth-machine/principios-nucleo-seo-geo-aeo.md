---
tipo: produto
status: vivo
criado: 2026-07-06
ultima-revisao: 2026-07-10
tags: [growth-machine, seo, geo, aeo, principios, roadmap]
---

# Princípios-núcleo SEO/GEO/AEO — por que cada resolução foi priorizada

> **Reconciliado em 2026-07-10** com o caso real do emtecorp, as regras do
> Gregory e a vault externa (achados F-30 a F-40) — ver
> [[03-Produtos/growth-machine/validacao-fluxos-principios]]. A fila abaixo
> mudou de posição #1: o achado de doorway/scaled content (F-39) não
> existia quando esta nota foi escrita em 06/07 e é, por unanimidade das
> duas análises independentes, **o item mais urgente do projeto inteiro**.

> Documento explicativo, não é feature nova. Formaliza o raciocínio já
> construído em [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
> e em [[01-Ideias/anti-praticas-seo-growth-excellence]] — aqui a intenção é
> unir os 3 pilares (hoje tratados em tabelas separadas) numa única leitura
> de princípios e numa única fila de prioridade, com o "porquê" explícito de
> cada posição. Serve de matéria-prima para o template oficial de
> documentação que está sendo desenhado com o PO.

## Por que este documento existe
Até aqui, SEO, GEO e AEO foram analisados como 3 frentes paralelas — cada
uma com seu score, suas lacunas, seu tempo estimado. Isso é correto para
diagnóstico, mas esconde uma coisa importante: **os três pilares são a
mesma lógica de busca aplicada em granularidades diferentes**, e boa parte
das ideias de melhoria serve a mais de um pilar ao mesmo tempo. Separar em
3 listas faz o time perder essas sinergias e priorizar por pilar, não por
impacto real. Este documento existe para corrigir isso.

## Princípios-núcleo (atravessam os 3 pilares)

### 1. Intenção real > palavra isolada
- **Em SEO:** cluster de keywords por intenção de busca, não por volume
  isolado — base de [[02-Fluxos/estudo-de-keywords]].
- **Em GEO:** trecho extraível que responde sozinho a uma pergunta real,
  sem depender do parágrafo anterior.
- **Em AEO:** frase única, literal, sem ambiguidade — a versão mais rígida
  da mesma ideia, porque aqui só existe uma resposta escolhida, não uma
  lista.
- **Por quê isso é o princípio-mãe:** todo o resto (anti-canibalização,
  arquitetura de silo, extrabilidade) é uma consequência de levar essa
  ideia a sério em cada granularidade. É o único princípio que já está
  100% maduro em SEO e 0% formalizado em AEO — a distância entre os dois
  extremos é a distância entre os pilares.

### 2. Anti-canibalização como regra estrutural, não checagem pontual
- Vale para páginas competindo pela mesma busca (SEO), para trechos
  competindo pela mesma citação de IA (GEO), para qual é *a* resposta
  (AEO — o caso mais crítico, porque não há "segundo lugar credível").
- **Por quê importa mais em AEO do que parece:** em SEO, duas páginas
  canibalizando ainda aparecem as duas na SERP, só que mal posicionadas —
  o dano é gradual. Em AEO, a resposta escolhida é uma só; perder essa
  disputa não é "cair de posição", é ficar invisível.

### 3. E-E-A-T como filtro de qualidade, não decoração
- Já explícito nos **prompts de conteúdo** do MPI Plus (nível de geração).
  `[correção 2026-07-10]` a auditoria **estrutural** on-page (autor,
  página "sobre", fontes citadas) ainda não existe como checagem — é a
  proposta **RN-SGA-07** (sub-dimensão 2E, nova, MVP). Ou seja: E-E-A-T é
  princípio na geração, mas só vira auditável de fato quando RN-SGA-07
  entrar em produção.
- **Por quê é tratado como princípio-núcleo e não como item de SEO:** o
  Google trata E-E-A-T como critério transversal (mais rígido ainda em
  YMYL) — um site que falha nisso é penalizado tanto na SERP tradicional
  quanto na chance de ser citado por um motor generativo. Não é possível
  "ter E-E-A-T só pra SEO".

### 4. Governança humana em toda ação automatizada
- RN-47 (aprovação obrigatória), RN-81 (validação por IA pós-execução),
  Gate 1/Gate 2 na geração delegada ao MPI Plus.
- **Por quê isso não muda com GEO/AEO:** a tentação ao adicionar novos
  pilares é automatizar mais rápido (mais dimensões, mais agentes) — mas
  o princípio do produto é que velocidade de cobertura não pode custar
  supervisão humana. Toda ideia nova das seções abaixo herda essa regra
  por padrão, não é reavaliada caso a caso.

### 5. Medir → ajustar → remedir (loop fechado)
- É onde SEO está maduro (Índice de Performance: 40% posicionamento + 40%
  tráfego + 20% leads — `[⚠️ sob revisão, achado F-30]`, ver
  [[04-Decisões/adr-camada-calibracao-continua]]) e onde GEO/AEO falha por
  completo — nenhuma métrica de citação ou de "resposta escolhida" compõe
  nota nenhuma hoje (**Dimensão 11, proposta, ainda Fase 2**).
- **Por que este é o gargalo mais repetido em toda a documentação:** sem
  esse loop, GEO/AEO não tem como provar progresso nem regressão — é o
  motivo direto pelo qual a integração com [[03-Produtos/ideal-tracker]]
  aparece como "maior alavancador único" no comparativo de maturidade: não
  é a ideia mais sofisticada, é a que resolve o gargalo mais estrutural
  com o menor esforço (a métrica já existe, só não está plugada).
- **`[novo, 2026-07-10]` o princípio se generalizou além de SEO/GEO/AEO:**
  a Camada de Calibração Contínua ([[04-Decisões/adr-camada-calibracao-continua]])
  aplica o mesmo "medir → ajustar → remedir" aos **parâmetros do modelo**
  em si (pesos, CTR, curvas), não só ao resultado — antes, um benchmark
  envelhecia em silêncio (aconteceu com a tabela de CTR); agora vira
  revisão trimestral/semestral agendada, com aprovação humana (princípio
  4). Confirma que este é o princípio mais transversal dos 6 — vale tanto
  para "o site melhorou?" quanto para "o modelo que mede isso ainda é
  válido?".

### 6. Alinhamento com sistemas do Google nomeados explicitamente
- **Helpful Content System** — qualidade do domínio inteiro é avaliada,
  não só página a página; conteúdo fraco acumulado arrasta o resto.
- **E-E-A-T reforçado em YMYL** — já coberto no princípio 3.
- **`[novo, 2026-07-10]` Scaled Content Abuse / Doorway Pages** — política
  de spam ativa desde 2024, prioridade número um de fiscalização desde
  março/2026 (sites flagrados perdem 50-80% de tráfego em 2 semanas),
  estendida a citação em AI Overviews desde maio/2026. **É o único dos três
  sistemas nomeados onde o produto hoje faz o oposto do que a prática pede**
  (achado F-39) — o método de geração de página por combinação
  palavra×região×tipo é, textualmente, o exemplo que o Google usa para
  definir o padrão punido. Ver
  [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] para a
  solução (Cluster Wrapping + Portão de Diferenciação Real, RN-SGA-05).
- **Por que agora são três, não dois:** os dois primeiros já estavam
  citados com nome próprio no comparativo de maturidade; o terceiro
  entrou porque virou **achado confirmado com fonte e data** (não achismo)
  — mesma régua que já regia esta seção antes.

## Onde cada pilar está hoje (e por que a régua é diferente)

| Pilar | Score | Por que a régua não é a mesma dos outros dois |
|---|---|---|
| SEO tradicional | ~75-80% `[⚠️ score anterior ao achado F-39]` | Auditoria comparativa contra concorrentes reais (Dimensão 2), 10 dimensões cobrindo o site inteiro — regra madura, é polimento. **Mas** o score não considerava risco ativo de penalização por doorway pages (não era conhecido em 06/07) — não é score de "quão bem otimizado", é score sem esse fator de risco embutido |
| GEO | ~20-25% | Fundação existe (Dimensão 2C), mas audita página, não bloco extraível — e não tem loop de mensuração nenhum |
| AEO | Não medido (mais baixo que GEO) | Tratado até hoje como sinônimo de GEO no glossário e nas regras — nunca teve critério, dimensão ou métrica própria |

**Por que AEO fica atrás mesmo de GEO, e não empatado:** GEO ao menos tem
um pilar maduro (Dimensão 2C) e uma métrica pronta isolada (Ideal
Tracker). AEO não tem nenhum dos dois — o único material dedicado a AEO no
cofre inteiro é a análise de lacunas, nunca uma implementação.

## Fila única de prioridade (as 3 frentes cruzadas, não 3 filas separadas)

> Esta é a mudança de formato central deste documento: em vez de "3
> lacunas por pilar", uma fila só, ordenada por esforço/impacto real,
> porque várias ideias servem mais de um pilar ao mesmo tempo — priorizar
> por pilar isolado faria o time refazer trabalho equivalente duas vezes.
> **Reordenada em 2026-07-10** — cada item agora aponta a RN proposta
> correspondente ([[03-Produtos/growth-machine/catalogo-regras-negocio]]),
> fechando a rastreabilidade RN→princípio→prioridade.
>
> **Reconciliação com a vault externa:** esta fila cobre SEO/GEO/AEO; o
> roadmap da vault externa (Frente Z/A-G, ver
> [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]]) cobre
> um escopo mais largo (inclui calibração de fórmula, cobertura de dados,
> leads multicanal). Onde os dois se sobrepõem (item 1 = Frente Z desta
> fila), a ordem é a mesma; onde não se sobrepõem, são complementares, não
> concorrentes.

| Ordem | Ideia | RN | Pilar(es) | Por que essa posição |
|---|---|---|---|---|
| **1** | **Anti-doorway / Cluster Wrapping** — auditar a carteira por quase-duplicatas (Frente Z1, já) + construir cluster de suporte em `/informacoes`/`/artigos` (aditivo, zero toque no contrato) | **RN-SGA-05, RN-SGA-06** | SEO | `[NOVO, 2026-07-10]` **Item mais urgente do documento inteiro** — não é melhoria, é redução de risco ativo: o método de geração por combinação palavra×região×tipo é o exemplo textual que o Google usa para doorway/scaled content abuse, punido com força total desde março/2026 (50-80% de queda em sites flagrados). Confirmado por duas análises independentes (esta + vault externa, achado F-39) |
| 2 | Poda de conteúdo — ajustar RN-84 de bloqueio total para sugestão de candidata, com scoring (baixo tráfego + baixa relevância + sem backlink) | RN-84 (ajuste) | SEO | Continua alta prioridade — única RN que hoje faz o oposto do Helpful Content System — mas cede o #1 para o item 1, que é risco ativo, não só contradição de boa prática |
| 3 | E-E-A-T on-page — autor, página "sobre", fontes citadas (sub-dimensão 2E) | **RN-SGA-07** | SEO + GEO | `[NOVO]` Barato (MVP), e é o único dos 3 sistemas nomeados do princípio 6 onde falta só **auditoria**, não geração — o conteúdo já nasce com E-E-A-T no prompt, falta checar |
| 4 | Priorização de AEO por nicho — pesar a régua AEO conforme o nicho do cliente (local/prático vs. B2B complexo) | RN-SGA-04 | AEO | Mais barato de todos (1 sprint) — reaproveita a segmentação de nicho que o briefing já coleta |
| 5 | Meta description ≤160 / title ≤60 como checagem determinística em 2C | RN-SGA-03 | SEO + AEO | Regra já validada externamente (Growth Excellence), barata, serve dois pilares — reduz truncamento (SEO) e aumenta chance de snippet direto (AEO) |
| 6 | Sinal "conteúdo preso em PDF → migrar para HTML" | **RN-SGA-16** | SEO | `[NOVO]` Barato (MVP) — catálogos/PDFs hoje competem como ativo primário em vez de HTML indexável (caso real: emtecorp) |
| 7 | Extrabilidade de bloco — cada seção responde sozinha, sem depender do parágrafo anterior | RN-SGA-01 | GEO + AEO | Mesma base de prompt/checagem serve as duas frentes — 1-2 trimestres |
| 8 | Resposta única e inequívoca por pergunta do nicho (AEO estrito) | **RN-SGA-02** | AEO | `[NOVO, separado do item 7]` Mais rígido que extrabilidade — aqui a resposta é lida literalmente, não parafraseada; reaproveita a mesma base, mas é checagem própria |
| 9 | Sinal de conteúdo original / information gain frente à SERP | **RN-SGA-08** | SEO + GEO | `[NOVO]` Motores generativos preferem citar informação exclusiva — hoje o produto audita cobertura, não ineditismo |
| 10 | Accessibility tree + Cumulative Layout Shift + WebMCP (pilares agênticos) | RN-SGA-15 | GEO | Accessibility+CLS reaproveita Core Web Vitals (barato); WebMCP é mais caro e incerto (depende de o site do cliente implementar protocolo emergente) — mesma RN, custos internos diferentes |
| 11 | Log de crawler real (bots de IA + Googlebot) — confirmar visita real, não só permissão declarada | RN-SGA-12 | SEO + GEO | Mais caro (log de servidor por cliente), resolve lacuna de SEO e GEO com a mesma infraestrutura |
| 12 | Controle granular de crawler de IA — distinguir bloqueio de treino (sem custo) de bloqueio de citação ao vivo (custo real, Perplexity) | **RN-SGA-13** | GEO | `[NOVO, refinamento validado externamente]` Mais barato que o item 11 e resolve parte do mesmo problema — fazer primeiro |
| 13 | Integração Ideal Tracker → Dimensão 11 (GEO/Citação) | RN-SGA-10 | GEO | Direção já confirmada pelo PO — resolve o gargalo do princípio 5 (loop fechado) com o menor esforço técnico, a métrica já existe pronta |
| 14 | Ofensiva de autoridade/backlink (prospecção, não só disavow) | RN-SGA-09 | SEO | Mais transformador dos itens de SEO, mas o mais caro (2-3 trimestres) — muda a Dimensão 8 de reativa para propositiva |
| 15 | Autoridade de entidade — `sameAs` no schema + presença fora do site | **RN-SGA-14** | GEO | `[NOVO]` Base barata (schema) + presença off-site cara — pode começar pela parte barata |
| 16 | Presença off-site (Reddit, fóruns, reviews) | — (sem RN ainda) | GEO | Mudança de escopo mais estrutural — desloca o produto de "auditor de site" para "auditor de reputação de marca fora do site"; exige decisão de escopo antes de virar RN |
| 17 | Medir "sou a resposta escolhida" em assistente de voz | — (sem RN ainda) | AEO | Mais especulativo do cofre inteiro — viabilidade técnica não confirmada; não priorizar até essa dependência ser resolvida |

**Segmentação de tráfego de origem IA** (GA4/Motor de Percepção,
**RN-SGA-11**) fica **fora desta fila de propósito** — não é item de
conteúdo/técnica SEO/GEO/AEO, é ajuste de mensuração do Motor de Percepção;
está no Track F de [[03-Produtos/growth-machine/plano-fechamento-prd-v2]].

## O que fica deliberadamente de fora desta fila
- **Hipótese "template de conteúdo como impulsionador e ofensor de
  red-flag"** — discutida em paralelo, mas ainda é hipótese não validada;
  não entra em fila de priorização até virar achado confirmado.
- **Core updates específicos além de Helpful Content System e E-E-A-T** —
  não documentados no cofre ainda; qualquer novo update precisa entrar
  primeiro na tabela de Tendências de Busca 2026 antes de gerar princípio
  ou item de fila aqui.

## Notas relacionadas
- [[03-Produtos/growth-machine/validacao-fluxos-principios]] — validação de fluxo que motivou esta reescrita (2026-07-10)
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] — decisão formal do item 1 da fila
- [[04-Decisões/adr-camada-calibracao-continua]] — mecanismo do princípio 5 generalizado
- [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] — origem dos achados F-30 a F-40
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — todas as RN-SGA-* citadas na fila
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] — origem do diagnóstico por pilar (scores, lacunas individuais, tendências 2026)
- [[01-Ideias/anti-praticas-seo-growth-excellence]] — origem da regra de meta/title e das anti-práticas cruzadas
- [[03-Produtos/growth-machine]] — produto ao qual todos os itens da fila se aplicam
- [[03-Produtos/ideal-tracker]] — produto-fonte da métrica de GEO (item 13 da fila)
- [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]
- [[00-Painel-Estado]] · [[00-Cerebro]]
