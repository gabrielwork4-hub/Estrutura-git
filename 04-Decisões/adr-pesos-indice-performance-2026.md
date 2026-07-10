---
tipo: decisao
status: superada-por-camada-calibracao-continua
criado: 2026-07-10
ultima-revisao: 2026-07-10
tags: [growth-machine, indice-performance, rn-18, gregory, seo, geo, google-2026]
---

# Pesos do Índice de Performance: 35 posicionamento / 20 tráfego / 45 leads

> **SUPERADA (2026-07-10) — acesso à vault externa liberado e reconciliado.**
> A vault real (autoria Lucas Bevilacqua/Gabriel Santos, cruzando as mesmas
> 3 fontes: PRD, Gregory, ata) chegou a uma resposta mais rigorosa: manter
> **40/40/20 vigente, com flag explícita "sob revisão"**, e calibrar por
> **correlação real com outcome de negócio** (renovação/upsell/churn) via
> uma **Camada de Calibração Contínua** formal — não por leitura de mercado
> genérica. Essa decisão é estritamente mais forte (dado da própria
> operação > estatística de mercado). **A decisão vigente agora é
> [[04-Decisões/adr-camada-calibracao-continua]].** Esta nota permanece
> como registro histórico do racional de zero-click/AI Overview, que passa
> a ser **insumo** da calibração, não substituto dela. Ver
> [[03-Produtos/growth-machine/reconciliacao-vault-externa-v1-9-19]] para o
> episódio completo.

## Contexto
O PRD original do Growth Machine (v1.9.14) fixava o Índice de Performance
em **40% posicionamento / 40% tráfego / 20% leads**, sem origem documentada
(ver [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]]).

As regras entregues pelo **Gregory** (fonte autoritativa da régua de
Growth) trazem **40/30/30** — já reduzindo o peso do tráfego a favor de
leads, coerente com o kickoff original ("Lead é a principal grandeza") —
ver [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] (conflito
C1).

Ao avaliar qual proposta adotar, cruzamos com o consenso de mercado sobre
SEO em 2026: **60% das buscas no Google terminam sem clique** (zero-click),
o CTR da posição 1 caiu de ~27% para ~11% onde há AI Overview, e o
framework de KPI 2026 recomendado por especialistas trata **tráfego como
sinal cada vez menos confiável** de sucesso — "uma queda de 30% em sessões
orgânicas com aumento de 15% em conversões é uma **melhoria** de SEO, não
uma falha" é citado como o novo consenso. Visitante que clica numa resposta
de IA converte **23x mais** que busca tradicional. Fontes: [SEO KPIs in a
World of Zero-Click SERPs](https://www.reflectdigital.co.uk/blog/seo-kpis-in-a-world-of-zero-click-serps),
[60% Zero-Click Searches: The 2026 SEO Crisis Strategy](https://www.digitalapplied.com/blog/60-percent-searches-zero-click-crisis-2026-seo-strategy),
[Measuring Success: New SEO KPIs for the AI-First Era 2026](https://www.clickrank.ai/new-seo-kpis-for-the-ai-first-era/).

Ou seja: nem 40/40/20 nem 40/30/30 vão tão longe quanto os dados de 2026
sugerem — os dois ainda dão a tráfego peso igual ou próximo ao de
posicionamento, quando tráfego é justamente o sinal mais erodido pela busca
generativa.

## Decisão
Fixar o Índice de Performance (RN-18) em **35% posicionamento / 20%
tráfego / 45% leads**.

- **Posicionamento (35%)** — mantido como insumo relevante: é o que a SEO
  controla diretamente e o que alimenta elegibilidade de citação em IA
  (GEO), mas não mais empatado com tráfego.
- **Tráfego (20%, reduzido de 40%)** — rebaixado por ser o sinal mais
  distorcido pelo zero-click/AI Overview: uma página bem posicionada pode
  perder tráfego por motivo estrutural do mercado, não por falha do
  trabalho de SEO.
- **Leads (45%, elevado de 20%)** — passa a ser o componente dominante,
  como o "resultado real de negócio" que o framework de KPI 2026 recomenda
  priorizar (conversão/pipeline acima de sessões).

Continua **parametrizável na Tela 8** (RN-18/RN-122) — este é o default
calibrado, não um valor hardcoded; pode ser recalibrado com dado real de
operação.

**Nota para a Fase 2:** esta reponderação **não substitui** a necessidade
de medir GEO/citação em LLM ([[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]]) —
são frentes complementares. Reduzir o peso de tráfego mitiga parcialmente a
distorção do zero-click sobre o índice atual, mas não adiciona um sinal de
visibilidade em IA — isso segue dependendo da Dimensão 11 (GEO/Citação)
planejada em [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]].

## Alternativas consideradas
- **Manter 40/40/20** — descartado: não reflete nem a direção do Gregory
  nem o consenso de mercado 2026 sobre confiabilidade de tráfego.
- **Adotar 40/30/30 do Gregory sem ajuste** — descartado como final: é a
  direção certa, mas o dado de zero-click/AI Overview justifica ir além.
- **Adicionar um 4º componente (citação em IA) agora, recalculando pesos
  entre 4 sinais** — descartado para o MVP: a métrica de citação
  (Ideal Tracker) ainda não está plugada ao Motor de Percepção (F-28,
  Fase 2); forçar um peso sem dado real geraria número artificial.

## Consequências
- **Positivo**: o Índice deixa de penalizar clientes bem posicionados só
  porque o tráfego caiu por erosão de zero-click — mais justo e mais
  alinhado ao que o Google está de fato recompensando em 2026.
- **Positivo**: origem e racional documentados — resolve a lacuna "números
  de negócio sem origem" identificada em
  [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] para RN-18.
- **Negativo / ação necessária**: muda a classificação (Ruim/Regular/Bom/
  Ótimo) de parte da carteira ativa — requer reprocessamento/recalibração
  anunciada antes de entrar em produção, e validação com o Gregory antes do
  build (ele ainda não viu o dado de zero-click aplicado à régua dele).
  Ver [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]].
- **Negativo / risco**: sem dado real de conversão da própria carteira MPI
  ainda validando este split — é uma extrapolação de boas práticas de
  mercado, não um teste interno. Recalibrar após primeiro ciclo real.

## Relacionados
- RN-18 (pesos do índice): [[03-Produtos/growth-machine/catalogo-regras-negocio]]
- Conflito C1 (origem da divergência): [[03-Produtos/growth-machine/reconciliacao-regras-gregory]]
- PRD consolidado: [[03-Produtos/growth-machine/prd-v2-mvp]] (Bloco 5 RF-11, Bloco 7)
- Fila de calibração: [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]]
- [[03-Produtos/growth-machine]] · [[00-Cerebro]]
