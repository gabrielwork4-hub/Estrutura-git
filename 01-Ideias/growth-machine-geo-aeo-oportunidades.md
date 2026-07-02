---
tipo: ideia
status: bruta
criado: 2026-07-02
tags: [growth-machine, geo, aeo, seo, oportunidade, ideal-tracker]
---

# Growth Machine — oportunidades de GEO/AEO e busca generativa

## Contexto
Surgiu de uma avaliação de alinhamento do fluxo do Growth Machine com
práticas atuais de SEO/GEO/AEO (2026-07-02), cruzando o PRD já documentado
em [[03-Produtos/growth-machine]] com o estado da arte de otimização para
busca generativa (ChatGPT, AI Overview, Perplexity). Avaliação completa
registrada em [[03-Produtos/growth-machine/avaliacao-fluxo]], bloco
"Alinhamento SEO/GEO/AEO com práticas atuais do Google".

Esta nota é o espaço solto para as ideias e oportunidades de melhoria
futura — não é compromisso de roadmap, é registro de possibilidade.

## Descrição
O Growth Machine hoje **otimiza para ser citável**, mas **não mede se está
sendo citado**. Ele prepara estrutura (Dimensão 2C, RN-82, Schema), mas o
Índice de Performance que decide prioridade de cliente é 100% métricas de
SEO tradicional (posicionamento, tráfego, leads) — nenhum componente de
GEO/AEO real.

A oportunidade central: **essa métrica de citação já existe no cofre**,
só que isolada — é o que o [[03-Produtos/ideal-tracker]] mede (Share of
Voice em LLM). Os dois produtos nunca foram pensados juntos.

Outras oportunidades identificadas na mesma avaliação:
- Segmentar tráfego de origem de IA (ChatGPT, Perplexity) no GA4, hoje
  invisível dentro do tráfego orgânico genérico.
- Sinal de "conteúdo original/dado exclusivo" — motores generativos
  preferem citar informação que não é replicada de outras fontes.
- Presença de entidade (Knowledge Graph, Wikidata, consistência de marca)
  como fator de aparecer em respostas de IA.
- Cobertura de vídeo — hoje ausente das 10 dimensões, mas crescente em
  resultados de busca e respostas de IA.
- Evoluir RN-82 de "existe o arquivo sim/não" para avaliar se o
  AI Instructions/LLM.txt realmente ajuda a IA a entender o site.
- Revisar a cadência de 6 meses de revisão de conteúdo (RN-59) — pode ser
  lenta demais para o ritmo de atualização que busca generativa recompensa.

## Próximos passos
- [ ] Validar com o time de produto se integrar Growth Machine + Ideal
  Tracker faz sentido de negócio (não é óbvio que devam ser o mesmo
  sistema — pode fazer mais sentido como sinal de entrada, não fusão).
- [ ] Priorizar, dentre as oportunidades listadas, quais viram item formal
  de [[05-Backlog]] primeiro.
- [ ] Acompanhar se o mercado de GEO/AEO amadurece (ex: API oficial de AI
  Overview) antes de investir pesado nessa frente — hoje o próprio Ideal
  Tracker registra que não há API oficial (ver
  [[05-Backlog/ideal-track-definir-metodologia-sov]]).

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[03-Produtos/ideal-tracker]]
- [[03-Produtos/mapa-dependencia-produtos]]
