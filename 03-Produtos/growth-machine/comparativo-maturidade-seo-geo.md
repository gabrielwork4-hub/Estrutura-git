---
tipo: produto
status: vivo
criado: 2026-07-03
ultima-revisao: 2026-07-03
tags: [growth-machine, seo, geo, aeo, maturidade, comparativo]
---

# Comparativo de Maturidade SEO vs. GEO/AEO — Growth Machine

> Nota viva, evolutiva — atualizar sempre que houver progresso real (não
> planejado) em qualquer um dos pilares. Não é compromisso de roadmap, é
> **termômetro**: onde estamos agora vs. onde seria o ideal. Fonte da
> primeira leitura: [[03-Produtos/growth-machine/avaliacao-fluxo]], bloco
> "Alinhamento SEO/GEO/AEO com práticas atuais do Google".

## Score atual (2026-07-03)

| Pilar | Score | Leitura |
|---|---|---|
| **SEO tradicional** | **~75-80%** | Avançado — auditoria técnica completa, anti-canibalização, E-E-A-T como princípio, governança séria |
| **GEO/AEO (busca generativa)** | **~25-30%** | Fundação existe (estrutura de conteúdo, dados estruturados), mas sem loop de mensuração |
| **Combinado** | **~55-60%** | Puxado pra cima pelo SEO, pra baixo pelo GEO |

## Por que SEO tradicional está avançado
- Auditoria técnica completa: 10 dimensões cobrindo conteúdo, arquitetura, performance, schemas, indexabilidade, sinais externos, infra, leads.
- Anti-canibalização + arquitetura em silo — alinhado com "topical authority", que é o que o Google mais recompensa hoje.
- E-E-A-T como princípio explícito nos prompts, não decoração.
- Governança séria: aprovação humana obrigatória (RN-47), validação por IA pós-execução (RN-81), versionamento de regras (RN-122).

**O que falta pro 100%:** ajustes de afinação, não reconstrução — calibração de thresholds sem origem documentada, cadência de 6 meses (RN-59) possivelmente lenta, cotas de ferramentas talvez subdimensionadas para 2.500 clientes. Ver itens de backlog médios já abertos.

## Por que GEO/AEO está atrasado

| O que teria numa versão ideal | O que existe hoje |
|---|---|
| Métrica de citação em LLM compondo a nota do cliente | Índice de Performance é 100% SEO tradicional (posicionamento/tráfego/leads) — zero peso de GEO |
| Medir se a IA realmente cita o site | Só verifica se o arquivo AI Instructions/LLM.txt **existe** (RN-82), não se funciona |
| Sinal de autoridade de entidade (Knowledge Graph) | Inexistente |
| Conteúdo estruturado para ser citável em resposta de IA | Existe (Dimensão 2C) — único pilar realmente maduro de GEO hoje |
| Rastreamento de tráfego vindo de IA (ChatGPT, Perplexity) | Inexistente — GA4 só olha orgânico tradicional |
| Loop fechado (medir → ajustar → remedir citação) | Não existe — métrica mora isolada no [[03-Produtos/ideal-tracker]], sem conexão |

## Leitura estrutural
Não é "faltam X% de funcionalidades" — é mais de fundo: o Growth Machine
foi desenhado como sistema de SEO que ganhou um verniz de GEO (Dimensão
2C, RN-82), não desenhado do zero pensando nos dois igualmente. Normal
para um PRD escrito antes de GEO virar prioridade de mercado — mas
significa que fechar a distância não é "adicionar uma feature", é decidir
se GEO vira **pilar de primeira classe** (peso próprio no Índice, métrica
própria, ferramenta própria) ou continua complemento dentro do SEO.

## Maior alavancador único identificado
Conectar o [[03-Produtos/ideal-tracker]] ao Growth Machine — é o atalho
mais barato, porque a métrica de GEO que falta **já existe pronta** em
outro produto do mesmo cofre, só não está ligada. Ver
[[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]].

---

## 3 Lacunas de Pensamento — SEO (2026-07-03)

> Diferente das lacunas operacionais já mapeadas (calibração de
> thresholds, cadência, cotas) — estas são lacunas de **estratégia SEO**:
> faltam no desenho do produto, não na execução dele.

### Lacuna 1 — RN-84 bloqueia poda de conteúdo, que hoje é boa prática reconhecida

**O que temos hoje:** RN-84 diz explicitamente: "o sistema nunca sugere
remover páginas, exceto quando o CS informa pedido explícito do cliente."

**Caminho ideal:** Desde que o Google formalizou o Helpful Content System,
"poda de conteúdo" (remover/consolidar páginas finas, desatualizadas ou
que nunca performaram) virou prática reconhecida — conteúdo ruim acumulado
arrasta a qualidade percebida do domínio inteiro, prejudicando até as
páginas boas.

**Tradução prática:** O sistema deveria **identificar candidatas a poda**
(baixo tráfego + baixa relevância + sem backlink + conteúdo fino) e
**sugerir ao analista**, que decide — hoje ele nem chega a sugerir.

**Estimativa:** Ajuste de RN-84 + lógica de scoring de "candidata a poda"
na Dimensão 2. **2–3 sprints**, sem dependência de infraestrutura nova.

### Lacuna 2 — Sem análise de crawl budget / log file, só sitemap declarado

**O que temos hoje:** Dimensão 7 audita se sitemap.xml/robots.txt existem,
estão corretos e sem conflito — o que o site **diz** que quer que o
Google rastreie.

**Caminho ideal:** SEO técnico avançado em escala (2.500 sites) audita o
que o Googlebot **realmente** rastreia via log de servidor — revela
páginas importantes nunca visitadas, orçamento de crawl desperdiçado,
frequência real de recrawl.

**Tradução prática:** Hoje o sistema audita a intenção declarada, não o
comportamento real do crawler.

**Estimativa:** Item mais caro dos 3 — precisa de acesso a log de servidor
por cliente (nem sempre disponível), processamento em escala, nova
sub-dimensão dentro da Dim 7 ou 9. **1–2 trimestres**, com dependência de
negociar acesso a dado que o produto hoje nem pede.

### Lacuna 3 — Só defesa (disavow), nenhuma ofensiva de autoridade/backlink

**O que temos hoje:** Dimensão 8 só detecta backlinks tóxicos para
desativar (disavow, sempre com revisão humana) — 100% postura defensiva.

**Caminho ideal:** Backlink de qualidade continua entre os fatores de
ranqueamento mais fortes — a régua ideal também sugere oportunidades de
construção de autoridade (domínios relevantes sem link ainda, menções não
linkadas, PR digital), não só limpa o que é ruim.

**Tradução prática:** O sistema só reage a ameaça, sem função propositiva
de ganho de autoridade — justamente a ação de mais alto impacto e mais
difícil de escalar manualmente.

**Estimativa:** Requer nova fonte de dado (ferramenta de backlink gap em
modo prospecção) + agente de IA novo (Dim 8 expandida ou dimensão nova).
**2–3 trimestres** — o mais estrutural dos 3, muda o papel da Dim 8 de
reativa para proativa.

### Tempo total estimado — SEO "literalmente ideal"
Somando as 3 lacunas (baixa dependência entre si, não 100% paralelizáveis):
**6–9 meses** de produto+dev. Lacuna 1 (poda de conteúdo) é o ganho mais
rápido e barato; Lacuna 3 (ofensiva de autoridade) é o mais transformador.

---

## 3 Lacunas de Pensamento — GEO (Generative Engine Optimization, 2026-07-03)

> SEO otimiza pra aparecer na lista de resultados; GEO otimiza pra ser o
> trecho que a IA copia e cola na resposta dela. Objetivo diferente, muda
> o que "boa prática" significa.

### Lacuna 1 — Conteúdo estruturado pra ranquear ≠ conteúdo estruturado pra ser extraído

**O que temos hoje:** Dimensão 2C cobre "estrutura para mecanismos
generativos, FAQ, headings, resumo objetivo, entidades relevantes" — bom
passo, mas ainda pensa em página, não em trecho extraível.

**Caminho ideal:** LLMs não citam a página inteira — extraem blocos
autocontidos: um parágrafo que responde a pergunta sozinho, sem depender
do contexto ao redor. "Resposta direta nas primeiras linhas, depois
aprofundamento" — o oposto de muito conteúdo SEO clássico, que enrola a
resposta pra aumentar tempo de leitura/scroll.

**Tradução prática:** Falta checagem de **extrabilidade** — se cada seção
consegue responder sozinha a uma pergunta específica, sem precisar do
parágrafo anterior. Diferente de "tem FAQ" — é sobre a escrita de cada
bloco, não só a presença de uma seção de perguntas.

**Estimativa:** Agente/prompt novo dedicado — avaliação qualitativa de
escrita, não dá pra estender checagem determinística existente.
**1–2 trimestres.**

### Lacuna 2 — Não sabemos se os crawlers de IA sequer estão visitando o site

**O que temos hoje:** RN-82 verifica se **existe** AI Instructions/LLM.txt
— presença, não uso real.

**Caminho ideal:** Cada motor generativo tem crawler com user-agent
próprio (GPTBot, PerplexityBot, ClaudeBot, Google-Extended). Prática
correta: (1) confirmar que robots.txt não bloqueia esses bots sem querer,
e (2) confirmar via log de servidor que eles de fato visitam o site — ter
o arquivo certo não significa nada se o bot nunca passou por lá.

**Tradução prática:** Mesmo tipo de lacuna da Lacuna 2 de SEO (log de
servidor), aplicada a bots de IA em vez do Googlebot — faz sentido
resolver as duas juntas, é a mesma infraestrutura de dado.

**Estimativa:** Parte de permissão (robots.txt) é barata — estende o
Módulo Sentinela, que já roda diário. Parte de confirmação real (log)
depende da mesma infraestrutura da Lacuna 2 de SEO. Bundle: **1
trimestre** se feito junto com o log de servidor.

### Lacuna 3 — O produto só audita o site do cliente, nunca a presença dele fora do próprio domínio

**O que temos hoje:** Todas as 10 dimensões auditam o site do cliente.
Nenhuma olha para fora dele.

**Caminho ideal:** Motores generativos frequentemente preferem citar
fontes de terceiros percebidas como neutras — Reddit, fóruns
especializados, Quora, reviews, Wikipedia — em vez do site institucional
da própria marca, visto como "parcial" por natureza. GEO maduro inclui
monitorar e influenciar essa presença fora do site.

**Tradução prática:** Mudança de escopo mais estrutural das 3 — desloca a
pergunta de "meu site está bom?" para "minha marca está bem representada
onde as IAs realmente confiam?".

**Estimativa:** Exige fonte de dado nova (monitoramento de menção/presença
off-site) — capability nova do zero, não extensão de nada existente.
**2–3 trimestres**, o mais caro e mais estratégico dos 3.

### Tempo total estimado — GEO "literalmente ideal"
**6–10 meses**, com boa parte da Lacuna 2 podendo ser resolvida junto com
a Lacuna 2 de SEO (mesma infraestrutura de log). A Lacuna 3 é a que muda o
produto de forma mais profunda — sai de "auditor de site" para "auditor de
reputação de marca em fontes de IA".

**Nota importante:** mesmo em número de meses parecido com SEO, GEO parte
de uma base muito mais baixa (25-30% vs. 75-80%) — em termos absolutos,
fechar GEO exige praticamente reconstruir uma capability nova do zero,
enquanto SEO é polimento de algo já maduro.

---

## Histórico de leituras
| Data | Score SEO | Score GEO/AEO | Combinado | O que mudou |
|---|---|---|---|---|
| 2026-07-03 | ~75-80% | ~25-30% | ~55-60% | Leitura inicial — baseline |

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[03-Produtos/growth-machine/cheat-sheet]]
- [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
- [[03-Produtos/ideal-tracker]]
