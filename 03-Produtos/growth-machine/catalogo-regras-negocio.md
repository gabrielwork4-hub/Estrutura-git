---
tipo: produto
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-02
tags: [growth-machine, rn, catalogo, prd]
---

# Catálogo Completo de Regras de Negócio (RN-01 a RN-122) — Growth Machine

> As **122 RNs** do PRD v1.9.14, extraídas na íntegra. `growth-machine.md`
> traz só um subconjunto "chave" (27 RNs mais citadas); esta nota é a
> referência completa. Ver [[03-Produtos/growth-machine]] para o produto e
> [[00-Glossario]] para o que significa "RN".

## RN-01 a RN-10 — Briefing e Estrutura
- **RN-01:** Validação do briefing pelo cliente via CS — a análise não avança até validação ativa do cliente. Sem prazo automático.
- **RN-02:** Cadência: Ruim/Regular = mensal. Bom/Ótimo = trimestral. Motor roda mensalmente para TODOS.
- **RN-03:** Gatilho do bloqueio de 60 dias: disparado estritamente após homologação e OK final do analista.
- **RN-04:** Alerta de 28 dias: ação gerada e não executada após 28 dias = alerta ao gerente.
- **RN-05:** Briefing sem páginas institucionais: resolvido na v1.7 (crawler varre todas as páginas).
- **RN-06:** Cliente rejeita ativamente o briefing/estudo (via CS): máximo 2 iterações. 3ª rejeição → escala pro gerente. Sem resposta = sem prazo automático.
- **RN-07:** PageSpeed/Performance Front-end: análise por URL, mobile e desktop separados. Score ≥80 é a régua operacional MPI.
- **RN-08:** Servidor/TTFB/Infraestrutura: GTmetrix por URL representativa; M3 não abre em medição isolada; decisão considera recorrência, escopo, origem provável e evidência cruzada.
- **RN-09:** Tipo de projeto: E-commerce, Loja, Revendedor, Marketplace = Produto. Demais = Serviço.
- **RN-10:** Arquitetura MPI/Silo/Linkagem: estudo aprovado no MPI Plus é fonte de verdade. Direção padrão: variações → lateral + pilar; pilar não linka para baixo.

## RN-11 a RN-20 — Auditoria e Motor
- **RN-11:** W3C validação self-hosted em Docker. Classifica por severidade, impacto, recorrência e origem. Warnings leves só exibidos; erros críticos geram ação.
- **RN-12:** Breadcrumbs: padrão estático. Fora do escopo de auditoria.
- **RN-13:** Menu Header e Footer: mesmos itens.
- **RN-14:** Geração de texto baseada no padrão da SERP. Removida a distinção "texto épico vs texto comum".
- **RN-15:** Bonificação de palavras: similaridade vetorial ≥70% → fila de sugestões. Sujeita à trava de 50% do pacote (RN-85). Não fura aprovação humana.
- **RN-16:** Fronteiras de CTR: sem arredondamento. Posição 10,5 = CTR 1%.
- **RN-17:** Maturidade: interpolação linear. Mês 5 = 22,5%.
- **RN-18:** Pesos configuráveis via admin. Soma = 100%. Default oficial = 40 posicionamento / 40 tráfego / 20 leads.
- **RN-19:** Thresholds inclusivos: índice no limite sobe de categoria.
- **RN-20:** Volume zero: `volume_total = 0` → "Sem estudo válido" → alerta.

## RN-21 a RN-30 — Cenários e Alertas
- **RN-21:** Lead zerado é alerta extremo: sempre dispara.
- **RN-22:** Detecção de spam: padrões no campo assunto/mensagem. Não bloqueia — apenas alerta.
- **RN-23:** Formulário e SendGrid: lead salvo na base E log "entregue" = funcionando.
- **RN-24:** Trigger de upsell: ≥70% posicionamento E tráfego bom OU lead consistente.
- **RN-25:** Cadência do alerta de upsell: imediato, 24/7.
- **RN-26:** Bloqueio pós-ação: 60 dias (2 ciclos).
- **RN-27:** Janela de maturação: 60 dias fixos (corrige contradição da v1.7.2).
- **RN-28:** Alerta de ação não executada: 28 dias sem execução = alerta ao gerente.
- **RN-29:** Escore por etapa: 100% = não mexe. Abaixo = entra como ação.
- **RN-30:** Ações isoladas: Linkagem, W3C, GTmetrix, PageSpeed podem ser executados sozinhos.

## RN-31 a RN-40 — Workflow e Casos Especiais
- **RN-31:** Pacote obrigatório: causa raiz = Estudo → gera Estudo + Conteúdo + Imagem.
- **RN-32:** Análise em fases: 1ª Estudo/Conteúdo/Imagem. 2ª Silo/W3C/etc.
- **RN-33:** Cliente novo (&lt;28 dias): bloqueado até 28 dias.
- **RN-34:** Site em reformulação: flag "pausado". Reativado = começa do zero.
- **RN-35:** Cliente com múltiplos sites: cada site = projeto separado.
- **RN-36:** Site fora do padrão MPI: fora do escopo V1.
- **RN-37:** Inadimplência: normal nos primeiros 30 dias. Após 30 dias, bimestral + alerta. Após 60 dias, "pausado".
- **RN-38:** Cancelamento em negociação: análise normal.
- **RN-39:** Retry automático: 3 tentativas em 3 dias diferentes. Backoff exponencial.
- **RN-40:** Site fora do ar: 3 tentativas falhas em dias diferentes = alerta.

## RN-41 a RN-50 — Performance e Aprovação
- **RN-41:** Tintambi: identifica e informa ao analista. Não abre M3.
- **RN-42:** Scripts de terceiros: sinaliza scripts pesados.
- **RN-43:** Histórico real: baixo recurso (CPU) = timeout = desindexação.
- **RN-44:** Sistema prioriza, não pergunta: ordem de impacto calculada.
- **RN-45:** Ação desconsiderada: motivo + notifica Supervisor/Líder. Não fica em aberto.
- **RN-46:** Execução parcial: "2 de 6". Restantes voltam na próxima análise.
- **RN-47:** Aprovação humana obrigatória: nada é publicado automaticamente.
- **RN-48:** Macro atividade: Front-end finaliza macro → próxima análise.
- **RN-49:** Papel do Analista na Entrega: persona "Revisor" extinta. Analista acumula aprovação inicial e validação técnica final.
- **RN-50:** Boletim para o cliente: "melhoria", nunca "problema".

## RN-51 a RN-57 — Infraestrutura e Integração
- **RN-51:** Canal de notificações: E-mail + WhatsApp API.
- **RN-52:** Notificação de upsell: vai pro gerente.
- **RN-53:** ACL: Admin cria perfis customizados por módulo.
- **RN-54:** Cross-company: flag `cross_company = true`.
- **RN-55:** Múltiplos usuários por papel: transferência de projetos.
- **RN-56:** SendGrid pull diário: obrigatório. Logs 3 meses.
- **RN-57:** SendGrid plano atual: 7 dias de log. Armazenar localmente.
  > **Nota de conciliação (2026-07-06):** RN-56 e RN-57 têm prazos de
  > retenção diferentes (3 meses vs. 7 dias) para o mesmo dado — leitura
  > mais provável é que RN-56 seja a meta/requisito do produto e RN-57 o
  > limite do plano SendGrid contratado atualmente (por isso "armazenar
  > localmente": o pull diário exporta o log antes que o plano descarte
  > em 7 dias, viabilizando os 3 meses de retenção real da RN-56). **A
  > confirmar com o time técnico** — não está explícito no PRD original.

## RN-58 a RN-68 — Ajustes da Reunião 09/06/2026
- **RN-58:** Classificação macro de conteúdo: IA classifica em nível macro para evitar duplicação.
- **RN-59:** Cadência semestral de conteúdo: após 1º ajuste, Conteúdo só reavaliado a cada 6 meses (salvo força do analista).
- **RN-60:** Conversão WebP via API (opcional): analista decide.
- **RN-61:** Padrão de nomes de imagem: nomenclatura definida.
- **RN-62:** Formato de entrega: HTML "tagueado".
- **RN-63:** Vínculo de BU a usuários: múltiplas BUs por analista; visão consolidada.
- **RN-64:** Hard Stop por ausência de posicionamento: o GM exige dado de posicionamento para rodar. Fonte = relatório mensal do MPI Plus. Bright Data não é integração direta do GM. Se relatório ausente → Hard Stop completo.
- **RN-65:** Tempo de bloqueio de interface: 10 minutos.
- **RN-66:** Automação parametrizável: global ou por cliente; avanço sem validação = aprovação admin.
- **RN-67:** Sitemap/Robots/Indexabilidade: Dimensão 7 não usa o MPI Plus como fonte de verdade. Base é o site real descoberto pelo FireCrawl.
- **RN-68:** Sem reprocessamento com ações pendentes (exceto críticas: lead zerado ≥7d, site fora ≥3d, queda ≥30% em 7d).

## RN-69 a RN-73 — Ajustes da v1.7
- **RN-69:** Crawler completo: FireCrawl varre todas as páginas.
- **RN-70:** Paper Clip removido.
- **RN-71:** Aprovação obrigatória de novo estudo, conduzida pelo CS. Sem prazo automático; alerta ao gerente em 14 dias, escalação em 30.
- **RN-72:** Fila de Validação Operacional: tarefas concluídas geram flag "[!] Validar" no painel do analista.
- **RN-73:** Expulsão de Dados de Custo: proibido armazenar/exibir métricas financeiras, custo por token ou precificação de APIs na interface ou logs públicos.

## RN-74 a RN-89 — Ajustes da v1.8 (Reunião de Aprovação)
- **RN-74:** Salesforce é a fonte única de gestão de atividades, prazos e responsáveis; o GM não duplica gestão de tarefas.
- **RN-75:** Apenas ações aprovadas pelo analista são exportadas ao Salesforce.
- **RN-76:** Atividades exportadas são agrupadas por área/função; detalhe técnico permanece no GM.
- **RN-77:** Conclusão de atividade no Salesforce sincroniza o status automaticamente no GM (ida-e-volta).
- **RN-78:** Nenhum conteúdo/detalhe técnico trafega para o Salesforce — somente título e escopo da atividade.
- **RN-79:** A reativação dos robôs de validação só ocorre via botão de validação acionado pelo analista no GM; gatilho da maturação de 60 dias.
- **RN-80:** Briefing auto-incrementado: toda ação validada incrementa o briefing (nunca substitui o aprovado).
- **RN-81:** Validação automática por IA pós-execução: ao acionar a validação, o sistema relê o site e confere se cada ação do plano foi executada.
- **RN-82:** Otimização para IA (GEO/AEO): o sistema valida a presença de página AI Instructions (HTML em formato de prompt) e LLM.txt, referenciados no robots.txt e em meta tag no header.
- **RN-83:** WebP no robots: o sistema detecta e sinaliza robots.txt que bloqueie indexação de WebP. Recomenda fallback JPEG por navegador.
- **RN-84:** Sem sugestão de remoção de páginas: o sistema nunca sugere remover páginas, exceto quando o CS informa pedido explícito do cliente.
- **RN-85:** Trava de bonificação/criação de páginas: limitada a 50% do tamanho do pacote contratado; a IA deve evitar canibalização.
- **RN-86:** Tráfego orgânico: o `trafego_real` do motor considera apenas tráfego orgânico (exclui pago/patrocinado).
- **RN-87:** Medição de evolução por página alterada: após uma ação, a página é rastreada; reanálise da etapa de conteúdo só após evolução insuficiente em ≥60 dias.
- **RN-88:** Travamento condicional ao Estudo: a auditoria das 10 dimensões só é interrompida quando o problema crítico está no Estudo (Dim 1). Se o Estudo está OK, as dimensões 2–10 são auditadas integralmente e geram ações simultaneamente.
- **RN-89:** Camada de IA de Tradução de Diagnóstico: sobre o resultado de todas as dimensões roda uma camada de IA que converte o diagnóstico técnico em ações localizadas, priorizadas e em linguagem do executor/cliente. Não detecta — traduz e enriquece.

## RN-90 a RN-95 — Módulo Sentinela
- **RN-90:** Módulo Sentinela: monitoramento diário de disponibilidade, independente do ciclo de auditoria.
- **RN-91:** Escopo total: roda para todos os projetos ativos, inclusive bloqueados/em maturação.
- **RN-92:** Checks diários: uptime, SSL, DNS/MX, redirecionamento, robots/sitemap acessíveis, latência básica, AI Instructions/LLM.txt, mixed content.
- **RN-93:** Execução leve e noturna: janela noturna em lotes; não consome APIs caras. Fila via Laravel Horizon (Redis).
- **RN-94:** Sobreposição ao bloqueio: problema crítico de infra (site fora ≥3d, SSL expirado) dispara alerta e reabre análise mesmo em maturação.
- **RN-95:** Alerta antecipado de SSL: 30/15/7 dias antes do vencimento, ao analista + gerente.

## RN-96 a RN-99 — Consolidação e Modelos
- **RN-96:** Score de Saúde Técnica: nota determinística 0–100 = `100 − Σ(peso_dim × fator_severidade)` sobre as dimensões estruturais 2–10. Fica parcial com pesos renormalizados quando há dimensão não auditada.
- **RN-97:** Parecer Consolidado (agente de IA): diagnóstico executivo do projeto unindo Índice de Performance, Score de Saúde, as 10 dimensões, Sentinela e histórico. Roda 1x por análise completa.
- **RN-98:** Telas globais × contextuais: as telas de projeto (Telas 3, 4, 5 e 10) não figuram no menu principal — são acessadas ao selecionar um cliente no Painel de Carteira.
- **RN-99:** Modelo padrão dos agentes: GPT-5 é o modelo padrão dos agentes de IA do Growth Machine. Configurável por agente na Tela 9. As checagens determinísticas (Dim 4, 5, 6, 7, 9) não usam IA.

## RN-100 a RN-111 — Integração MPI Plus, Elegibilidade e Leads
- **RN-100:** Geração delegada e sob comando humano: o GM não gera estudo/conteúdo/imagem; ele detecta o gap e o apresenta ao analista. A geração no MPI Plus só é acionada quando o analista decide e clica "Gerar" (Gate 1). O asset gerado retorna ao GM via API e passa pela revisão interna do analista (Gate 2) antes de ser liberado ao cliente no MPI Plus.
- **RN-101:** Conexão via MPI Plus: o GM aciona a API do MPI Plus (que internamente usa a API Idealplus e o portal-cliente), não a API Idealplus direta. Padrão assíncrono: request → IntegrationJob → webhook assinado/importação de status.
- **RN-102:** Origem dos dados por completude: cliente no MPI Plus com dados completos → importação direta; cliente no MPI Plus com briefing legado/incompleto → FireCrawl complementa. Cliente fora do MPI Plus está fora de escopo (RN-108).
- **RN-103:** Dois níveis de aprovação, sem duplicar: revisão interna (analista, com apoio do CS) ocorre no GM; aprovação do cliente (briefing, estudo novo, conteúdo, imagens) ocorre no MPI Plus (portal-cliente).
- **RN-104:** Growth Machine é exclusivamente interno: nenhuma persona externa (cliente) acessa o GM. O cliente acessa apenas o MPI Plus.
- **RN-105:** Relatório mensal como fonte primária: Motor de Percepção consome o relatório mensal do MPI Plus (dia 1º, fotografia do mês fechado) como fonte primária de posicionamento, tráfego orgânico e leads. Bright Data e SendGrid passam a fallback.
- **RN-106:** Gatilho mensal + precedência: a chegada do relatório (~dia 1º/2) é o único gatilho de calendário, disparando o ciclo para toda a carteira.
- **RN-107:** Leads multicanal: o `leads_real` do índice é o total do relatório (formulário + WhatsApp + demais canais). O alerta de lead zerado dispara quando o total multicanal é 0.
- **RN-108:** Elegibilidade = estar no MPI Plus: ter contrato/projeto no MPI Plus é pré-requisito para um cliente ser monitorado pelo Growth Machine.
- **RN-109:** Alerta de falha de formulário condicionado à existência do formulário: cenário A2 só dispara se o projeto tiver formulário.
- **RN-110:** Coerência do índice de leads: como `leads_real` é multicanal, a `taxa_conversao` que compõe `leads_potencial` é a taxa multicanal.
- **RN-111:** Análise da SERP no GM, à parte, para diagnóstico: o GM roda sua própria análise da SERP (DataForSEO), separada e prévia, na Dim 2. Duplicação consciente aceita (diagnóstico no GM × criação no MPI Plus).

## RN-112 a RN-122 — Cada Dimensão como Contrato
- **RN-112:** Dimensão 1 como Agente Auditor de Estudo MPI (não gera estudo; audita o existente; DataForSEO/KeywordTools são condicionais; nenhuma ação é automática).
- **RN-113:** Dimensão 2 como Auditoria de Conteúdo SERP por página MPI (escopo = todas as páginas MPI elegíveis; DataForSEO identifica concorrentes; OpenAI/embeddings comparam cobertura; geração só após clique humano).
- **RN-114:** Dimensão 3 como Auditoria de Arquitetura MPI/Silo/Linkagem (estudo aprovado = fonte de verdade; FireCrawl = grafo real; IA só resolve ambiguidades; execução via Salesforce após aprovação humana).
- **RN-115:** Dimensão 4 como Checagem Determinística W3C (detecção é determinística; agrupa por página/template; classifica severidade por impacto e recorrência; warning leve é só exibido).
- **RN-116:** Dimensão 5 como Checagem Determinística PageSpeed por URL (GM monta cobertura a partir de páginas MPI elegíveis; roda mobile e desktop por URL; Camada de Tradução por IA não detecta performance; problemas de servidor/TTFB → Dimensão 9/M3).
- **RN-117:** Dimensão 6 como Checagem Determinística de Schemas JSON-LD (análise por URL elegível; MPI Plus define template esperado; IA traduz achados e apoia coerência semântica; sistema bloqueia sugestões de schema spam — ex: reviews, ratings, preços e FAQ fabricados/não verificáveis).
- **RN-118:** Dimensão 7 como Checagem Determinística de Sitemap/Robots/Indexabilidade (não usa o MPI Plus como fonte de verdade; usa FireCrawl + parsers; problemas bloqueando rastreamento ou indexação de páginas relevantes são críticos).
- **RN-119:** Dimensão 8 como Presença no Google/Sinais Externos (GSC como fonte principal; SemRush para backlinks; não substitui o Motor de Percepção; Agente Tradutor consolida achados e evita duplicidade; disavow sempre com revisão humana).
- **RN-120:** Dimensão 9 como Servidor/TTFB/Infraestrutura (não mede performance front-end geral; GTmetrix por URL representativa; M3 não abre por medição isolada; evidência cruzada necessária).
- **RN-121:** Dimensão 10 como Captação, Entrega e Qualidade de Leads (não recalcula o índice de leads; diagnostica se os canais estão captando, salvando, entregando e qualificando leads; falha de formulário só gera alerta se houver formulário ativo).
- **RN-122:** Contrato Parametrização × Agentes × Ferramentas (réguas, pesos, thresholds ficam na Tela 8; agentes, prompts, whitelists e schemas ficam na Tela 9; nenhum prompt pode hardcodar regra parametrizável; toda execução deve registrar `prompt_version_id`, `ruleset_version_id`, entradas, ferramentas, saída JSON, confiança e auditoria).

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[03-Produtos/growth-machine/cheat-sheet]]
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[00-Glossario]]
