---
tipo: cerebro
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-02
tags: [glossario, core]
---

# Glossário

> Termos e siglas que aparecem no cofre. Existe para que alguém entrando
> agora (PO, dev, ou uma IA) não precise decifrar jargão por contexto.
> Atualizar sempre que um termo novo se tornar recorrente.

## Siglas gerais de produto/negócio

| Termo | Significado |
|---|---|
| **PO** | Product Owner. |
| **PRD** | Product Requirements Document — documento de especificação de produto (ex: PRD do Growth Machine, v1.9.14). |
| **MVP** | Minimum Viable Product — versão mínima viável de um produto. |
| **SLA** | Service Level Agreement — acordo/prazo de nível de serviço (ex: SLA de revisão de conteúdo, ainda em aberto no Growth Machine). |
| **ADR** | Architecture Decision Record — formato de registro de decisão (o que foi decidido, por quê, alternativas); é o modelo usado em [[04-Decisões]]. |
| **KPI** | Key Performance Indicator — indicador-chave de desempenho. |
| **UX** | User Experience — experiência do usuário. |
| **UI** | User Interface — interface do usuário. |
| **QA** | Quality Assurance — garantia/auditoria de qualidade; também o nome de uma etapa do pipeline de conteúdo do MPI Plus. |
| **RN-XX** | Regra de Negócio numerada — usado no PRD do Growth Machine (RN-01 a RN-122). Cada uma é uma regra específica e rastreável, com número fixo citado nas notas. |
| **NFR-XX** | Non-Functional Requirement (Requisito Não-Funcional) — desempenho, disponibilidade, segurança etc., não comportamento de negócio. |
| **QXX** (ex: Q18, Q27) | Questão em aberto numerada no PRD do Growth Machine — pergunta ainda sem resposta definitiva, listada em "Questões em Aberto". |

## Siglas técnicas de infraestrutura/sistema

| Termo | Significado |
|---|---|
| **SPOF** | Single Point of Failure — ponto único de falha. No Growth Machine, o MPI Plus é reconhecido como SPOF da integração. |
| **API** | Application Programming Interface — interface de comunicação entre sistemas (ex: API REST do MPI Plus). |
| **REST** | Representational State Transfer — estilo de API usado na integração GM↔MPI Plus. |
| **JSON** | JavaScript Object Notation — formato de dado estruturado usado como saída obrigatória dos agentes de IA e dos prompts. |
| **JSON-LD** | JSON for Linking Data — formato de dados estruturados (Schema.org) embutido em páginas HTML; auditado na Dimensão 6 do Growth Machine. |
| **HTML** | HyperText Markup Language — linguagem de marcação das páginas web, validada na Dimensão 4 (W3C). |
| **URL** | Uniform Resource Locator — endereço de uma página/recurso na web. |
| **SSO** | Single Sign-On — login único; o Growth Machine usa SSO integrado ao MPI Plus, sem senha própria. |
| **ACL** | Access Control List — lista de controle de acesso, usada na Tela 7 (Gestão de Perfis) do Growth Machine. |
| **LGPD** | Lei Geral de Proteção de Dados — lei brasileira de privacidade, citada nos requisitos de retenção de dados. |
| **TTFB** | Time To First Byte — tempo até o servidor responder o primeiro byte; métrica de performance de infraestrutura (Dimensão 9). |
| **CWV** | Core Web Vitals — métricas de experiência de página do Google (LCP, INP, CLS). |
| **LCP / INP / CLS** | Largest Contentful Paint / Interaction to Next Paint / Cumulative Layout Shift — as 3 métricas que compõem o Core Web Vitals. |
| **DNS** | Domain Name System — sistema que resolve domínio em endereço de servidor. |
| **MX** | Mail Exchange — registro DNS que direciona e-mails de um domínio. |
| **SPF / DKIM / DMARC** | Protocolos de autenticação de e-mail que evitam spoofing/spam — checados na Dimensão 10 (Leads) do Growth Machine. |
| **SSL / HTTPS** | Secure Sockets Layer / protocolo seguro de navegação — certificado checado diariamente pelo Módulo Sentinela. |
| **CDN** | Content Delivery Network — rede de distribuição de conteúdo, relevante para cache/performance (Dimensão 9). |
| **Docker** | Tecnologia de containers usada para hospedar o W3C Validator self-hosted (Dimensão 4). |
| **PHP / Laravel** | Linguagem e framework que formam o stack de backend do Growth Machine. |
| **Redis / Laravel Horizon** | Redis é o banco em memória usado para filas; Laravel Horizon é o gerenciador de filas assíncronas do Growth Machine (substituiu BullMQ/Node por consistência de stack). |
| **Webhook** | Notificação HTTP automática entre sistemas (ex: MPI Plus avisa o GM quando um asset termina de ser gerado). |
| **IntegrationJob** | Padrão assíncrono da integração GM→MPI Plus: request → IntegrationJob → webhook assinado/importação de status. |
| **Row-level access** | Controle de acesso por linha do banco de dados — usado no Growth Machine para separar empresas/BUs numa base compartilhada (sem multi-tenant isolado). |
| **`cross_company`** | Flag no modelo de dados do Growth Machine que permite um usuário ver dados de mais de uma empresa do grupo. |

## Siglas de IA/LLM

| Termo | Significado |
|---|---|
| **IA** | Inteligência Artificial. |
| **LLM** | Large Language Model — modelo de linguagem grande (ex: GPT-5, usado como modelo padrão dos agentes do Growth Machine). |
| **GPT** | Generative Pre-trained Transformer — família de modelos da OpenAI. |
| **Embeddings** | Representação vetorial de texto usada para comparar similaridade semântica (ex: `text-embedding-3-small`, usado para detectar canibalização e bonificação de palavras). |
| **Prompt de sistema / prompt de usuário** | As duas partes de uma instrução dada a um LLM: o "system prompt" define papel/regras gerais; o "user prompt" traz a tarefa/dados específicos da chamada. |
| **`prompt_version_id` / `ruleset_version_id`** | Identificadores obrigatórios registrados em todo log de execução de agente do Growth Machine, para rastrear qual versão de prompt/regra gerou uma ação. |
| **Golden-set** | Conjunto de casos de teste validados manualmente, usado para comparar a saída de duas versões de um prompt antes de promover a nova para produção. |
| **Alucinação** | Quando um LLM inventa informação não presente no contexto fornecido — mitigado pela "Regra Anti-Alucinação" injetada nos prompts de conteúdo do MPI Plus. |
| **MCP** | Model Context Protocol — protocolo que conecta este assistente de IA a ferramentas externas (Jira, Google Drive, Notion, GitHub etc.). Ainda não conectado ao Jira neste cofre. |
| **RAG** | Retrieval-Augmented Generation — motivo de existir a regra de linkagem obrigatória do cofre: permitir que uma IA navegue de uma ideia até produto/fluxo/decisão sem perder contexto. |

## Siglas/conceitos de SEO tradicional

| Termo | Significado |
|---|---|
| **SEO** | Search Engine Optimization — otimização para mecanismos de busca (Google). |
| **SERP** | Search Engine Results Page — página de resultados de busca. |
| **DR** | Domain Rating — métrica de autoridade de domínio (escala Ahrefs), usada na Análise Competitiva. |
| **CTR** | Click-Through Rate — taxa de cliques; no Growth Machine, varia por posição (Top 3 → 20%, Top 10 → 5%, acima do Top 10 → 1%). |
| **CPC** | Custo Por Clique — métrica de mídia paga, usada como dado de enriquecimento de keyword no MPI Plus. |
| **KD** | Keyword Difficulty — dificuldade estimada de ranquear para um termo. |
| **E-E-A-T** | Experience, Expertise, Authoritativeness, Trustworthiness — critério de qualidade de conteúdo do Google, referenciado nos prompts de conteúdo do MPI Plus. |
| **YMYL** | Your Money or Your Life — categoria de conteúdo sensível (saúde, finanças) que exige padrão mais rígido de qualidade/veracidade. |
| **Helpful Content** | Diretriz do Google que prioriza conteúdo genuinamente útil ao usuário sobre conteúdo otimizado só para ranquear. |
| **Featured Snippet** | Bloco de resposta em destaque no topo da SERP do Google. |
| **Information Gain** | Quanto um conteúdo novo agrega além do que já existe na SERP — critério usado nos prompts de Análise de Padrão/Estrutura do MPI Plus. |
| **Sitemap / Robots.txt** | Arquivos técnicos que declaram, respectivamente, as páginas do site e as regras de rastreamento para buscadores — auditados na Dimensão 7. |
| **Canonical** | Tag HTML que indica a URL "oficial" de uma página, evitando conteúdo duplicado. |
| **Noindex** | Instrução que impede uma página de ser indexada pelo Google. |
| **Backlink** | Link externo apontando para o site — auditado na Dimensão 8 (tóxicos via SemRush). |
| **Disavow** | Ação de pedir ao Google para ignorar backlinks tóxicos — sempre com revisão humana no Growth Machine, nunca automático. |

## Siglas/conceitos de GEO/AEO (busca generativa)

| Termo | Significado |
|---|---|
| **GEO** | Generative Engine Optimization — otimização para mecanismos de busca generativos (ChatGPT, Google AI Overview). Tema central do Ideal Tracker. Não confundir com "GEO local" (ver abaixo). |
| **AEO** | Answer Engine Optimization — variante de GEO focada em otimizar para ser a resposta direta de um LLM. |
| **GEO local** | No fluxo de estudo de keywords, é o cluster/pilar dedicado a variações geográficas de busca (cidade/região) — uso diferente do "GEO" de busca generativa; desambiguar pelo contexto. |
| **SoV** | Share of Voice — participação de menções/visibilidade de uma marca frente a concorrentes; usado no Ideal Tracker para medir presença em respostas de LLM. |
| **AI Overview** | Recurso do Google que gera resposta sintetizada por IA no topo da busca, sem API oficial de coleta (ponto crítico em aberto no Ideal Tracker). |
| **LLM.txt / AI Instructions** | Arquivo/página que orienta LLMs sobre como interpretar o site — checado como parte da Dimensão 7 e do Módulo Sentinela do Growth Machine (RN-82). |

## Conceitos de SEO/keywords (fluxo de estudo de keywords do cofre)

| Termo | Significado |
|---|---|
| **Cluster** | Agrupamento de keywords por intenção de busca real, não por volume isolado — base da lógica de [[02-Fluxos/estudo-de-keywords]]. |
| **Canibalização** | Quando duas páginas diferentes competem pela mesma intenção de busca, prejudicando o ranqueamento de ambas. O fluxo do cofre existe para evitar isso. |
| **Silo semântico** | Estrutura de página-pilar + páginas-filhas ligadas por relação de significado real (não só palavras parecidas) — regra central do prompt v3 oficial. |
| **Pilar / Página Pilar** | Página principal de alta autoridade dentro de um silo/cluster. |
| **Palavra épica** | No sistema real do MPI Plus: a keyword eleita como principal de um produto, escolhida pelo maior volume entre termos comerciais/transacionais (fallback: maior volume geral). |
| **Content Map** | Tabela que define, por página, qual é a keyword principal (nunca repetida entre páginas) e as secundárias — a "pauta" que vira produção de conteúdo. |
| **Keyword-âncora** | Termo/ponto de partida do Cluster Pillar/Core de um estudo — no prompt v3 oficial, é derivada pelo próprio prompt a partir do serviço principal, não fornecida como entrada (correção de 2026-07-02). |
| **Long-tail** | Termo de busca específico, com 3+ palavras ou modificador forte — baixo volume individual, alta especificidade. |
| **Head / termo head** | Termo genérico e curto, alto volume, baixa conversão (ex: "notebook"). |
| **Long-tail de baixa concorrência** | Cluster obrigatório do prompt v3 dedicado a termos específicos com pouca disputa de ranqueamento. |
| **`{$objetivo}`** | Variável do prompt v3 que funciona como peso de priorização por seção (Leads/Vendas, SEO local, Autoridade), não só um rótulo. |
| **KeywordTool** | Ferramenta externa que enriquece termos com dados reais (volume, CPC, concorrência) — na inversão de fluxo proposta, deixa de filtrar e passa só a enriquecer. |
| **Google Autocomplete** | Recurso de sugestão automática do Google usado hoje como motor de descoberta de sementes — a ser substituído por geração direta via IA. |

## Termos específicos do Growth Machine

| Termo | Significado |
|---|---|
| **Índice de Performance** | Fórmula do Motor de Percepção (Fase 2): 40% posicionamento + 40% tráfego + 20% leads, classificando cliente em Ruim/Regular/Bom/Ótimo. |
| **Score de Saúde Técnica** | Nota determinística 0-100 calculada a partir das 10 dimensões de auditoria (Fase 3), separada do Índice de Performance. |
| **Parecer Consolidado** | Diagnóstico executivo em linguagem natural gerado por um agente de IA, unindo Índice + Score + as 10 dimensões + Sentinela. |
| **Módulo Sentinela** | Vigilância diária e leve (uptime, SSL, DNS) de 100% dos sites, independente do ciclo de auditoria mensal/trimestral. |
| **Maturação (60 dias)** | Janela de bloqueio de reanálise após uma ação ser validada — evita medir resultado antes do efeito real aparecer. |
| **Dimensão (1 a 10)** | Cada uma das 10 áreas de auditoria técnica do Growth Machine (Estudo, Conteúdo, Arquitetura, W3C, PageSpeed, Schemas, Sitemap, Search Console, Servidor, Leads). |
| **Hard Stop** | Bloqueio total da análise de um cliente quando falta um dado essencial (ex: relatório mensal do MPI Plus ausente). |
| **M3** | Macroatividade de infraestrutura — ação aberta quando há evidência cruzada e recorrente de problema de servidor/TTFB (Dimensão 9). Não abre por medição isolada. |
| **Double-Check** | Padrão de validação em duas camadas na Fase 4: aprovação inicial do analista + validação técnica automática por IA antes da homologação final. |
| **Gate 1 / Gate 2** | Pontos de aprovação humana na geração delegada ao MPI Plus: Gate 1 = analista aciona "Gerar"; Gate 2 = analista revisa o asset gerado antes de liberar ao cliente. |
| **CS** | Customer Success — time que valida o briefing com o cliente na Fase 1 (não é o cliente sozinho que valida). |
| **BU** | Business Unit — unidade de negócio; o Growth Machine opera com 3 empresas (Ideal Marketing, Busca Cliente, MPI Solutions), cada uma com suas BUs. |

## Termos específicos do vault/processo

| Termo | Significado |
|---|---|
| **Nota órfã** | Nota sem nenhum link de entrada ou saída — proibida pela regra do cofre (CLAUDE.md). |
| **Fluxo** | Processo/workflow documentado em [[02-Fluxos]], com histórico de ajustes. |
| **Decisão fundadora** | Decisão registrada em [[04-Decisões]] que molda o funcionamento do cofre ou de um produto — estilo ADR. |
| **Frontmatter** | Bloco de metadados YAML no topo de cada nota (`tipo`, `status`, `criado`, `tags` etc.), usado para categorização e busca estruturada. |
| **Wikilink (`[[Nota]]`)** | Sintaxe de link interno do Obsidian, obrigatória pela regra de linkagem do cofre em vez de menção em texto livre. |

## Notas relacionadas
- [[00-Cerebro]]
- [[00-Painel-Estado]]
- [[03-Produtos/mapa-dependencia-produtos]]
