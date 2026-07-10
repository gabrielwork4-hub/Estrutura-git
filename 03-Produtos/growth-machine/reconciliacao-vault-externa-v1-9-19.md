---
tipo: produto
status: concluida
criado: 2026-07-10
ultima-revisao: 2026-07-10
tags: [growth-machine, reconciliacao, vault-externa, canibalizacao, rn, seo, geo, aeo, google-2026, calibracao-continua]
---

# Reconciliação com a vault externa — "Vault PRD GROWTH MACHINE MODIFICADO" (v1.9.19)

> **Acesso liberado e reconciliação concluída em 2026-07-10.** Registra o
> episódio completo: da colisão de numeração detectada só pela descrição
> do PO, passando pelo bloqueio de acesso, até a leitura completa da vault
> real e a reconciliação ponto a ponto. A vault existe em
> `drive.google.com/drive/folders/1PipUHjPCfWR7L2Op7n4Dc9_cK5hpOZ_T`,
> autoria **Lucas Bevilacqua / Gabriel Santos (gabriel.santos@idealtrends.com.br)**,
> estruturada em 11 pastas temáticas (00-overview a 10-modelo-proposto-v2),
> reorganizando o mesmo PRD monolítico (2.461 linhas) que este cofre também
> trabalha, na versão **v1.9.19** (08/07/2026).

## Descoberta central
A vault externa fez, **de forma independente**, essencialmente o mesmo
trabalho que este cofre: cruzar o PRD oficial, o documento original do
Gregory e boas práticas/dados de mercado 2026, chegando aos **mesmos
achados críticos** (doorway pages, Cluster Wrapping como solução, pesos do
índice incompatíveis) — em alguns pontos com mais rigor que nós. Isso não é
coincidência de nome: é convergência de raciocínio a partir das mesmas
fontes.

## O que confirma, ponto a ponto

| Item | Nossa leitura (antes) | Vault externa | Resultado |
|---|---|---|---|
| Cluster Wrapping | ADR própria (2026-07-10) | Mesma solução, mesmo nome, **cita o emtecorp como exemplo confirmado** | ✅ Validado quase palavra por palavra — ver enriquecimento abaixo |
| Ambiguidade Dim 1 (`<50%`) | Fechada (F-03) | Confirma `<50%` como decisão do PO | ✅ Igual |
| Bright Data / RNs supersedidas | Fechadas (F-01/F-05) | Mesmas correções, já na v1.9.19 | ✅ Igual — convergência confirmada, não coincidência |
| Fonte de posicionamento (relatório mensal × GSC) | C5 — relatório mensal vence | Confirma, **com o motivo real**: teto de cobertura do GSC (6 contas p/ 2.500 clientes, F-14/F-32) | ✅ Reforçado com causa raiz que não tínhamos |
| Pesos do índice | Propusemos 35/20/45 (leitura de mercado) | **Manter 40/40/20 sob revisão**, calibrar por correlação real com outcome de negócio | 🔄 **Nossa ADR corrigida** — ver [[04-Decisões/adr-camada-calibracao-continua]] |
| RN-123/RN-124 | Propusemos extrabilidade/AEO (renumeadas p/ `RN-SGA-*`) | São, na verdade, **confirmação de entrega multicanal + paridade de spam** (achado F-40, auditoria à Dim 10) | ✅ Colisão evitada; RN-123/124 reais incorporadas ao catálogo |

## O que a vault externa traz de genuinamente novo (não tínhamos)

1. **Camada de Calibração Contínua** — mecanismo formal de recalibração
   periódica (trimestral/semestral) com proposta→aprovação→log, extensão do
   padrão `ruleset_version_id` já existente. Adotado como novo caminho para
   RN-18 e outros parâmetros hoje fixos. Ver
   [[04-Decisões/adr-camada-calibracao-continua]].
2. **Portão de Diferenciação Real** — regra de decisão antes de gerar
   qualquer página/artigo por combinação (dado local, prova social
   específica, resposta a pergunta real), com métrica `taxa_diferenciacao_real`
   — complementa o Cluster Wrapping, incorporado à
   [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] e à Dim 1/2/3
   em [[03-Produtos/growth-machine]].
3. **Frente Z1 — auditoria imediata da carteira** por quase-duplicatas
   (FireCrawl sobre a base atual), sem depender de nenhuma decisão — é o
   item mais urgente do roadmap deles inteiro.
4. **Circularidade do `ctr_estimado`** (F-08/F-31): se a posição cai, o
   "potencial" cai junto, mascarando queda real. Proposta: baseline
   defasada (janela saudável, trimestral).
5. **Curva de CTR única erra para clientes locais** — Local Pack tem curva
   muito mais achatada que busca orgânica; precisa de 2 curvas segmentadas.
6. **RN-41 "Tintambi"** é termo não identificado — precisa esclarecimento
   de Lucas/Growth antes de reescrever.
7. **Cobertura de GSC insuficiente** (6 contas para ~2.500 clientes) é o
   teto real por trás de várias decisões já tomadas — expandir para 9-10
   contas ou implementar alocação dinâmica.

## O que ficou por ler (não esgotado, por economia de esforço)
A vault tem ~50 arquivos. Lemos os documentos decisórios centrais (índice,
roadmap consolidado, Cluster Wrapping, anti-doorway, Camada de Calibração
Contínua, Motor Adaptativo, confirmação multicanal). **Não lidos ainda**:
os 14 ADRs individuais (`07-adrs/`), as 10 notas de dimensão detalhadas
(`02-dimensoes/`), o radar de schema (`04-schemas-radar-de-politica.md`),
a matriz de bots de IA (`05-robots-matriz-adaptativa-bots-ia.md`), a
alocação de GSC (`06-gsc-alocacao-dinamica.md`), o loop de GEO
(`03-geo-loop-de-resultado.md`), a revisão crítica completa (29 achados) e
as questões em aberto (Q1-Q30) por extenso. Ficam disponíveis para
aprofundar quando o PO quiser — nada impede leitura pontual sob demanda.

## Ações executadas nesta reconciliação
- [x] RN-18 revertida para 40/40/20, sinalizada "sob revisão" em todas as
  notas que a citavam (catálogo, nota-mãe, cheat-sheet, prep-reunião, PRD v2)
- [x] ADR de pesos original marcada `superada-por-camada-calibracao-continua`
- [x] Nova ADR criada: [[04-Decisões/adr-camada-calibracao-continua]]
- [x] RN-123/RN-124 reais (confirmação de entrega multicanal) incorporadas
  ao catálogo, distintas das nossas `RN-SGA-*`
- [x] RN-41 sinalizada como termo não identificado
- [x] RN-16 sinalizada para segmentação Local Pack × orgânica
- [x] Portão de Diferenciação Real incorporado à nota-mãe e à ADR de cluster
- [x] Anti-canibalização dentro do cluster + auditoria de quase-duplicatas
  incorporadas à Dim 3

## Próximos passos (não executados ainda — ficam para o PO priorizar)
- [ ] Frente Z1 — rodar auditoria de quase-duplicatas na carteira (FireCrawl)
- [ ] Quick wins C3 (backtest `posicionamento_esperado`) e C4 (correlação
  peso×outcome) — sem dependência, podem começar já
- [ ] Emenda à RN-107 (enumerar "demais canais") antes de implementar
  RN-123/RN-124
- [ ] Ler os 14 ADRs individuais e as 10 notas de dimensão da vault externa,
  se o PO quiser aprofundar além do que já foi reconciliado aqui

## Notas relacionadas
- [[04-Decisões/adr-camada-calibracao-continua]] — substitui a ADR de pesos original
- [[04-Decisões/adr-pesos-indice-performance-2026]] — superada
- [[04-Decisões/adr-cluster-informacoes-sem-alterar-contrato]] — validada e enriquecida
- [[03-Produtos/growth-machine/reconciliacao-regras-gregory]] — mesma classe de reconciliação, fonte diferente
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — RN-123/124 reais + todas as correções aplicadas
- [[03-Produtos/growth-machine/plano-fechamento-prd-v2]] — tracker principal
- [[03-Produtos/growth-machine/prd-v2-mvp]] · [[03-Produtos/growth-machine]] · [[00-Painel-Estado]] · [[00-Cerebro]]
