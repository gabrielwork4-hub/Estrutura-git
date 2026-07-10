---
tipo: cerebro
status: vivo
criado: 2026-06-30
ultima-revisao: 2026-06-30
tags: [core]
---

# Cérebro — Estrutura-Git

> Esta é a nota raiz do cofre. Toda leitura do vault (humana ou de IA) deve
> começar por aqui. Ela é a fonte de verdade da ideia inicial e do
> funcionamento geral — tudo o resto do cofre existe para detalhar,
> ajustar ou contestar o que está escrito aqui.
>
> Leitura complementar recomendada para quem chega agora: [[00-Glossario]]
> (jargão do cofre), [[00-Painel-Estado]] (snapshot de onde cada coisa
> está) e [[03-Produtos/mapa-dependencia-produtos]] (quem depende de quem
> e ordem de prioridade).

## Ideia inicial
Este cofre existe para resolver **perda de contexto entre reuniões e
decisões**: ideias, ajustes de fluxo e decisões de produto se perdiam
espalhadas entre Notion, Drive, WhatsApp e reuniões, sem um lugar único que
amarrasse tudo e explicasse o porquê de cada mudança.

Tem duas visões de uso, não excludentes:
1. **Base de conhecimento para IA (RAG)** — alimentar assistentes de IA com
   contexto estruturado e confiável sobre produtos, fluxos e decisões, sem
   depender de o humano lembrar/repetir contexto a cada conversa.
2. **Ferramenta pessoal de raciocínio do PO** — espaço para pensar, avaliar
   criticamente (ver [[03-Produtos/growth-machine/avaliacao-fluxo]] como
   exemplo do formato) e estruturar decisões antes de levar ao time.

Não é, por enquanto, pensado como fonte de verdade formal para o time
técnico consultar diretamente — as histórias/prompts que nascem aqui viram
input para Jira/dev, mas o cofre em si é o espaço de elaboração do PO.

## Funcionamento
O fluxo real, validado nesta sessão, é:

```
Reunião / transcrição (Notion, WhatsApp, Drive)
        │
        ▼
Vira nota no cofre (ideia, fluxo, produto ou decisão)
        │
        ▼
Cruzamento com documentação existente (PRD, Drive, prompts em produção)
        │
        ▼
Avaliação crítica (pontos fortes/riscos) quando aplicável
        │
        ▼
Vira item de 05-Backlog ou história pronta para Jira/DEV
        │
        ▼
00-Cerebro.md é atualizado com o link (nunca fica órfão)
```

Não é um processo fechado/formal ainda — está sendo descoberto e ajustado
à medida que o cofre é usado. O padrão acima é o que já se repetiu de forma
consistente (ex: estudo de keywords, PRD do Growth Machine, prompts do MPI
Plus) e deve ser tratado como o funcionamento de referência até que mude.

## Fluxos ativos
Lista dos fluxos centrais em operação, linkados para [[02-Fluxos]].
- [[02-Fluxos/estudo-de-keywords]] — como o estudo de keywords deve pensar clusterização, evitar canibalização e tratar variações locais.
- [[02-Fluxos/processo-kickoff-discovery]] — kick-off → discovery (2 semanas) → aprovação de documentação → quebra de backlog.
- [[02-Fluxos/prompt-avaliacao-keywords]] — v1/v2 registrados como histórico; **v3 é a versão oficial** (2026-07-01): Estudo SEO clusterizado com silo semântico, teste explícito de anti-canibalização e dados estimados rotulados como qualitativos.

## Problemáticas atuais
Problemas identificados nos fluxos que ainda não viraram itens de backlog, ou que são recorrentes o suficiente para ficar visíveis aqui.
- Estudo de keywords partia direto da keyword isolada, sem clusterizar por intenção, gerando risco de canibalização entre páginas e variações locais tratadas fora do cluster. Ajustado em [[02-Fluxos/estudo-de-keywords]].

## Backlog gerado
Itens de [[05-Backlog]] que nasceram de problemas listados acima.
- [[05-Backlog/ideal-track-definir-metodologia-sov]] — metodologia de medição do Share of Voice ainda indefinida no MVP do Ideal Track.
- 10 itens derivados da avaliação crítica do PRD do Growth Machine (ver [[03-Produtos/growth-machine/avaliacao-fluxo]]), priorizados pela síntese executiva: [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]] (alta), [[05-Backlog/gm-atribuir-dono-prazo-questoes-abertas]] (alta), [[05-Backlog/gm-desenho-fino-prompts-agentes]] (alta), [[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]] (alta), [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]] (média), [[05-Backlog/gm-segregacao-funcoes-pontos-controle]] (média), [[05-Backlog/gm-criterio-desempate-fronteiras-componentes]] (média), [[05-Backlog/gm-escopo-sentinela-infraestrutura-cron]] (média), [[05-Backlog/gm-dimensionamento-cotas-ferramentas-externas]] (média), [[05-Backlog/gm-salvaguarda-aprovacao-massa-telas]] (baixa).
- 6 itens derivados da avaliação de alinhamento SEO/GEO/AEO (2026-07-02, ver [[03-Produtos/growth-machine/avaliacao-fluxo]] e [[01-Ideias/growth-machine-geo-aeo-oportunidades]]): [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]] (alta — **direção confirmada pelo PO em 2026-07-03**: alimentar a aba GEO do projeto com dados do Ideal Tracker), [[05-Backlog/gm-segmentar-trafego-origem-ia]] (média), [[05-Backlog/gm-sinal-conteudo-original]] (média), [[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]] (média), [[05-Backlog/gm-checagem-presenca-entidade]] (baixa), [[05-Backlog/gm-cobertura-video-como-dimensao]] (baixa).
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]] (alta, 2026-07-06) — cobrir os 6 pilares agênticos (Agentic Browsing/Lighthouse: accessibility tree, CLS, WebMCP form/tools/schemas, llms.txt); Growth Machine cobre hoje só 1 de 6. Motivou revisão do score de GEO em [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]].
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] (2026-07-06) — documento explicativo consolidando os princípios-núcleo transversais a SEO/GEO/AEO e uma fila única de prioridade (11 itens cruzando os 3 pilares), com o porquê de cada posição; matéria-prima para o template oficial de documentação em construção com o PO.
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]] (2026-07-06) — versão final de fechamento da fase de diagnóstico: diagnóstico x recomendação de desenvolvimento (oportunidades) por frente (SEO/GEO/AEO) e diagnóstico das RNs que hoje vão contra boas práticas do Google (RN-84 confirmada, RN-14/RN-59/RN-07 como candidatas não confirmadas).
- [[03-Produtos/growth-machine/briefing-lideranca-seo-geo-aeo]] (2026-07-07) — documento de embasamento para conversa com a liderança: mapa de todos os documentos-fonte, linha de raciocínio única das 3 frentes (tese, scores, decidido vs. pendente, justificativa de investimento, riscos/lacunas em aberto) e 3 perguntas de decisão a levar.
- [[03-Produtos/growth-machine/revisao-critica-prd-v1-frente-levantamento]] (2026-07-07) — frente de levantamento e questionamento (não reconciliada) sobre a Revisão Crítica externa do PRD v1.0 (29 achados, decisões do PO): F-28 confirma formalmente o gap de medição de GEO já identificado; diverge a numeração de versão do PRD (v1.0 vs. v1.9.14 citado no cofre); RNs supersedidas (21/22/23/29/32) ainda sem marcação no catálogo.
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] (2026-07-08) — avaliação de aderência da documentação atual à estrutura de PRD ideal (13 blocos) + auditoria das 122 RNs contra critérios de qualidade (atômica/testável/independente/rastreável/sem ambiguidade), cruzando vault + Drive. Diagnóstico central: doc forte no "o quê", fraca no "quem/quando/validar" — blocos ausentes são RF numerado (5), User Stories + CA (8), North Star (2) e rollout (12). Traz o esqueleto proposto da v2 e o checklist "pronto para dev" (hoje reprovado). Base direta para escrever a nova documentação.
- [[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]] (2026-07-08, **candidato a ADR**) — como ranquear por cluster/entidade/intenção sem renegociar o contrato (que vende página por keyword): usar `/informacoes` e `/artigos` (que o próprio PRD do Gregory exclui do escopo MPI) como camada editorial de cluster que envelopa e eleva a página contratada. Antídoto ao doorway/scaled content do core 2026. Estrutura-se via Dim 1 (estudo→cluster), Dim 3 (linkagem sobe p/ pilar) e Dim 2 (conteúdo).
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] (2026-07-08) — mapa que amarra cada oportunidade ao princípio-núcleo, à RN e à Dimensão que a contemplam (ou à lacuna), com a ação de estruturação (ajustar RN · criar RN · nova sub-dimensão). Estrutura-alvo: ~3 ajustes de RN (07/82/84), ~16 RNs novas (RN-123+), 2 sub-dimensões em Dim 2 (2D-AEO, 2E-E-E-A-T), 1 dimensão nova (Dim 11 GEO/Citação). Base direta para dividir as frentes no PRD v2.
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] (2026-07-08) — checklist cruzando boas práticas **Google 2026** (core updates mar/mai que punem scaled content; AI Overview derruba CTR 27%→11%) × estrutura real do **emtecorp.com.br** (DR 6, LPs por modificador, www×loja, PDFs rankeando) × regras do Gregero × Growth Machine, separada em SEO/GEO/AEO. Destaca os **padrões que a GM ainda repete** e 4 oportunidades **NOVAS** (canibalização www×loja, conteúdo preso em PDF, E-E-A-T on-page, incorporar robots-IA do Gregory).
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] (2026-07-08) — ultra-análise cruzando as **regras entregues pelo Gregory** (4 sub-PRDs: percepção/estudo/schema/robots) contra o cofre + boas práticas + core updates. **Confirma** o gate <50% da Dim 1, resolve a Q23 (posicionamento esperado = maturidade) e dá origem aos números. **Conflitos de canibalização a decidir:** pesos do índice **40/30/30 (Gregory) × 40/40/20 (nossa doc)**, colisão de numeração de RN, concatenação × QA anti-concatenação, fluxo de keywords, fonte de posicionamento (GSC × relatório MPI Plus). Nada propagado até decisão do PO.
- [[03-Produtos/growth-machine/prd-v2-mvp]] (2026-07-08) — **PRD v2.0 (MVP) consolidado**: os 13 blocos preenchidos, RF numerados (RF-00 a RF-46), User Stories/CA dos fluxos críticos, RNs reconciliadas (supersedidas, threshold Dim 1, Bright Data) e escopo SEO/GEO/AEO no nível de MVP (GEO = checklist; medição = Fase 2, F-28). Anti-canibalização por design: RNs seguem morando só no catálogo; o PRD referencia. Base para iniciar o MVP; divisões finas de SEO/GEO/AEO ficam para a sequência.

## Produtos em desenvolvimento
Linka para [[03-Produtos]] os produtos atualmente ativos. Validado contra a
pasta do Drive em 2026-06-30 (16 pastas de projeto ao todo; só os 3 abaixo
foram aprofundados até agora).
- [[03-Produtos/growth-machine]] — orquestração de SEO para ~2.500 projetos MPI, 4 fases (briefing → percepção → auditoria 10 dimensões → fila de ações no Salesforce). PRD v1.9.14 já existe no Drive.
- [[03-Produtos/mpi-plus]] — pré-requisito de carteira da Growth Machine (RN-108); refatoração de processo e palavras-chave em 3 histórias: geração de termos (**enviada ao Jira em 2026-07-03**, [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]], resolve o gargalo do fluxo), endurecimento anti-concatenação/GEO genérico (oficial, motivada por QA de produção real, [[03-Produtos/mpi-plus/historia-prompt-endurecimento-anti-concatenacao-geo]]) e arquitetura de site (oficial, aguardando envio, [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]]); sem PRD próprio encontrado no Drive ainda.
- [[03-Produtos/ideal-tracker]] (Ideal Track) — ferramenta de GEO/visibilidade em LLMs; tem PRD, doc de funcionalidades e briefing de UX no Drive, mas com pontos críticos em aberto (ver backlog acima).

## Ideias registradas
Brainstorms/oportunidades soltas em [[01-Ideias]] — não são compromisso de
roadmap, só registro para não perder a ideia.
- [[01-Ideias/growth-machine-geo-aeo-oportunidades]] — oportunidades de GEO/AEO para o Growth Machine (2026-07-02), com destaque para a integração com [[03-Produtos/ideal-tracker]] ainda não explorada.
- [[01-Ideias/anti-praticas-seo-growth-excellence]] — anti-práticas e boas práticas de SEO do evento interno Growth Excellence (2026-07-03), registradas soltas de propósito, sem linkar ainda aos PRDs/RNs dos projetos — servirá futuramente como filtro de revisão dos fluxos existentes.
- [[01-Ideias/analise-mercado-concorrencia-growth-machine]] (2026-07-06, **validada com pesquisa ativa**) — mercado de GEO é maduro e bem financiado (Profound, Peec AI, AthenaHQ, Scrunch, Otterly), diferencial do GM é integrar SEO+GEO+execução no mesmo produto; pilares agênticos (Lighthouse "Agentic Browsing", lançado em maio/2026) seguem sem concorrente comercial conhecido — espaço ainda livre.

## Outras pastas de projeto no Drive (não aprofundadas ainda)
Ideal Sync - Pix Automático BB, Auditoria Ideal, Procedimentos Depto Infraestrutura, Perfil Colaboradores, Infra Central, Ideal Sales, Ideal Multibusiness, SE - Sales Enablement, Ideal Pro, Soluções Industriais, Clínica Ideal, Projeto Matriz.

## Decisões fundadoras
Decisões em [[04-Decisões]] que moldam o funcionamento descrito aqui.
- [[04-Decisões/migracao-prompt-keywords-v2]] — substituição do prompt de avaliação de keywords (v1 → v2): saída passa de tabela de keywords avaliadas para arquitetura completa de site (Pilar → Cluster → Suporte); documenta diferenças de parâmetros e formato de saída para a equipe de tecnologia. Especificação técnica detalhada em [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]].
- [[04-Decisões/padrao-historia-jira]] — formaliza `_templates/template-historia-jira.md` como formato padrão para toda história de mudança técnica no cofre, preparando o terreno para quando o MCP do Jira for conectado.

## Estrutura de apoio para onboarding
- [[00-Glossario]] — siglas e conceitos recorrentes (RN, NFR, SPOF, GEO/AEO, silo semântico, palavra épica etc.).
- [[00-Painel-Estado]] — snapshot único de status de produtos, fluxos, decisões e backlog, sem precisar ler nota por nota.
- [[03-Produtos/mapa-dependencia-produtos]] — cadeia de dependência entre Growth Machine, MPI Plus e Ideal Tracker, e a ordem de prioridade de foco atual (Growth Machine → MPI Plus → Ideal Tracker, definida pelo PO em 2026-07-02).
