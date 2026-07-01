---
tipo: backlog
status: pronto-para-refinamento
prioridade: alta
criado: 2026-07-01
origem-fluxo: "[[02-Fluxos/prompt-avaliacao-keywords]]"
tags: [mpi-plus, prompt, keywords, jira, historia, seo]
---

# [MPI-XXX] Substituir prompt de avaliação de keywords pelo Estudo SEO Clusterizado (v3)

> História redigida na posição de PO, para o time de DEV. Título/ID Jira
> (`MPI-XXX`) é placeholder — substituir pelo número real ao criar no board.

## Epic
Evolução do pipeline de Estudo/Keywords do IdealPlus (MPI Plus)

## Tipo
Story (mudança de prompt em produção — sem mudança de infraestrutura)

## Contexto (por que esta história existe)
Hoje, a etapa de avaliação de keywords do MPI Plus roda em cima de um
prompt (v1) que avalia **keyword por keyword, isoladamente** — sem
clusterização, sem checagem de canibalização entre páginas, sem content
map e sem plano de execução. Essa limitação já está documentada em
[[02-Fluxos/estudo-de-keywords]] e no comparativo
[[04-Decisões/migracao-prompt-keywords-v2]].

O pipeline de **Construção de Conteúdo** do MPI Plus (SERP Search → Domain
Classification → Pattern Analysis → Structure → Section → Cohesion → QA)
já assume uma `{keyword}` pronta como entrada — ele não decide qual
keyword/página deve existir, nem verifica canibalização entre páginas. Essa
decisão acontece **antes** desse pipeline, e é exatamente o prompt que
estamos substituindo.

O novo prompt (**v3**, texto completo em
[[02-Fluxos/prompt-avaliacao-keywords]]) resolve isso: gera um **Estudo SEO
completo e executável** — cluster de keywords, content map (máx. 25
páginas, 1 keyword principal por página), análise competitiva, estratégia
GEO, briefs de conteúdo, estratégia de linkagem interna, KPIs e plano de
implementação em 3 fases.

## Objetivo da história
Trocar o prompt de produção da etapa de avaliação/clusterização de keywords
(hoje v1) pelo prompt v3, sem alterar o restante do pipeline de Construção
de Conteúdo (SERP Search, Domain Classification, Pattern Analysis,
Structure, Section, Cohesion, QA), que permanece como está.

## Story (formato ágil)
**Como** Product Owner do MPI Plus,
**quero** substituir o prompt de avaliação de keywords existente pelo
prompt v3 (Estudo SEO Clusterizado),
**para que** o sistema pare de gerar keywords soltas e passe a entregar um
estudo com arquitetura de páginas, sem canibalização, com plano de execução
pronto para o time de SEO/copywriting.

## Escopo desta história (o que muda)

| Item | Hoje (v1) | Depois (v3) |
|---|---|---|
| Unidade de saída | Lista de keywords avaliadas (intenção/especificidade/relevância/justificativa) | Estudo SEO completo: cluster de keywords + content map + análise competitiva + GEO + briefs + linkagem interna + KPIs + plano de implementação |
| Volume de keywords | Não especificado | Mínimo 50–80 keywords, organizadas em 8 clusters obrigatórios (Pillar/Core, Problemas/Sintomas, Serviços específicos, Marcas, GEO local, Comparação/preço/decisão, FAQ, Long-tail) |
| Canibalização | Não verificada | Regra explícita: máximo 1 keyword principal por página; content map limitado a 15–25 páginas |
| Critério de corte | Não definido | Descartar (não incluir na tabela final) qualquer keyword com relevância < 3 |
| Análise competitiva | Inexistente | Top 5 concorrentes (DR estimado, tráfego, força, fraqueza, oportunidade de ataque) + 3 oportunidades de ganho de mercado |
| SEO local | Não tratado no prompt de avaliação | Pirâmide de localização (primária/secundária/terciária) com landing page, keywords locais, estratégia de conteúdo e SEO local (GBP, schema, citações) por nível |
| Briefs de conteúdo | Inexistente | Brief completo (H1/H2/H3, seções obrigatórias, diferencial, CTAs, extensão) para as 5 páginas mais importantes |
| Linkagem interna | Inexistente | Fluxo de autoridade Homepage→Pilares→Serviços→Long-tail, anchors recomendados, profundidade máx. 3 cliques |
| KPIs | Inexistente | Tráfego, keywords ranqueadas, leads, CTR, ranking local, DR — com meta de 6 meses, ferramenta e frequência de medição |
| Plano de implementação | Inexistente | 3 fases (0–4 sem. / 5–12 sem. / 13+ sem.) |

**Fora de escopo desta história:** qualquer alteração no pipeline de
Construção de Conteúdo (`domain_classification`, `pattern_analysis`,
`structure`, `section`, `cohesion`, `qa`) documentado no guia de prompts do
IdealPlus — este pipeline continua recebendo `{keyword}` normalmente,
agora just vinda de um estudo mais robusto.

## Critérios de aceite
1. **Dado** um briefing de empresa/produto completo, **quando** o estudo
   for executado com o prompt v3, **então** o sistema deve retornar as 8
   seções obrigatórias na ordem: Cluster de Keywords, Content Map, Análise
   Competitiva, Estratégia GEO (quando aplicável), Briefs de Conteúdo,
   Internal Linking Strategy, KPIs, Plano de Implementação.
2. **Dado** o cluster de keywords gerado, **quando** qualquer keyword tiver
   relevância < 3, **então** ela não deve aparecer na tabela final entregue.
3. **Dado** o content map gerado, **quando** for auditado, **então** cada
   página deve ter exatamente 1 keyword principal, sem repetição de keyword
   principal entre páginas (zero canibalização), e o total de páginas deve
   estar entre 15 e 25.
4. **Dado** um nicho sem componente geográfico relevante, **quando** o
   estudo for gerado, **então** a seção de Estratégia GEO pode ser omitida
   ou marcada como não aplicável, sem quebrar o restante da saída.
5. **Dado** o estudo completo, **quando** entregue ao time de SEO/
   copywriting, **então** deve ser executável sem necessidade de
   interpretação adicional (briefs já contêm H1/H2/H3, CTAs e extensão).
6. **Dado** o pipeline de Construção de Conteúdo existente, **quando** a
   keyword de uma página do novo content map for usada como `{keyword}` de
   entrada, **então** o pipeline deve continuar funcionando sem alteração
   de contrato/formato de entrada.

## Tarefas técnicas sugeridas (para o DEV detalhar/refinar)
- [ ] Localizar o serviço/endpoint que hoje executa o prompt v1 de
  avaliação de keywords no MPI Plus (equivalente ao `BriefingProcessJob` do
  pipeline de Estudo, ou job próprio se a avaliação de keywords for uma
  etapa separada).
- [ ] Substituir o prompt de sistema/usuário atual pelo texto do prompt v3
  (ver [[02-Fluxos/prompt-avaliacao-keywords]] para o texto integral).
- [ ] Validar/mapear os placeholders do v3 (`{$empresaNome}`,
  `{$segmentosAtuacao}`, `{$tipoEmpresa}`, `{$publicoAlvoEmpresa}`,
  `{$nomePrincipal}`, `{$nomeSecundario}`, `{$outrosNomes}`,
  `{$tipoProduto}`, `{$especificacaoTecnica}`, `{$funcionalidades}`,
  `{$beneficios}`, `{$publicoAlvoProduto}`, `{$informacoesAdicionais}`)
  contra os campos reais do briefing no banco — confirmar que todos existem
  e estão populados corretamente.
- [ ] Definir e implementar o parser da nova saída (8 seções, várias
  tabelas) — **não é compatível com o parser do v1** (que tratava só uma
  lista simples de keywords).
- [ ] Definir onde os campos livres do prompt (`Nicho`, `Localização`,
  `Objetivo: LEADS/VENDAS/SEO LOCAL/AUTORIDADE`) são preenchidos — hoje
  aparecem como texto livre `[EX: ...]` no prompt, não como variável
  `{$...}` — decidir se viram novos campos de briefing ou se ficam como
  input manual do analista/CS.
- [ ] Validar limite de tokens/contexto da chamada, já que a saída é
  significativamente maior que a do v1 (8 seções vs. 1 tabela).
- [ ] Confirmar que o `{keyword}` consumido downstream pelo pipeline de
  Construção de Conteúdo (`pattern_analysis`, `structure`, `section`)
  recebe corretamente a keyword principal definida no Content Map do v3,
  sem quebra de contrato.
- [ ] Rodar teste A/B ou golden-set comparando saída v1 vs. v3 para pelo
  menos 3 briefings reais antes de promover para 100% do tráfego.

## Riscos e pontos de atenção (para o time técnico avaliar)
- **Sem regra anti-alucinação explícita no v3** (diferente do pipeline de
  Conteúdo, que injeta `{anti_hallucination_rule}` em 5 etapas) — avaliar
  se a Análise Competitiva (DR estimado, tráfego estimado) e as métricas de
  KPI podem gerar números "estimados" sem fonte real, o que é um padrão que
  o restante do MPI Plus evita explicitamente em outros pipelines.
- **Volume de saída (50-80 keywords + 8 seções) é uma mudança grande de
  contrato** — times consumidores da saída anterior (v1) provavelmente
  quebram se não houver adaptação do parser.
- **Sem critério de corte para análise competitiva/GEO** equivalente ao
  "relevância < 3" do cluster de keywords — a qualidade dessas seções
  depende inteiramente do prompt, sem validação determinística.

## Definition of Done
- [ ] Prompt v3 em produção substituindo o v1 na etapa de avaliação de
  keywords do MPI Plus.
- [ ] Parser da nova saída implementado e testado.
- [ ] Critérios de aceite 1-6 validados em ambiente de homologação.
- [ ] Golden-set de pelo menos 3 briefings reais comparando v1 vs. v3
  aprovado pelo time de SEO.
- [ ] Documentação atualizada em [[02-Fluxos/prompt-avaliacao-keywords]]
  com status `ativo` para v3 (hoje `candidato`).

## Relacionados
- [[02-Fluxos/prompt-avaliacao-keywords]] — texto completo dos prompts v1, v2 e v3
- [[02-Fluxos/estudo-de-keywords]] — fluxo de origem (clusterização, anti-canibalização, variação local)
- [[04-Decisões/migracao-prompt-keywords-v2]] — decisão e comparativo anterior (v1→v2)
- [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]] — especificação técnica anterior
- [[03-Produtos/mpi-plus]] — produto onde o pipeline roda
