---
tipo: produto
status: bloqueada-aguardando-acesso
criado: 2026-07-10
ultima-revisao: 2026-07-10
tags: [growth-machine, reconciliacao, vault-externa, canibalizacao, rn, seo, geo, aeo, google-2026]
---

# Reconciliação com vault externa (PRD v1.9.19 + pasta "10-modelo-proposto-v2")

> Registra um episódio crítico: o PO descreveu, em texto, o conteúdo de uma
> **vault externa** (não este cofre, não o Drive já mapeado) contendo uma
> versão do PRD mais avançada (**v1.9.19**, contra a v1.9.14 que temos no
> Drive) e uma pasta de propostas não aprovadas
> (**`10-modelo-proposto-v2`**). O cruzamento revelou uma **colisão real de
> numeração de RN** contra o que construímos nesta sessão — corrigida na
> hora. Acesso ao arquivo real segue **pendente**.

## O que o PO descreveu (v1.9.19, resumo)
Mesmo produto, mesmas 4 fases + 10 dimensões + módulo Sentinela + 11 telas
já conhecidos deste cofre, com 3 diferenças relevantes em relação ao que
tínhamos mapeado:

1. **Índice de Performance ainda em 40/40/20`** (posição/tráfego/leads) —
   **diferente** da nossa ADR (35/20/45,
   [[04-Decisões/adr-pesos-indice-performance-2026]]).
2. **Dimensão 8 (Search Console) já inclui CWV real** ("evidência real de
   indexação, impressões, cliques, CWV") — dado novo, não estava explícito
   no que tínhamos antes; mitiga parte da preocupação com RN-07 (PageSpeed
   Score como proxy), se esse dado de fato alimentar decisão.
3. **3 correções já presentes**: resíduo de Bright Data removido, threshold
   da Dim 1 em `<50%`, RNs supersedidas marcadas — **idênticas** ao que
   fechamos no F-01/F-03/F-05. Convergência ainda não explicada (aplicado
   lá a partir daqui, ou paralelo independente) — **pergunta em aberto**.

### Pasta "10-modelo-proposto-v2" (não aprovada, resumo)
- **Camada de Calibração Contínua** — CTR/pesos/régua adaptativos. É,
  pelo nome, o mecanismo formal de governança para o tipo de mudança que
  fizemos na ADR de pesos. Recomendação: tratar a ADR como **entrada para
  essa camada**, não como decisão unilateral fechada e paralela a ela.
- **Cluster Wrapping** — **mesmo nome, mesma lógica** da nossa
  [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]]. Validação
  cruzada forte: chegamos à mesma solução por caminhos diferentes (caso
  real emtecorp + exclusão de `/informacoes` no PRD do Gregory + core
  update 2026) — não é coincidência de nome à toa, é o mesmo problema
  (doorway pages) com a mesma resposta.
- **RN-123 / RN-124 = "paridade de canal em leads"** — **colide** com as
  RN-123/RN-124 que este cofre havia proposto (extrabilidade / resposta
  única AEO). Ver ação abaixo. Conteúdo completo dessas RNs ainda
  **desconhecido** — só o rótulo foi descrito; possível relação com
  RN-107/RN-110 (leads multicanal), não confirmada.

## Tentativa de acesso (resultado: bloqueado)
- Busca por texto no Drive já mapeado (`fullText contains 'Cluster
  Wrapping'`, `'10-modelo-proposto'`, `'v1.9.19'`): **nada encontrado** —
  confirma que é uma fonte genuinamente separada do Drive que já
  cruzamos.
- Link de pasta fornecido pelo PO
  (`drive.google.com/drive/folders/1PipUHjPCfWR7L2Op7n4Dc9_cK5hpOZ_T`):
  `search_files` retornou vazio e `read_file_content` retornou "Requested
  entity was not found" — **sem acesso** com a conta conectada nesta
  sessão.
- **Ação pendente do PO**: compartilhar a pasta com a conta usada por este
  agente, ou colar/anexar o conteúdo real diretamente na conversa.

## Ação tomada agora (não esperou o acesso): renumeração RN-SGA-*
Para não deixar a colisão viva enquanto o acesso não é liberado, as 16 RNs
propostas nesta sessão foram **renumeradas de RN-123–138 para
`RN-SGA-01` a `RN-SGA-16`** (SEO/GEO/AEO), liberando 123/124 para a vault
externa. Mesmo padrão de namespace já usado para as regras do Gregory
(`RN-EST-*`). Atualizado em:
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]]
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]]
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] (convenção G2)

**Isto é uma correção provisória**, não a reconciliação final — quando o
conteúdo real da pasta `10-modelo-proposto-v2` for acessível, este
namespace pode precisar de novo ajuste (e o próprio conteúdo das 16 RNs
precisa ser comparado ponto a ponto com o que já existe lá, para não
duplicar proposta).

## Veredito direto — as 4 dores, hoje (v1.9.19 oficial, sem a pasta proposta)

| Dor | Atende hoje? | Leitura |
|---|---|---|
| **Canibalização** | 🟡 Parcial | Prevenida só na etapa de **planejamento** (Dim 1 audita conformidade estudo↔briefing; Dim 3 audita se a linkagem segue o pilar→variação *previsto*). Nenhuma dimensão audita canibalização **viva na SERP** nem entre subdomínios (o caso www×loja do emtecorp não seria pego hoje). |
| **Ranqueamento** | 🟢 Sim, de forma abrangente | As 10 dimensões cobrem os fatores clássicos (conteúdo vs. SERP, link equity, HTML/schema/sitemap determinísticos, infra). Se a Dim 8 realmente traz CWV real via GSC, resolve parte do gap de RN-07. Falta: nenhuma ofensiva de autoridade/backlink foi mencionada na descrição — se não existe, é o maior buraco de ranqueamento hoje. |
| **Intenção de busca** | 🟡 Parcial | Resolvida na **geração** (MPI Plus classifica intenção), auditada só **indiretamente** na Dim 2 via comparação com padrão da SERP — proxy razoável, mas sem checagem explícita de conformidade de intenção pós-publicação. |
| **AEO × GEO** | 🔴 Não | Confirma o diagnóstico já feito: GEO existe só como preparação estrutural (FAQ/headings, Dim 2), zero medição, zero peso no Índice. AEO não existe como conceito na v1.9.19 oficial. Bate com a decisão F-28 (medição de GEO = Fase 2). |

## As novas análises desta sessão fazem sentido? Veredito
**Sim na direção, com 2 status rebaixados até reconciliar:**
1. **Cluster Wrapping** — validado de forma independente (mesmo nome, mesma
   lógica já na pasta proposta da vault externa). Reforça priorizar a
   promoção de "proposta" para "aprovada".
2. **Pesos 35/20/45** — racional se sustenta (zero-click 60%, CTR pos.1
   ~27%→~11% com AI Overview), mas como a v1.9.19 oficial ainda mostra
   40/40/20 e existe uma "Camada de Calibração Contínua" que parece ser o
   canal certo, a ADR deveria alimentar essa camada, não competir com ela
   — **rever status de "aceita" para "proposta" até confirmar o canal**.
3. **RN-SGA-01–16** — bloqueadas de virar "oficiais" até o conteúdo real
   da pasta proposta ser lido e comparado ponto a ponto.

## Próximos passos
- [ ] PO libera acesso à pasta `10-modelo-proposto-v2` (ou cola o conteúdo)
- [ ] Ler v1.9.19 completa e comparar linha a linha contra
  [[03-Produtos/growth-machine/prd-v2-mvp]] (base ainda é v1.9.14)
- [ ] Confirmar se as 3 correções (Bright Data, threshold Dim 1,
  supersedidas) já vieram deste cofre ou foram paralelas
- [ ] Comparar RN-123/RN-124 reais (paridade de canal em leads) com
  RN-107/RN-110
- [ ] Decidir se a ADR de pesos vira input formal da Camada de Calibração
  Contínua, mantendo ou revertendo o status "aceita"

## Notas relacionadas
- [[04-Decisões/adr-pesos-indice-performance-2026]] — status a revisar
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] — validado externamente
- [[03-Produtos/growth-machine/mapa-estruturacao-seo-geo-aeo]] — RN-SGA-01–16 renumeradas aqui
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — tracker principal
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — mesma classe de reconciliação, fonte diferente
- [[03-Produtos/growth-machine/prd-v2-mvp]] · [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
