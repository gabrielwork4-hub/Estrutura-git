---
tipo: revisao
status: levantamento-em-aberto
criado: 2026-07-07
ultima-revisao: 2026-07-07
origem: "Revisão Crítica PRD Growth Machine v1.0 — autor Claude, revisão solicitada por Will"
tags: [growth-machine, prd, revisao, levantamento, questionamento, seo, geo, aeo]
---

# Revisão Crítica do PRD v1.0 — frente de levantamento e questionamento

> **Natureza desta nota:** registro de uma frente de trabalho **externa** à
> análise SEO/GEO/AEO que vínhamos construindo — feita por outro fluxo de
> revisão (Will), com 29 achados (F-01 a F-29) e decisões já tomadas pelo
> PO. Não é reconciliada com o restante do cofre ainda — esta nota existe
> para **levantar e questionar** onde ela se cruza, confirma ou diverge do
> que já documentamos, sem reescrever nada existente por enquanto. Trata-se
> de matéria-prima para uma reconciliação futura, não de fato já unificado.

## O que é o documento de origem
Revisão crítica formal do PRD do Growth Machine, com escopo na Fase 1
(auditoria + relatoria + fila de ações). Traz 29 achados numerados,
priorizados em P0 (decidir antes do dev) / P1 (corrigir no documento) /
P2 (completar especificação), cada um já com **decisão registrada do PO**
— diferente da nossa `avaliacao-fluxo.md`, que traz recomendação crítica
mas não decisões formalmente fechadas.

## Pontos de cruzamento com a análise SEO/GEO/AEO já construída

### F-28 confirma, e formaliza, o gap central que já tínhamos identificado
> "GEO na V1 deve ser preparação, não promessa de medição." Decisão do PO:
> GEO/AEO na V1 é checklist técnico/semântico — **não deve prometer medir
> presença real em respostas de IA**. Mensuração de GEO, AI Overviews e
> citações em assistentes fica **explicitamente para Fase 2**.

Isso é validação independente do achado central de
[[03-Produtos/growth-machine/avaliacao-fluxo]] ("o GM prepara o site para
ser citável, mas nunca mede se ele está sendo citado"). A diferença: ali
era leitura nossa; aqui é **decisão formal do PO já registrada**.

**Questionamento em aberto:** isso muda o enquadramento da oportunidade
#7 da nossa fila única
([[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]] —
integração Ideal Tracker → aba GEO)? Ela deixa de ser só "oportunidade a
priorizar" e passa a ter respaldo oficial como item de Fase 2 — o que
pode tanto **fortalecer** o argumento (não é fora de escopo, é o próximo
passo natural já reconhecido) quanto **enfraquecer a urgência** (se já
está formalmente adiado para Fase 2, pode virar argumento contra
priorizar agora). Não resolvido — precisa de leitura do PO/liderança.

### Divergência de numeração de versão do PRD (não reconciliada)
Todo o cofre cita **"PRD v1.9.14"** (`growth-machine.md`,
`catalogo-regras-negocio.md`, `comparativo-maturidade-seo-geo.md`, entre
outras). O documento de origem desta nota formaliza a versão oficial como
**v1.0**, tratando as marcações v1.9.x como "resíduos das iterações com
IA" (F-02 do documento).

**Questionamento em aberto:** as notas do cofre precisam ser corrigidas
para "v1.0", ou "v1.9.14" continua sendo a referência válida até essa
mudança ser confirmada por quem gerencia o PRD oficial? Não sei responder
sozinho — depende de qual documento é hoje a fonte de verdade real fora
do cofre.

### RNs marcadas como supersedidas no documento de origem, sem marcação equivalente no catálogo do cofre
F-05 lista como **[SUPERSEDIDA]**: RN-21/22/23 (substituídas por
RN-107/RN-121, leads multicanal), RN-29 (contradiz réguas por dimensão) e
RN-32 (contradiz RN-88, travamento condicional). O nosso
[[03-Produtos/growth-machine/catalogo-regras-negocio]] mantém essas RNs
sem qualquer marcação de que estariam superadas.

**Questionamento em aberto:** nenhuma dessas RNs foi citada diretamente
nas análises SEO/GEO/AEO já fechadas (verificado por busca no
`principios-nucleo-seo-geo-aeo.md` e no `versao-final-hoje-x-desenvolvimento-seo-geo-aeo.md`
— sem ocorrência). Ou seja, **não invalida** nenhuma conclusão já
registrada sobre SEO/GEO/AEO, mas o catálogo geral do cofre está
desatualizado nesse ponto e deveria ser corrigido em algum momento.

### Outros achados do documento sem overlap direto com SEO/GEO/AEO (registrados só para referência)
F-01 (Bright Data), F-03/F-04 (thresholds de dimensão), F-08/F-09/F-10
(fórmula do Índice de Performance/CTR), F-13/F-14 (capacidade de
PageSpeed/GSC), F-21/F-22/F-23/F-24 (artefatos de engenharia — ERD,
máquinas de estado, contratos de integração) — todos relevantes para o
produto como um todo, mas fora do escopo direto da frente SEO/GEO/AEO já
fechada. Não foram cruzados em detalhe nesta nota.

## Por que isso fica registrado como "levantamento", não como fato incorporado
Por decisão explícita: o documento de origem é denso (29 achados, 13
candidatos a ADR) e merece reconciliação própria, cuidadosa, quando houver
tempo dedicado a isso — misturar isso agora dentro das notas já fechadas
de SEO/GEO/AEO (`versao-final-hoje-x-desenvolvimento-seo-geo-aeo.md`,
`comparativo-maturidade-seo-geo.md`) arriscaria reescrever conclusões já
validadas sem a devida checagem ponto a ponto.

## Próximos passos
- [ ] Confirmar com quem gerencia o PRD oficial qual é a numeração de
  versão vigente (v1.0 vs. v1.9.14) antes de propagar correção pelo cofre.
- [ ] Marcar RN-21/22/23/29/32 como `[SUPERSEDIDA]` no catálogo, se a
  divergência de versão for confirmada.
- [ ] Decidir com o PO/liderança se F-28 (GEO como Fase 2 oficial) muda a
  prioridade da integração Ideal Tracker na fila única de oportunidades.
- [ ] Se/quando houver tempo dedicado, cruzar os outros 24 achados
  (F-01/03/04/08-24) contra o restante do cofre, fora do escopo SEO/GEO/AEO.

## Notas relacionadas
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[03-Produtos/growth-machine/comparativo-maturidade-seo-geo]]
- [[03-Produtos/growth-machine/principios-nucleo-seo-geo-aeo]]
- [[03-Produtos/growth-machine/versao-final-hoje-x-desenvolvimento-seo-geo-aeo]]
- [[03-Produtos/growth-machine/catalogo-regras-negocio]]
- [[03-Produtos/growth-machine/briefing-lideranca-seo-geo-aeo]]
- [[00-Cerebro]]
