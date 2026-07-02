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

## Ideia inicial
Por que esse cofre existe, qual problema ele resolve, qual é a visão por trás dele.

> _A preencher._

## Funcionamento
Como o cofre opera no dia a dia: como ideias entram, como viram fluxo, como fluxo vira produto, como decisões são tomadas.

> _A preencher._

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

## Produtos em desenvolvimento
Linka para [[03-Produtos]] os produtos atualmente ativos. Validado contra a
pasta do Drive em 2026-06-30 (16 pastas de projeto ao todo; só os 3 abaixo
foram aprofundados até agora).
- [[03-Produtos/growth-machine]] — orquestração de SEO para ~2.500 projetos MPI, 4 fases (briefing → percepção → auditoria 10 dimensões → fila de ações no Salesforce). PRD v1.9.14 já existe no Drive.
- [[03-Produtos/mpi-plus]] — pré-requisito de carteira da Growth Machine (RN-108); refatoração de processo e palavras-chave em 2 etapas oficiais: geração de termos ([[03-Produtos/mpi-plus/historia-prompt-inversao-fluxo-keywords]]) e arquitetura de site ([[03-Produtos/mpi-plus/historia-jira-prompt-estudo-keywords-v3]]); sem PRD próprio encontrado no Drive ainda.
- [[03-Produtos/ideal-tracker]] (Ideal Track) — ferramenta de GEO/visibilidade em LLMs; tem PRD, doc de funcionalidades e briefing de UX no Drive, mas com pontos críticos em aberto (ver backlog acima).

## Outras pastas de projeto no Drive (não aprofundadas ainda)
Ideal Sync - Pix Automático BB, Auditoria Ideal, Procedimentos Depto Infraestrutura, Perfil Colaboradores, Infra Central, Ideal Sales, Ideal Multibusiness, SE - Sales Enablement, Ideal Pro, Soluções Industriais, Clínica Ideal, Projeto Matriz.

## Decisões fundadoras
Decisões em [[04-Decisões]] que moldam o funcionamento descrito aqui.
- [[04-Decisões/migracao-prompt-keywords-v2]] — substituição do prompt de avaliação de keywords (v1 → v2): saída passa de tabela de keywords avaliadas para arquitetura completa de site (Pilar → Cluster → Suporte); documenta diferenças de parâmetros e formato de saída para a equipe de tecnologia. Especificação técnica detalhada em [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]].
- [[04-Decisões/padrao-historia-jira]] — formaliza `_templates/template-historia-jira.md` como formato padrão para toda história de mudança técnica no cofre, preparando o terreno para quando o MCP do Jira for conectado.
