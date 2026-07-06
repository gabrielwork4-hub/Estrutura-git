---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-07-06
origem-fluxo: "[[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]"
tags: [growth-machine, geo, agentic-browsing, webmcp, lighthouse]
---

# Implementar auditoria dos 6 pilares agênticos (Agentic Browsing / WebMCP)

## Problema
O Lighthouse já audita uma categoria real chamada **Agentic Browsing**,
com 6 critérios concretos que medem se um agente de IA consegue navegar e
interagir de verdade com o site (não só ler conteúdo pra citar):
accessibility tree well-formed, Cumulative Layout Shift, WebMCP form
coverage, WebMCP tools registered, WebMCP schemas valid, e llms.txt. O
Growth Machine hoje cobre **apenas 1 desses 6** (llms.txt, e só
parcialmente — RN-82 verifica presença, não uso real). Os outros 5 são
ausência total em qualquer uma das 10 dimensões.

## Necessidade de implementação
- **Accessibility tree well-formed** e **Cumulative Layout Shift**: baixa
  necessidade de infraestrutura nova — CLS já é medido indiretamente via
  Core Web Vitals (Dimensão 5); accessibility tree pode reaproveitar
  ferramentas prontas (ex: axe-core) como nova checagem determinística.
- **WebMCP form coverage / tools registered / schemas valid**: necessidade
  alta e nova — depende de o site do cliente sequer **implementar o
  protocolo WebMCP**, o que hoje não é nem cobrado no processo de
  entrega/dev do site. Não é ajuste de regra existente, é capability
  inteiramente nova, incluindo trabalho fora do Growth Machine (no
  processo de construção do site em si).
- **llms.txt**: já parcialmente coberto (RN-82) — precisa evoluir de
  "existe sim/não" para "está estruturado corretamente" (ver também
  [[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]]).

## Importância (pensando em GEO)
Esse é o critério mais concreto e mensurável de "prontidão agêntica" que
existe hoje publicamente (Lighthouse já roda isso em produção, não é
especulação de mercado). Cobrir só 1 de 6 pilares significa que, pela
métrica mais objetiva disponível, o Growth Machine está estruturalmente
despreparado pra a próxima onda de otimização (agentes de IA operando
sites, não só citando conteúdo). É a lacuna mais concreta e verificável de
toda a frente GEO — motivo pelo qual o score de GEO/AEO no comparativo de
maturidade foi revisado para baixo (~20-25%, de ~25-30%) após esse
detalhamento.

## Impacto de não fazer
Enquanto WebMCP e accessibility tree não forem auditados, o Growth Machine
segue medindo "o site é bom pra buscador tradicional e pra ser citado",
mas fica cego pra "o site funciona quando um agente de IA tenta operar
nele" — um critério que já é auditável hoje e tende a virar sinal de
ranqueamento/confiança à medida que navegação agêntica cresce.

## Proposta de ajuste
1. Adicionar accessibility tree e CLS como sub-critérios reaproveitando
   infraestrutura existente (Dimensão 4/5) — baixo custo, alto retorno de
   cobertura (2 de 6 pilares rapidamente).
2. Avaliar com o time técnico se WebMCP deve entrar como requisito de
   processo de construção de site (não só auditoria) — sem o protocolo
   implementado no site, não há o que auditar.
3. Evoluir RN-82 (llms.txt) para checagem de qualidade, não só presença.

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
- Produto: [[03-Produtos/growth-machine]]
- Relacionado: [[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]]
