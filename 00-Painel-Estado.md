---
tipo: cerebro
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-10
tags: [painel, estado, core]
---

# Painel de Estado

> Snapshot único de "onde cada coisa está" — cada nota tem seu próprio
> `status` no frontmatter, mas antes desta nota era preciso ler uma por
> uma para montar essa visão. Atualizar sempre que um status mudar.

## Cheat sheets (resumo de 1 página, para ter "na ponta da língua")
- [[03-Produtos/growth-machine/cheat-sheet]] — números/regras do Growth Machine sem precisar abrir a nota completa.
- [[03-Produtos/growth-machine/prep-reuniao-po-lead]] — preparo para reunião com o responsável pelos POs (2026-07-03).
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] — termômetro evolutivo de maturidade SEO vs. GEO/AEO (score atual: SEO ~75-80% / GEO ~25-30% / combinado ~55-60%).
- [[03-Produtos/growth-machine/briefing-lideranca-seo-geo-aeo]] — briefing pronto para conversa com liderança: mapa de fontes + linha de raciocínio única das 3 frentes + 3 perguntas de decisão (2026-07-07).
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] — aderência da doc atual ao PRD ideal (13 blocos) + auditoria de qualidade das 122 RNs + esqueleto da v2 (2026-07-08). Base para projetar a nova documentação.
- [[03-Produtos/growth-machine/documentacao-v2-rf-e-user-stories]] — demonstração de formato dos blocos 5 e 8 (**absorvida** no PRD v2.0).
- [[PRDFINAL]] — **PRD final (v1.0)**: 13 blocos, RF-00 a RF-54 (8 novas formalizando RN-SGA/RN-EST ✅ MVP), User Stories/CA, checagem dedicada de aderência a boas práticas Google 2026 × estrutura interna. Substitui [[03-Produtos/growth-machine/prd-v2-mvp]] como cópia de leitura para build (2026-07-10).
- [[03-Produtos/growth-machine/prd-v2-mvp]] — rascunho de consolidação (13 blocos, RF-00 a RF-46) que originou o PRD final — **histórico**, não mais atualizado (2026-07-08).
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — ultra-análise das regras do Gregory (4 sub-PRDs) × cofre × boas práticas/core updates. **5 conflitos resolvidos em 2026-07-10** (pesos 40/40/20 sob revisão, numeração RN, cluster, fluxo keywords, fonte posicionamento) (2026-07-08).
- [[03-Produtos/growth-machine/checklist-google-2026-emtecorp-gregory]] — checklist SEO/GEO/AEO: Google 2026 × emtecorp real × Gregory × GM. Padrões recorrentes da GM + 4 oportunidades novas a virar backlog (2026-07-08).
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] — mapa princípio→RN→Dimensão→ação; estrutura-alvo das dimensões (2D-AEO, 2E-E-E-A-T, Dim 11 GEO) para o PRD v2 (2026-07-08).
- [[03-Produtos/growth-machine/estrategia-cluster-sem-mexer-contrato]] — análise de apoio, **formalizada em ADR** ([[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]) em 2026-07-10 (2026-07-08).
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — **tracker de fechamento do PRD**: 9 decisões-gate **todas resolvidas** (2026-07-10) + 5 trilhas paralelas + checklist dimensão a dimensão do PRD ajustado, com "Definição de PRD fechado" como critério de saída (2026-07-08).
- [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] — **✅ concluída**: acesso liberado, vault externa lida (índice + roadmap + Cluster Wrapping + Camada de Calibração Contínua). Pesos revertidos p/ 40/40/20 sob revisão; RN-123/124 reais (entrega multicanal) incorporadas; Cluster Wrapping validado e enriquecido com Portão de Diferenciação Real (2026-07-10).
- [[03-Produtos/growth-machine/validacao-fluxos-principios]] — validação das 5 correntes operacionais × 6 princípios-núcleo: nenhuma contradição lógica encontrada, 3 correções de fluxo aplicadas, 1 gap real confirmado (loop de GEO/Dim 11 segue Fase 2) (2026-07-10).
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] — **reescrito**: fila de prioridade agora com 17 itens, anti-doorway/Cluster Wrapping como #1 (era ausente na versão original), todos os itens amarrados a RN-SGA (2026-07-10).
- [[03-Produtos/mpi-plus/mapa-funcionalidades-painel]] — primeira UX/UI do painel MPI+ mapeada: Dashboard/Clientes/Relatórios/Usuários/Configurações; confirma que o "relatório mensal" (RN-105/RN-106) e a aprovação do cliente (RN-103) do GM têm tela concreta no Hub do Cliente; expõe 5 lacunas novas (geração automática × manual do relatório, papéis MPI+ × personas GM sem de-para, módulos do portal do cliente, logs, termo "Diagnóstico" ambíguo entre os dois produtos) (2026-07-13).

## Produtos

| Produto | Status | Prioridade | Nota |
|---|---|---|---|
| [[03-Produtos/growth-machine]] | Em desenvolvimento — **PRD final estruturado** ([[PRDFINAL]]); PRD v1.9.14 no Drive; avaliação crítica concluída | **Foco atual** | 10 itens de backlog abertos, 7 questões de integração ainda bloqueiam build |
| [[03-Produtos/mpi-plus]] | Em desenvolvimento — sem PRD próprio, prompts oficiais definidos, **UI/UX mapeada** ([[03-Produtos/mpi-plus/mapa-funcionalidades-painel]], 2026-07-13) | 2º | Dependência direta do Growth Machine (RN-108) |
| [[03-Produtos/ideal-tracker]] | Em desenvolvimento — PRD/UX documentados | 3º | 6 pontos críticos em aberto, sem dependência cruzada |

## Fluxos

| Fluxo | Status | Nota |
|---|---|---|
| [[02-Fluxos/estudo-de-keywords]] | Ativo | Fluxo-mãe da lógica de clusterização/anti-canibalização |
| [[02-Fluxos/prompt-avaliacao-keywords]] | **v3 oficial** | v1/v2 mantidos como histórico. Correção de keyword-âncora aplicada em 2026-07-02 |
| [[02-Fluxos/processo-kickoff-discovery]] | Ativo | Kick-off → discovery → aprovação → backlog |
| [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]] | Histórico (superado pelo v3) | Mantido para rastreabilidade |

## Decisões

| Decisão | Status |
|---|---|
| [[04-Decisões/migracao-prompt-keywords-v2]] | Histórico (superado pelo v3) |
| [[04-Decisões/padrao-historia-jira]] | Aceita — vigente |
| [[04-Decisões/adr-camada-calibracao-continua]] | Aceita — vigente (RN-18 = 40/40/20 sob revisão) |
| [[04-Decisões/adr-pesos-indice-performance-2026]] | Superada por adr-camada-calibracao-continua |
| [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] | Aceita — vigente (cluster aditivo via /informacoes) |

## Histórias/prompts do MPI Plus

| História | Status | Produto |
|---|---|---|
| [[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]] | Oficial, aguardando envio ao Jira | MPI Plus |
| [[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]] | **Enviada ao Jira (2026-07-03)** — resolve gargalo de geração de termos | MPI Plus |
| [[03-Produtos/mpi-plus/historia-prompt-endurecimento-anti-concatenacao-geo]] | **Versão final consolidada** (vigente para geração de termos), aguardando envio ao Jira — motivada por QA de produção real | MPI Plus |

## Backlog aberto por prioridade

**Alta**
- [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]]
- [[05-Backlog/gm-atribuir-dono-prazo-questoes-abertas]]
- [[05-Backlog/gm-desenho-fino-prompts-agentes]]
- [[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]]
- [[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]] — direção confirmada pelo PO (aba GEO)
- [[05-Backlog/gm-implementar-pilares-agenticos-webmcp]] — Agentic Browsing/WebMCP, 5 de 6 pilares ausentes
- [[05-Backlog/ideal-track-definir-metodologia-sov]]

**Média**
- [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]]
- [[05-Backlog/gm-segregacao-funcoes-pontos-controle]]
- [[05-Backlog/gm-criterio-desempate-fronteiras-componentes]]
- [[05-Backlog/gm-escopo-sentinela-infraestrutura-cron]]
- [[05-Backlog/gm-dimensionamento-cotas-ferramentas-externas]]
- [[05-Backlog/gm-segmentar-trafego-origem-ia]]
- [[05-Backlog/gm-sinal-conteudo-original]]
- [[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]]

**Baixa**
- [[05-Backlog/gm-salvaguarda-aprovacao-massa-telas]]
- [[05-Backlog/gm-checagem-presenca-entidade]]
- [[05-Backlog/gm-cobertura-video-como-dimensao]]

## Lacunas de onboarding conhecidas (não resolvidas ainda)
- **Donos/responsáveis**: nenhum fluxo, produto ou decisão tem uma pessoa
  nomeada como responsável — deliberadamente deixado em aberto (PO ainda
  mapeando stakeholders, 2026-07-02). Retomar quando os nomes existirem.
- **13 pastas do Drive** não avaliadas (ver [[03-Produtos/mapa-dependencia-produtos]]).

## Notas relacionadas
- [[00-Cerebro]]
- [[00-Glossario]]
- [[03-Produtos/mapa-dependencia-produtos]]
