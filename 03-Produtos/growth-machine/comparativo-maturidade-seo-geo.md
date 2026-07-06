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

## Score atual (revisado em 2026-07-06)

| Pilar | Score | Leitura |
|---|---|---|
| **SEO tradicional** | **~75-80%** | Avançado — auditoria técnica completa, anti-canibalização, E-E-A-T como princípio, governança séria |
| **GEO/AEO (busca generativa)** | **~20-25%** | Fundação existe (estrutura de conteúdo, dados estruturados), mas sem loop de mensuração — revisado pra baixo após detalhar os 6 pilares agênticos (Growth Machine cobre só 1 de 6) |
| **Combinado** | **~50-55%** | Puxado pra cima pelo SEO, pra baixo pelo GEO |

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

### Lacuna 2 — Não sabemos se os crawlers de IA sequer estão visitando o site (Pilares Agênticos)

**O que temos hoje:** RN-82 verifica se **existe** AI Instructions/LLM.txt
— presença, não uso real. Nenhuma outra checagem de "agentic readiness"
existe no Growth Machine.

**Caminho ideal — os 6 pilares agênticos (categoria "Agentic Browsing" do
Lighthouse):** essa lacuna é mais concreta e ampla do que só "o crawler
visita o site" — é sobre se um **agente de IA consegue navegar e interagir
de verdade** com o site (ler, preencher formulário, usar ferramenta), não
só "ler pra citar". Os 6 pilares auditados hoje pelo Lighthouse:

1. **Accessibility tree is well-formed** — a árvore de acessibilidade
   precisa estar bem formada para um agente "enxergar" a estrutura da
   página corretamente.
2. **Cumulative Layout Shift (CLS)** — instabilidade visual atrapalha
   também a leitura/interação de um agente, não só a experiência humana.
3. **WebMCP form coverage** — cobertura de formulários expostos via
   protocolo WebMCP, pra agente conseguir preencher/submeter.
4. **WebMCP tools registered** — ferramentas da página registradas via
   WebMCP, pra agente conseguir invocar ações do site diretamente.
5. **WebMCP schemas are valid** — os schemas WebMCP registrados precisam
   ser válidos para o agente interpretar corretamente o que pode fazer.
6. **llms.txt** — mesmo arquivo já coberto (parcialmente) pela RN-82.

Além disso, cada motor generativo tem crawler com user-agent próprio
(GPTBot, PerplexityBot, ClaudeBot, Google-Extended) — prática correta
complementar: (1) confirmar que robots.txt não bloqueia esses bots sem
querer, e (2) confirmar via log de servidor que eles de fato visitam o
site.

**Tradução prática:** O Growth Machine hoje cobre só 1 dos 6 pilares
(llms.txt, e só a presença dele, via RN-82) — os outros 5 (accessibility
tree, CLS, os 3 critérios de WebMCP) são **ausência total**. WebMCP em
particular é uma capability nova que não existe em nenhuma dimensão —
não é ajuste de regra existente, é uma frente inteira nova.

**Estimativa:** CLS já é medido indiretamente via Core Web Vitals
(Dimensão 5) — reaproveitável. Accessibility tree exige nova checagem
determinística (existem ferramentas prontas, tipo axe-core). WebPCP (os
3 critérios) é o mais caro — depende de o site do cliente sequer
implementar o protocolo, o que hoje não é nem cobrado no processo de
entrega/dev do site. Confirmação real de crawler via log de servidor
segue como no rascunho original: parte de permissão (robots.txt) é barata
— estende o Módulo Sentinela; parte de confirmação real (log) depende da
mesma infraestrutura da Lacuna 2 de SEO. **Bundle total: 1–2 trimestres**,
com WebMCP como a parte mais incerta (depende de adoção de protocolo
ainda emergente, não só de auditoria).

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

## 3 Lacunas de Pensamento — AEO (Answer Engine Optimization, 2026-07-03)

> A régua mais estreita das três: SEO otimiza pra aparecer numa lista;
> GEO otimiza pra ser citado dentro de uma resposta mais longa; AEO
> otimiza pra **ser a resposta direta** — assistente de voz, chat, caixa
> de resposta instantânea, onde não tem lista, tem uma única resposta
> escolhida.

### Lacuna 1 — Nenhuma auditoria de formato "resposta única, sem ambiguidade"

**O que temos hoje:** Dimensão 2C trata FAQ como um bloco de conteúdo
entre outros — não pensa em "qual é **a** resposta certa, numa frase, sem
depender de contexto nenhum".

**Caminho ideal:** Assistentes de voz e caixas de resposta direta (Google
Featured Snippet no modo pergunta-resposta, Alexa, Siri, Google Assistant)
escolhem uma única fonte pra responder — não citam múltiplas, não
sintetizam várias visões como um LLM de chat faz. A prática ideal é ter,
pra cada pergunta relevante do nicho, uma resposta de 1 frase objetiva e
inequívoca, sem "depende", isolada num bloco que consiga ser lida sozinha.

**Tradução prática:** Mais rígido que a "extrabilidade" de GEO — ali o LLM
pode adaptar/parafrasear o trecho; aqui a resposta muitas vezes é lida
literalmente, palavra por palavra.

**Estimativa:** Extensão direta da Lacuna 1 de GEO — dá pra fazer junto,
com checagem mais rígida em cima da mesma base. **1 trimestre**, se feito
em conjunto com a Lacuna 1 de GEO; sozinho, teria custo redundante.

### Lacuna 2 — Sem dado nenhum de "estou sendo a resposta escolhida" (nem por engano)

**O que temos hoje:** Nenhuma dimensão mede se o cliente já é a resposta
única em algum assistente de voz/caixa de resposta hoje.

**Caminho ideal:** Monitorar periodicamente um conjunto de perguntas
relevantes do nicho contra os principais assistentes (Google
Assistant/Gemini, Alexa, Siri) e caixas de resposta direta do Google,
registrando quem é a fonte escolhida — cliente, concorrente, ou ninguém.

**Tradução prática:** É a métrica mais "de resultado" das três frentes e a
mais ausente de todas — nem existe versão embrionária dela em lugar
nenhum do cofre (diferente de GEO, que ao menos tem o Ideal Tracker
medindo SoV em LLM de chat).

**Estimativa:** Item mais caro e especulativo dos 3 — depende de
automação de consulta a assistentes de voz (tecnicamente mais difícil que
LLM de chat, que tem API) e de cobertura de mercado. **3+ trimestres**,
com risco real de inviabilidade técnica dependendo do assistente.

### Lacuna 3 — Nenhuma priorização de nicho/vertical onde AEO já é decisivo

**O que temos hoje:** O sistema trata todos os ~2.500 clientes com a
mesma régua, independente do quanto AEO importa pro nicho deles.

**Caminho ideal:** AEO já é decisivo em nichos específicos — "onde
encontro X perto de mim", "qual o telefone de Y", "como faço Z" (nichos
locais, serviços, dúvidas práticas) viram resposta de voz/assistente. Em
nichos B2B complexos, isso importa muito menos.

**Tradução prática:** Investir a mesma régua de AEO em todos os 2.500
clientes é ineficiente — a prática ideal prioriza AEO só onde o
comportamento de busca do nicho realmente passa por assistente/resposta
única.

**Estimativa:** Não é funcionalidade nova, é **regra de priorização** —
praticamente grátis tecnicamente, mas exige decisão de produto. **1
sprint** de definição + reaproveita a segmentação de nicho que o briefing
já coleta.

### Tempo total estimado — AEO "literalmente ideal"
**4–6 meses**, mais barato em tempo que SEO e GEO — mas o mais incerto dos
três, porque a Lacuna 2 esbarra em limitação técnica real de acesso a
dado, não só em esforço de engenharia.

---

## Panorama fechado das 3 frentes

| Frente | Base atual | Tempo p/ ideal | Maior risco |
|---|---|---|---|
| SEO | ~75-80% | 6–9 meses | Nenhum — é polimento |
| GEO | ~25-30% | 6–10 meses | Depende de negociar acesso a log de servidor com clientes |
| AEO | Não medido (mais baixo que GEO) | 4–6 meses | Viabilidade técnica de consultar assistentes de voz programaticamente |

**Ordem de prioridade recomendada, se fosse decidir hoje:** SEO (Lacuna 1,
poda de conteúdo) → GEO+AEO Lacuna de log/crawler de IA (bundle) → GEO
Lacuna 1 (extrabilidade, reaproveitada pra AEO Lacuna 1) → o resto,
conforme prioridade de negócio.

---

## Tendências de Busca 2026 × Growth Machine Atual

> Cruzamento entre o que hoje se reconhece como tendência ativa de busca
> (SEO/GEO/AEO combinados) e o quanto o Growth Machine já cobre cada uma.
> Serve de checklist rápido — se uma tendência nova aparecer, ela entra
> como linha nova aqui antes de virar dimensão/RN formal.

| Tendência de busca 2026 | O que significa na prática | Cobertura no Growth Machine | Gap |
|---|---|---|---|
| **AI Overview como "posição zero"** | Resposta gerada por IA no topo da SERP, antes de qualquer link orgânico — captura clique antes mesmo do usuário rolar a página | Dimensão 2C estrutura conteúdo pra isso, mas não mede se está sendo citado | Sem métrica de citação (ver Lacuna GEO 1 do score geral) |
| **Zero-click search em crescimento** | Usuário obtém resposta sem clicar em nenhum link — tráfego orgânico tradicional cai mesmo com boa posição | Índice de Performance ainda mede só tráfego/clique | Sem métrica de "visibilidade sem clique" (impressão/citação) |
| **Diversificação de crawlers de IA** (GPTBot, PerplexityBot, ClaudeBot, Google-Extended) | Cada motor generativo rastreia com bot próprio, permissões distintas no robots.txt | RN-82 só checa presença de LLM.txt | Sem monitoramento de acesso real desses bots (GEO Lacuna 2) |
| **Conteúdo "resposta-primeiro" (answer-first)** | Resposta direta nas primeiras linhas, sem enrolação, pra ser extraível por IA | Dimensão 2C cobre estrutura geral, não o padrão de escrita por bloco | Sem checagem de extrabilidade (GEO Lacuna 1 / AEO Lacuna 1) |
| **Busca por voz/assistente em nichos locais e práticos** | "Onde encontro X perto de mim" já responde direto por assistente, sem lista de resultados | Cluster GEO local já existe no prompt de keywords do MPI Plus | Sem priorização por nicho nem medição de "sou a resposta" (AEO Lacuna 2/3) |
| **Helpful Content System penaliza conteúdo raso acumulado** | Qualidade do domínio inteiro é avaliada, não só página a página — conteúdo fraco arrasta o resto | RN-84 proíbe sugerir remoção de página | Contradiz a tendência diretamente (SEO Lacuna 1) |
| **Crawl budget cada vez mais escasso em sites grandes** | Google (e bots de IA) não rastreiam tudo — prioriza o que já demonstrou valor | Dimensão 7 audita sitemap/robots declarado, não comportamento real | Sem análise de log de servidor (SEO Lacuna 2) |
| **E-E-A-T mais rígido, principalmente YMYL** | Sinais de experiência/autoridade/confiança pesam mais a cada atualização de algoritmo | Já é princípio explícito nos prompts de conteúdo do MPI Plus | Coberto — ponto forte já reconhecido |
| **Dados estruturados como "API" de leitura para IA** | Schema.org/JSON-LD vira a forma mais confiável de uma IA extrair fato certo, não só rich snippet | Dimensão 6 audita Schema com regra anti-spam | Coberto — ponto forte já reconhecido |
| **Prova social fora do site (Reddit, fóruns, reviews)** | IA generativa cita fontes percebidas como neutras mais que o site institucional da marca | Nenhuma dimensão audita presença fora do domínio do cliente | Ausente (GEO Lacuna 3) |
| **Busca conversacional multi-turno** | Usuário refina a pergunta em vários turnos com o mesmo assistente/chat, contexto acumulado | Fora do escopo de qualquer dimensão — GM audita site estático, não conversa | Ausente, não mapeado como lacuna formal ainda |
| **Personalização de resposta por contexto do usuário** | LLM ajusta resposta com base em localização/histórico/dispositivo do usuário, não só na query | Fora do escopo do GM — decisão de produto do próprio motor de busca, não do site | Fora de controle do produto, apenas observar |

---

## Histórico de leituras
| Data | Score SEO | Score GEO/AEO | Combinado | O que mudou |
|---|---|---|---|---|
| 2026-07-03 | ~75-80% | ~25-30% | ~55-60% | Leitura inicial — baseline |
| 2026-07-03 | ~75-80% | ~25-30% (AEO não medido, mais baixo) | ~55-60% | Adicionadas as 3 lacunas de pensamento por frente (SEO/GEO/AEO), tempo estimado pra "literalmente ideal" de cada uma, e tabela de Tendências de Busca 2026 x Growth Machine. Nenhuma mudança de score ainda — é aprofundamento de diagnóstico, não progresso real. |
| 2026-07-06 | ~75-80% | ~20-25% (revisado pra baixo) | ~50-55% | GEO Lacuna 2 detalhada com os 6 pilares agênticos reais (Lighthouse "Agentic Browsing"): accessibility tree, CLS, WebMCP form coverage/tools/schemas, llms.txt. Growth Machine cobre só 1 de 6 (llms.txt, parcial). Score de GEO revisado pra baixo porque a lacuna é maior/mais concreta do que o rascunho original sugeria — WebMCP é capability nova ausente por completo. |

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[03-Produtos/growth-machine/cheat-sheet]]
- [[01-Ideias/growth-machine-geo-aeo-oportunidades]]
- [[03-Produtos/ideal-tracker]]
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]] — item de backlog formal para cobrir os 6 pilares agênticos (Agentic Browsing/WebMCP)
