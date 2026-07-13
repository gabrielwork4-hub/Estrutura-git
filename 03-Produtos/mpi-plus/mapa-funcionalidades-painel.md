---
tipo: produto
status: vivo
criado: 2026-07-13
ultima-revisao: 2026-07-13
origem:
  - "Avaliação de ferramenta/UX via assistente web (Painel MPI+ / Ideal Trends), trazida pelo usuário em 2026-07-13"
tags: [mpi-plus, ux, funcionalidades, painel, ideal-trends]
---

# Mapa de Funcionalidades — Painel MPI+ (Ideal Trends)

> Primeira documentação estrutural da **interface** do MPI Plus no cofre —
> até aqui só existia o lado de pipeline/prompts (ver
> [[03-Produtos/mpi-plus]] › "Pipeline de prompts"). Levantado via
> avaliação de UX/ferramenta pedida pelo usuário a um assistente web,
> 2026-07-13. Cruzado abaixo com as RNs do
> [[03-Produtos/growth-machine]] que já dependem dessas telas — várias
> peças que só existiam como conceito ("o relatório mensal", "a aprovação
> do cliente no MPI Plus") agora têm uma tela concreta associada.

## Estrutura global
- Menu lateral: Dashboard, Clientes, Relatórios, Usuários, Configurações.
- Topo: busca global (cliente/cor), notificações, modo escuro, perfil/sair.

## 1. Dashboard
- KPIs: Clientes Ativos, Total de Conteúdos, Publicações.
- Atalhos rápidos: Contratos Ativos, Briefings pendentes, Estudos em
  andamento, Conteúdos aguardando aprovação.
- Widget "Clientes por Etapa" (funil por etapa).

## 2. Clientes
- Listagem com filtros: analista, etapa, status, BU, origem
  (Manual/Salesforce), período.
- Ações em massa: Adicionar, Atualizar, Exportar CSV.
- Ações por linha: credenciais, editar, excluir, Acessar.
- **Hub do Cliente** (ao acessar um cliente/projeto/contrato):
  - **Resumo:** dados da empresa, dados contratuais, linha do tempo do projeto.
  - **Briefing:** formulário (dados da empresa, produtos/serviços, template), com IA de resumo e aprovação.
  - **Estudo:** estudo de palavras-chave (import CSV, status, aprovação, progresso do pacote).
  - **Relatório:** integrações (Google Analytics 4, Search Console, leads legado), envio automático mensal por e-mail, histórico de relatórios gerados.
- Pipeline padrão de etapas: Diagnóstico → Briefing → Estudo → Conteúdo →
  Aprovação → Publicação → Site no ar.

## 3. Relatórios
- Visão geral: KPIs (clientes ativos, conteúdos, publicações, taxa de
  aprovação, tempo médio de entrega).
- Clientes: relatório de contratos ativos (pacote, etapa, vencimento, responsável).
- Conteúdo: total/completos/em processamento, performance por
  palavra-chave (status texto/imagem).

## 4. Usuários
- **Usuários (internos):** nome, e-mail, telefone, cargo/permissão, BU.
- **Clientes (do portal):** usuários externos com acesso ao portal do cliente.
- **Permissões:** gestão de cargos (Administrador, Analista de
  CS/Estudo/Implementação/Produção, Gestor de CS/Estudo/Implementação) com
  controle granular por módulo (Dashboard, Clientes, Projetos, Contratos,
  Relatórios, Usuários, Configurações).

## 5. Configurações
- **Geral:** em desenvolvimento.
- **Briefing:** listas do formulário (segmentos, tipos de empresa, tipos
  de produto/serviço).
- **Notificações:** templates de e-mail/WhatsApp/interno por etapa do
  fluxo (30 templates).
- **Templates IA:** pipeline de geração de texto (6 etapas: classificador
  de domínio, análise de padrão, estrutura, seção, coesão final, QA) +
  prompt de imagem + regras de limpeza/formatação HTML + blacklist de
  palavras.
- **Templates WP:** temas visuais (WordPress) disponíveis no briefing, com
  upload de ZIP.
- **Módulos:** ativação/ordenação de blocos do portal do cliente (Temas,
  Configurações, Site, Componentes, Integrações).
- **Logs:** histórico de ações do sistema e integrações (filtros por
  usuário, status, tipo de job), paginado.

---

## Cruzamento com o Growth Machine
Várias telas aqui são a **contraparte concreta** de RNs do GM que até
agora só existiam como conceito abstrato ("o relatório mensal", "a
aprovação ocorre no MPI Plus"):

| Tela/bloco do MPI+ | RN/RF do GM que depende dela | Observação |
|---|---|---|
| **Hub do Cliente › Relatório** (GA4, Search Console, leads legado, envio automático mensal) | **RN-105/RN-106** (fonte única de posicionamento/tráfego/leads, gatilho mensal ~dia 1º/2), **RN-64** (Hard Stop se ausente) | Confirma que o "relatório mensal" citado dezenas de vezes no catálogo de RN **é literalmente esta aba** — não uma integração separada. Não confirma, porém, **se a geração é automática na virada do mês ou depende de disparo manual** — abre pergunta nova, ver "Lacunas" abaixo. |
| **Hub do Cliente › Estudo** (import CSV, status, aprovação, progresso do pacote) | **RN-101/RN-102** (import via API), **RN-103** (aprovação do cliente ocorre no MPI Plus, não no GM), auditado por **RN-112** (Dim 1) | Confirma RN-103 com tela concreta — a aprovação do estudo pelo cliente acontece aqui, não no GM. |
| **Hub do Cliente › Briefing** (formulário + IA de resumo + aprovação) | **RF-01/RF-03** (import + validação pelo CS), **RN-01** | A "IA de resumo" é um componente novo, não documentado antes em nenhuma RN do GM — provavelmente upstream do que o GM importa, não algo que o GM audita. |
| **Configurações › Templates IA** (6 etapas: classificador de domínio, padrão, estrutura, seção, coesão, QA) | Já documentado em [[03-Produtos/mpi-plus]] › "Pipeline de prompts" (SERP Search → Domain Classification → Pattern Analysis → Structure → Section → Cohesion → QA) | **Convergência confirma o pipeline já registrado** — a única diferença é que aqui a etapa "SERP Search" não aparece nomeada como "template" (provavelmente é coleta de dado upstream, não um template editável). Não é contradição, é nível de detalhe diferente. |
| **Configurações › Notificações** (templates e-mail/WhatsApp/interno, 30 templates) | **RN-51** (canal E-mail + WhatsApp API do GM) | Candidato natural a ser o mesmo canal que a proposta **RN-123** (confirmação de entrega WhatsApp) precisaria instrumentar via webhook — não confirmado se é a mesma infraestrutura de envio ou uma paralela. |
| **Configurações › Templates WP** (temas WordPress, upload ZIP) | **RN-62** (formato de entrega = HTML "tagueado") | Não fica claro se "tema WordPress" e "HTML tagueado" são o mesmo formato de entrega visto por ângulos diferentes, ou dois mecanismos distintos — sinalizado como pergunta aberta. |

## O que este mapa NÃO confirma (lacunas/perguntas em aberto)
- **Geração do relatório mensal — automática ou manual?** A aba Relatório
  mostra "envio automático mensal por e-mail" e "histórico de relatórios
  gerados", mas não diz se a **geração** (consolidação de GA4+GSC+leads) é
  automática no fechamento do mês ou depende de ação humana — isso importa
  para RN-106 (gatilho de calendário) e para o Hard Stop RN-64 (o que
  exatamente conta como "ausente"?).
- **Dois sistemas de papéis/permissão não conversam entre si.** O MPI+ tem
  seus próprios cargos (Administrador, Analista de CS/Estudo/
  Implementação/Produção, Gestor de CS/Estudo/Implementação), distintos
  das 5 personas do GM (Analista de Growth, CS, Gerente/Supervisor,
  Front-end, Cliente) — mesmo havendo nomes parecidos ("CS", "Analista",
  "Gestor"/"Gerente"), **não há de-para documentado** confirmando se é a
  mesma pessoa navegando dois painéis com nomenclaturas diferentes, ou
  papéis genuinamente distintos. Risco de confusão em qualquer
  especificação futura que cite "o CS" sem dizer em qual sistema.
- **Módulos do portal do cliente** (Temas, Site, Componentes, Integrações)
  nunca apareceram em nenhuma nota do GM até agora — não está confirmado
  se é aqui que o Cluster Wrapping (`/informacoes`/`/artigos`) ou o
  Portão de Diferenciação Real precisariam de algum toggle/configuração
  visível ao cliente, ou se isso é 100% invisível para ele.
- **Logs do MPI+** (ações do sistema + integrações, por usuário/status/tipo
  de job) — não confirmado se é a mesma trilha de auditoria que RN-122 exige
  do lado do GM (`prompt_version_id`, `ruleset_version_id` etc.) ou um log
  paralelo e desconectado.
- **"Diagnóstico" como 1º passo do pipeline do MPI+** (Diagnóstico →
  Briefing → Estudo → Conteúdo → Aprovação → Publicação → Site no ar) usa o
  mesmo termo que o GM usa para a auditoria recorrente mensal (Fase 3) —
  aqui parece ser um passo único de onboarding, não um ciclo repetido.
  Vale confirmar que não é o mesmo conceito antes de reusar terminologia
  entre os dois produtos.

## Cruzamento com outras notas
- [[03-Produtos/mpi-plus]] — nota-mãe do produto; esta nota preenche a
  lacuna de UI que lá estava marcada "a preencher".
- [[03-Produtos/growth-machine]] — RN-51, RN-62, RN-64, RN-101–RN-106,
  RN-112, RN-122 (ver tabela de cruzamento acima).
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — fonte das RNs citadas.
- [[PRDFINAL]] — Bloco 10 (Dependências) cita o MPI Plus como SPOF
  reconhecido; este mapa é o primeiro material concreto da superfície que
  o torna SPOF.

## Notas relacionadas
- [[03-Produtos/mpi-plus]]
- [[03-Produtos/growth-machine]]
- [[00-Painel-Estado]] · [[00-Cerebro]]
