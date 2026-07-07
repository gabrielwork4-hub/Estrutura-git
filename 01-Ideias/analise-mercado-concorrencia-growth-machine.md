---
tipo: ideia
status: validada-parcial
criado: 2026-07-06
ultima-revisao: 2026-07-06
tags: [growth-machine, mercado, concorrencia, geo, seo, aeo, validado-com-fonte]
---

# Análise de mercado/concorrência — Growth Machine (validada com pesquisa ativa em 2026-07-06)

> **Aviso de proveniência, atualizado:** a primeira versão desta nota era
> conhecimento geral do assistente, sem fonte — **foi substituída** pela
> seção "Panorama por frente" abaixo, agora com resultado de pesquisa
> ativa (`WebSearch`, 2026-07-06) e fontes citadas. Ainda não é o mesmo
> nível de rastreabilidade das notas de RN/PRD (não valida constância ao
> longo do tempo, é uma leitura pontual), mas já não é mais especulação
> sem checagem. Nasce da pergunta "existe algo competitivo ou parecido no
> mercado?" feita durante a análise de diferencial competitivo do produto
> (ver [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]]).

## Contexto
Depois de fechar o diagnóstico completo de SEO/GEO/AEO do Growth Machine
e identificar os prováveis diferenciais competitivos (integração GEO via
Ideal Tracker, pilares agênticos/WebMCP, presença off-site), surgiu a
pergunta natural: isso é inédito, ou já existe no mercado? A primeira
resposta foi de memória, sem fonte; esta versão já reflete pesquisa ativa
feita em 2026-07-06.

## Panorama por frente (validado com pesquisa ativa, 2026-07-06)

### SEO técnico tradicional (as 10 dimensões)
Não pesquisado novamente nesta rodada (mantido de leitura anterior, não
verificado) — mercado maduro e disputado, ferramentas como Semrush,
Ahrefs, Screaming Frog, Botify. O Growth Machine não seria pioneiro aqui;
o diferencial é a orquestração proprietária integrada a uma agência com
carteira própria (MPI Plus, Salesforce, governança), não a auditoria em
si.

### GEO (medir citação em LLM) — **correção importante da leitura anterior**
Não é um mercado fragmentado e em disputa aberta — é um mercado **já
maduro e bem financiado**, mais perto de "corrida institucionalizada" do
que de "território livre":
- **Profound** — líder no G2 Winter 2026 na categoria AEO/GEO, US$ 58,5M
  captados (Khosla Ventures, Kleiner Perkins, NVIDIA, Sequoia), SOC 2 Type
  II, monitora 10+ engines, US$ 499/mês.
- **AthenaHQ** — fundada por ex-engenheiros do Google Search/DeepMind.
- **Peec AI** — US$ 29M captados, US$ 4M+ ARR em 10 meses, 9+ modelos
  cobertos, a partir de €89/mês.
- **Scrunch AI** — SOC 2, 8 engines, detecção de alucinação (Enterprise).
- **Otterly.ai** — Gartner Cool Vendor 2025, 20.000+ usuários, a partir de
  US$ 29/mês.

**Ponto que se mantém válido:** todos esses são produtos **isolados de
monitoramento** — nenhum faz auditoria técnica de SEO nem orquestra
execução/ação dentro do mesmo fluxo. A vantagem do Growth Machine
continua sendo a integração num produto só (SEO + GEO + execução), não a
métrica de citação em si — que já tem oferta de mercado madura, cara e
bem capitalizada de replicar do zero.

### Prontidão agêntica (WebMCP, accessibility tree) — confirmado, mais recente do que se estimava
A categoria **"Agentic Browsing" do Lighthouse é real e recente**:
lançada no **Lighthouse 13.3, em 7 de maio de 2026**. Avalia 4 frentes —
llms.txt, protocolo WebMCP, árvore de acessibilidade, CLS (compatível com
os "6 pilares" já mapeados no cofre, já que WebMCP se decompõe em 3
critérios). Ponto importante: **o próprio Lighthouse ainda não dá nota
0-100 nessa categoria** — os padrões da web agêntica "ainda estão
emergindo", o foco atual é coletar dado, não ranquear. Não foi encontrado
nenhum concorrente comercial empacotando essa auditoria como produto
vendável — aqui a leitura de "espaço ainda livre" se sustenta.

## Por que isso está isolado do resto do cofre
Por decisão explícita — mesmo já validada com pesquisa, esta nota ainda é
uma leitura pontual de mercado (não constância documentada ao longo do
tempo como RN/PRD) — nenhuma nota de produto linka pra cá como se fosse
fato definitivo, só como referência datada.

## Próximos passos
- [x] Validar com pesquisa de mercado ativa (`WebSearch`, 2026-07-06) —
  feito, ver seção acima e fontes.
- [ ] Promover os achados de GEO (mercado já maduro/financiado) e de
  pilares agênticos (espaço ainda livre) para dentro de
  [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]] como
  leitura formal, se o PO validar a relevância.
- [ ] Revalidar em 3-6 meses — mercado de GEO está em movimento rápido
  (rodadas de captação, lançamento de features), leitura pode ficar
  desatualizada rápido.

## Fontes (pesquisa de 2026-07-06)
- [Best AI Visibility Tools 2026: Profound vs Peec vs Otterly vs the Rest](https://www.surmado.com/blog/best-ai-visibility-tools-2026)
- [AthenaHQ vs Profound vs Peec.ai: 30-Day GEO Platform Test Results](https://athenahq.ai/index/athenahq-vs-profound-vs-peec-ai-30-day-geo-platform-test-results/)
- [Ayzeo vs Otterly, Peec, Profound & Scrunch - GEO Tool Comparison](https://ayzeo.com/comparisons)
- [Lighthouse agentic browsing scoring — Chrome for Developers](https://developer.chrome.com/docs/lighthouse/agentic-browsing/scoring)
- [Google Lighthouse Has A New Agentic Browsing Category — DebugBear](https://www.debugbear.com/blog/lighthouse-agentic-browsing)
- [Is Your Website Ready for AI Agents? Google's New Lighthouse Agentic Browsing Audit Explained — Lucid Media](https://www.lucidmedia.co.nz/blog/lighthouse-agentic-browsing-llms-txt-webmcp/)

## Notas relacionadas
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]]
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
- [[03-Produtos/ideal-tracker]]
- [[00-Cerebro]]
