---
tipo: produto
status: vivo
criado: 2026-07-06
ultima-revisao: 2026-07-06
tags: [growth-machine, seo, geo, aeo, principios, roadmap]
---

# Princípios-núcleo SEO/GEO/AEO — por que cada resolução foi priorizada

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
- Já explícito nos prompts de conteúdo do MPI Plus e auditado na
  Dimensão 2 — é o critério mais alinhado ao Google hoje entre os três
  pilares, porque é aplicado desde a geração do conteúdo, não só na
  auditoria posterior.
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
  tráfego + 20% leads) e onde GEO/AEO falha por completo — nenhuma métrica
  de citação ou de "resposta escolhida" compõe nota nenhuma hoje.
- **Por que este é o gargalo mais repetido em toda a documentação:** sem
  esse loop, GEO/AEO não tem como provar progresso nem regressão — é o
  motivo direto pelo qual a integração com [[03-Produtos/ideal-tracker]]
  aparece como "maior alavancador único" no comparativo de maturidade: não
  é a ideia mais sofisticada, é a que resolve o gargalo mais estrutural
  com o menor esforço (a métrica já existe, só não está plugada).

### 6. Alinhamento com sistemas do Google nomeados explicitamente
- **Helpful Content System** — qualidade do domínio inteiro é avaliada,
  não só página a página; conteúdo fraco acumulado arrasta o resto.
- **E-E-A-T reforçado em YMYL** — já coberto no princípio 3.
- **Por quê só estes dois:** são os únicos sistemas/atualizações do Google
  citados com nome próprio em toda a documentação já validada do cofre até
  agora ([[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]],
  tabela de Tendências de Busca 2026). Qualquer novo core update ou
  percepção de mercado deve entrar primeiro nessa tabela de tendências,
  com data e fonte, antes de virar princípio aqui — evita basear decisão
  de produto em achismo de mercado sem registro.

## Onde cada pilar está hoje (e por que a régua é diferente)

| Pilar | Score | Por que a régua não é a mesma dos outros dois |
|---|---|---|
| SEO tradicional | ~75-80% | Auditoria comparativa contra concorrentes reais (Dimensão 2), 10 dimensões cobrindo o site inteiro — regra madura, é polimento |
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

| Ordem | Ideia | Pilar(es) | Por que essa posição |
|---|---|---|---|
| 1 | Poda de conteúdo — ajustar RN-84 de bloqueio total para sugestão de candidata, com scoring (baixo tráfego + baixa relevância + sem backlink) | SEO | Mais rápido (2-3 sprints), sem infraestrutura nova, e resolve uma contradição direta e já identificada contra o Helpful Content System — é a única lacuna onde o produto hoje faz o oposto do que a boa prática pede |
| 2 | Priorização de AEO por nicho — pesar a régua AEO conforme o nicho do cliente (local/prático vs. B2B complexo) | AEO | Mais barato de todos (1 sprint) — reaproveita a segmentação de nicho que o briefing já coleta, é decisão de produto, não capability nova |
| 3 | Meta description ≤160 / title ≤60 como checagem determinística em 2C | SEO + AEO | Regra já validada externamente (evento Growth Excellence), barata de implementar, e serve dois pilares ao mesmo tempo — reduz truncamento (SEO) e aumenta chance de virar resposta direta em snippet (AEO) |
| 4 | Extrabilidade de bloco — cada seção responde sozinha, sem depender do parágrafo anterior | GEO + AEO | Mesma base de prompt/checagem serve as duas frentes; separado, seria esforço redundante — 1-2 trimestres |
| 5 | Accessibility tree + Cumulative Layout Shift (2 dos 6 pilares agênticos) | GEO | Reaproveita Core Web Vitals já existente (Dimensão 5) — 2 de 6 pilares agênticos cobertos a baixo custo |
| 6 | Log de crawler real (bots de IA + Googlebot) — confirmar visita real, não só permissão declarada | SEO + GEO | Mais caro (depende de acessar log de servidor por cliente), mas resolve uma lacuna de SEO e de GEO com a mesma infraestrutura — não vale fazer separado |
| 7 | Integração Ideal Tracker → aba GEO do projeto | GEO | Direção já confirmada pelo PO (ver [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]) — resolve o gargalo do princípio 5 (loop fechado) com o menor esforço técnico relativo ao ganho, porque a métrica já existe pronta |
| 8 | WebMCP — form coverage, tools registered, schemas válidos | GEO | Mais caro e mais incerto dos pilares agênticos — depende do site do cliente implementar um protocolo ainda emergente, fora do controle direto do Growth Machine (ver [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]) |
| 9 | Ofensiva de autoridade/backlink (prospecção, não só disavow) | SEO | Mais transformador dos itens de SEO, mas o mais caro (2-3 trimestres) — muda a Dimensão 8 de reativa para propositiva |
| 10 | Presença off-site (Reddit, fóruns, reviews) | GEO | Mudança de escopo mais estrutural de todas — desloca o produto de "auditor de site" para "auditor de reputação de marca fora do site"; deixado por último de propósito, não por baixa importância, mas por exigir decisão de escopo maior antes de virar backlog |
| 11 | Medir "sou a resposta escolhida" em assistente de voz | AEO | Mais especulativo do cofre inteiro — depende de viabilidade técnica de consultar assistentes de voz programaticamente, ainda não confirmada; não priorizar até essa dependência ser resolvida |

## O que fica deliberadamente de fora desta fila
- **Hipótese "template de conteúdo como impulsionador e ofensor de
  red-flag"** — discutida em paralelo, mas ainda é hipótese não validada;
  não entra em fila de priorização até virar achado confirmado.
- **Core updates específicos além de Helpful Content System e E-E-A-T** —
  não documentados no cofre ainda; qualquer novo update precisa entrar
  primeiro na tabela de Tendências de Busca 2026 antes de gerar princípio
  ou item de fila aqui.

## Notas relacionadas
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] — origem do diagnóstico por pilar (scores, lacunas individuais, tendências 2026)
- [[01-Ideias/anti-praticas-seo-growth-excellence]] — origem da regra de meta/title e das anti-práticas cruzadas
- [[03-Produtos/growth-machine]] — produto ao qual todos os itens da fila se aplicam
- [[03-Produtos/ideal-tracker]] — produto-fonte da métrica de GEO (item 7 da fila)
- [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]]
- [[00-Cerebro]]
