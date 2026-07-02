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
