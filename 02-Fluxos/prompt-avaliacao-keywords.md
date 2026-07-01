---
tipo: fluxo
status: ativo
criado: 2026-06-30
ultima-revisao: 2026-06-30
tags: [seo, keywords, prompt, llm, arquitetura-site]
---

# Prompt de Avaliação de Keywords

## Objetivo
Documentar e versionar o prompt usado para um especialista-IA avaliar
keywords (intenção, especificidade, relevância) para um único produto/serviço
por vez. Este prompt é o que materializa, na prática, as regras descritas em
[[02-Fluxos/estudo-de-keywords]] — por isso toda alteração nele precisa ser
validada contra aquele fluxo.

## Por que foi revisado
O fluxo [[02-Fluxos/estudo-de-keywords]] foi ajustado em 2026-06-30 para
exigir **clusterização por intenção**, checagem de **canibalização** (cada
cluster → uma única página-alvo) e tratamento de **variações locais** como
parte do mesmo cluster. O prompt v1 avaliava keyword por keyword,
isoladamente (intenção/especificidade/relevância individuais) — não tinha
nenhuma etapa de clusterização, de checagem de canibalização entre keywords,
nem de tratamento específico de variação local. O v2, registrado abaixo,
resolve essas lacunas e vai além: gera a **arquitetura completa de páginas
do site** (Pilar → Cluster → Conteúdo de Suporte), não só uma avaliação de
keywords soltas.

Para a documentação de validação voltada à equipe de tecnologia, com o
comparativo lado a lado e o motivo de cada mudança, ver
[[04-Decisões/migracao-prompt-keywords-v2]].

## Histórico de versões
| Versão | Data | Mudança | Motivo |
|---|---|---|---|
| v1 | (anterior, data de criação não registrada) | Versão original — avaliação individual de keyword (intenção, especificidade, relevância 0-5, justificativa) | Baseline em uso até 2026-06-30 |
| v2 | 2026-06-30 | Saída passa de "lista de keywords avaliadas" para **arquitetura de site** (Pilar → Cluster → Suporte), com clusterização semântica, anti-canibalização explícita e SEO local incorporado como tipo de pilar | Alinhar o prompt ao ajuste registrado em [[02-Fluxos/estudo-de-keywords]] e decidido em [[04-Decisões/migracao-prompt-keywords-v2]] |
| v3 | 2026-07-01 | Expande o v2 mantendo o foco em **palavras para produção de conteúdo mais exata e ajustada**: cluster de keywords (intencao/especificidade/relevancia/justificativa, reaproveitando a modelagem de saída do "validador de keywords" do v1/v2), Content Map (15-25 páginas, 1 keyword principal por página), Análise Competitiva (Top 5) e Estratégia GEO (pirâmide de localização). Não inclui Briefs de Conteúdo, Internal Linking, KPIs nem Plano de Implementação — cortados em 2026-07-01 para manter o prompt focado em keywords/arquitetura, não em execução de conteúdo | Levar o estudo de keywords a um artefato de arquitetura + competição + GEO, sem expandir para escopo de execução (briefs, linkagem, KPIs, cronograma), que fica fora deste prompt |

**Nota de escopo (v3):** o v3 é o prompt candidato a **substituir a etapa de
avaliação/clusterização de keywords que hoje roda antes do pipeline de
"Construção de Conteúdo" do MPI Plus** (ver cruzamento com
[[03-Produtos/mpi-plus]]) — o pipeline de conteúdo documentado no MPI Plus
já recebe `{keyword}` pronta (SERP Search → Domain Classification →
Pattern Analysis → Structure → Section → Cohesion → QA); ele **não contém**,
hoje, nenhuma etapa de clusterização/anti-canibalização/content map — essa
etapa roda antes e fora desse pipeline. O v3 é o candidato a preencher essa
lacuna upstream.

## Prompt v1 (versão anterior — registrado em 2026-06-30 para referência)

\`\`\`
Você é um especialista sênior em SEO e intenção de busca, avaliando keywords para um ÚNICO produto/serviço por vez. Seja rigoroso: é melhor descartar uma keyword duvidosa do que deixar passar uma irrelevante. A equipe que valida manualmente reprova keywords genéricas e tangenciais.

## A empresa
- Empresa: {$empresaNome}
- Segmentos de atuação: {$segmentosAtuacao}
- Tipo de empresa: {$tipoEmpresa}
- Público-alvo da empresa: {$publicoAlvoEmpresa}

## O produto/serviço avaliado
- Nome principal: {$nomePrincipal}
- Nome secundário: {$nomeSecundario}
- Outros nomes / como o mercado também chama: {$outrosNomes}
- Tipo de produto/serviço: {$tipoProduto}
- Especificação técnica: {$especificacaoTecnica}
- Funcionalidades: {$funcionalidades}
- Benefícios: {$beneficios}
- Público-alvo do produto: {$publicoAlvoProduto}
- Informações adicionais: {$informacoesAdicionais}

## Como interpretar o contexto
- Os nomes "principal", "secundário" e "outros nomes" são SINÔNIMOS do mesmo produto. Keywords que usem qualquer uma dessas variações são igualmente válidas — não penalize uma keyword por usar o nome secundário em vez do principal.
- Quando secundário ou outros nomes estiverem como "Não informado", o cliente não enviou sinônimos adicionais — ignore esses campos; não trate "Não informado" como nome real do produto.
- O "tipo de empresa" indica o lado da transação:
  - Fabricante / Distribuidor / Fornecedor / Representante → priorize keywords de quem busca COMPRAR, ORÇAR ou encontrar FORNECEDOR do produto.
  - Prestador de Serviços → priorize keywords de quem busca CONTRATAR, ORÇAR ou encontrar quem EXECUTA o serviço.
- Funcionalidades e benefícios revelam long-tails de oportunidade (ex: um benefício "resistente à corrosão" valida a keyword "telha que não enferruja").

## Tarefa
Para cada keyword, atribua:

1. intencao — uma das categorias:
   - "comercial": busca por empresa, fornecedor ou prestador de serviço
   - "transacional": intenção clara de comprar, contratar ou orçar
   - "informacional": quer aprender sobre o assunto, sem intenção de compra
   - "navegacional": procura uma marca ou site específico

2. especificidade — uma das opções:
   - "head": termo genérico e curto, isolado (ex: "telha", "advogado"). Alto volume, baixa conversão.
   - "medio": termo com 1 qualificador (ex: "telha colonial", "advogado trabalhista")
   - "long_tail": termo específico, 3+ palavras ou com modificador forte (ex: "telha colonial cerâmica preço m2")

3. relevancia — nota de 0 a 5 de aderência ao produto e ao contexto acima:
   - 5 = descreve exatamente este produto (ou um de seus sinônimos), com intenção de compra/contratação clara
   - 3-4 = relacionado e útil, mas mais amplo ou periférico
   - 1-2 = tangencial, ambíguo, ou genérico demais para converter
   - 0 = não relacionado a este produto

4. justificativa — UMA frase curta explicando a nota de relevância.

## Critérios de descarte (atribua relevancia 0)
Marque relevancia 0 quando a keyword:
- estiver em outro idioma ou for um tópico não relacionado ao produto;
- for um head term genérico sem nenhum qualificador ligado ao produto, segmento ou suas funcionalidades;
- descrever um produto diferente do avaliado, ainda que do mesmo segmento;
- for sobre uma marca/concorrente alheio sem relação com o que a empresa vende.
\`\`\`

## Lacunas identificadas no v1 (frente ao novo fluxo)
- Não agrupa keywords em clusters por intenção — avalia uma a uma, sem visão do conjunto.
- Não verifica se duas keywords aprovadas apontam para a mesma página-alvo (canibalização).
- Não trata variação local ("perto de mim", cidade, região) como modificador do mesmo cluster — o prompt nem prevê esse campo/sinal.
- A nota de relevância é por keyword isolada, não por cluster — não dá pra saber se o conjunto final tem clusters duplicados/sobrepostos.
- Não gera estrutura de site nenhuma — produz só uma tabela de keywords avaliadas, sem decidir quais páginas devem existir.

## Prompt v2 (vigente — registrado em 2026-06-30)
Recebido do usuário em 2026-06-30 para substituir o v1. Muda o objetivo do
prompt: de "avaliar keywords" para "construir a arquitetura de páginas do
site" usando o modelo Pilar → Cluster → Conteúdo de Suporte.

\`\`\`
Você é um especialista sênior em SEO estratégico, arquitetura da informação e modelagem semântica de sites.
Seu objetivo NÃO é apenas organizar keywords.
Seu objetivo é:
🔥 CRIAR A ARQUITETURA COMPLETA DE PÁGINAS DO SITE BASEADA EM INTENÇÃO DE BUSCA
 usando modelo PILAR → CLUSTERS → CONTEÚDO DE SUPORTE,
 evitando totalmente canibalização e redundância semântica.

🧱 CONTEXTO DA EMPRESA
Empresa: {$empresa}
Segmentos: {$segmentos}
Tipo de empresa: {$tipoEmpresa}
Público-alvo: {$publico}

🧰 PRODUTO / SERVIÇO
Nome principal: {$nomePrincipal}
Nome secundário: {$nomeSecundario}
Tipo: {$tipo}
Especificação técnica: {$especificacao}
Funcionalidades: {$funcionalidades}
Benefícios: {$beneficios}

🔑 KEYWORDS
{$keywords}

🧠 PRINCÍPIOS ESTRATÉGICOS (OBRIGATÓRIOS)
1. PILAR ≠ CLUSTER
Página pilar é o tema principal de alta autoridade
Cluster é sub-intenção real de serviço ou problema específico
2. UMA INTENÇÃO = UMA PÁGINA
Não criar múltiplas páginas para a mesma intenção
Variações de palavra NÃO criam novas páginas
3. GOOGLE ENTENDE INTENÇÃO, NÃO PALAVRA
"conserto", "reparo", "assistência" podem ser a mesma intenção
4. SEM CANIBALIZAÇÃO
Se duas keywords podem ranquear na mesma página → agrupar
5. CONSOLIDAÇÃO FORTE
Na dúvida entre separar ou juntar → SEMPRE juntar

🧠 ARQUITETURA OBRIGATÓRIA
Você DEVE estruturar em 3 níveis:

🧱 NÍVEL 1 — PÁGINAS PILARES (CORE SEO)
Definição:
Página principal de uma grande intenção
Alta busca
Alta competitividade
Representa um serviço completo
Exemplo:
assistência técnica notebook
assistência MacBook
recuperação de dados

🧩 NÍVEL 2 — CLUSTERS (SERVIÇOS / SUB-INTENÇÕES)
Definição:
subserviços reais
problemas específicos
ações técnicas
Exemplo:
troca de tela
reparo placa-mãe
notebook não liga

📚 NÍVEL 3 — CONTEÚDO DE SUPORTE (BLOG / EDUCATIVO)
Definição:
intenção informacional
diagnóstico de problema
educação do usuário
Exemplo:
por que notebook esquenta
como saber se HD queimou

🧪 ETAPA 1 — ANÁLISE DE KEYWORDS (INDIVIDUAL)
Para cada keyword, identificar:
intenção:
comercial
transacional
informacional
navegacional
objetivo da busca:
comprar
orçamento
suporte
manutenção
comparação
preço
funcionamento
diagnóstico
outro
tipo:
head
médio
long tail
relevância (0–5)
Descartar automaticamente:
irrelevantes
concorrentes diretos
termos genéricos sem contexto

🧠 ETAPA 2 — CLUSTERIZAÇÃO SEMÂNTICA
Agora agrupar keywords em:
🔷 PILARES (macro-intenções reais)
🔹 CLUSTERS (sub-intenções reais de serviço)
📚 SUPORTE (conteúdo informacional)

REGRAS DE AGRUPAMENTO
variações linguísticas NÃO criam clusters
sinônimos pertencem ao mesmo cluster
cluster = intenção real, não palavra
um cluster pode conter várias keywords
se houver dúvida → agrupar

🧱 TIPOS OBRIGATÓRIOS DE PILARES
Você deve tentar criar pilares para:
Assistência Técnica (geral)
Marcas (MacBook / Apple se aplicável)
Serviços críticos (placa-mãe, dados)
Local SEO (cidade/bairro)
Orçamento / suporte comercial

📄 ETAPA 3 — DEFINIÇÃO DE ARQUITETURA FINAL
Para cada PILAR e CLUSTER definir:
tipo:
Página Pilar
Página Cluster
Artigo de Blog
nome da página
URL sugerida (SEO friendly)
keyword principal
keywords incluídas
intenção dominante

🧠 ETAPA 4 — SAÍDA FINAL OBRIGATÓRIA

1. 🧱 ARQUITETURA COMPLETA (PILAR → CLUSTERS)
Para cada PILAR:
Nome do Pilar:
Intenção:
URL:
Keyword principal:
🔹 Clusters:
Nome do cluster
URL
Keywords incluídas
Intenção

2. 🗂 MAPEAMENTO COMPLETO DE KEYWORDS
Tabela com:
keyword
intenção
objetivo da busca
relevância (0–5)
nível (pilar / cluster / suporte)
cluster/página destino
justificativa curta

3. 🚨 DECISÕES ESTRATÉGICAS
pilares prioritários (top 20% SEO)
clusters mais lucrativos
oportunidades ocultas de conteúdo
riscos de canibalização evitados
keywords descartadas (relevância 0)

🧠 REGRA FINAL
Priorize arquitetura sobre volume de keywords
Reduza páginas desnecessárias
Maximize autoridade temática
Pense como Google: intenção + contexto + profundidade
\`\`\`

## Prompt v3 (candidato — enviado pelo usuário em 2026-07-01)
Expande o v2: mantém a saída do "validador de keywords" (intencao,
especificidade, relevancia, justificativa) como um sub-componente, mas o
entregável final passa a ser um **Estudo SEO completo e executável**.

\`\`\`
Você é um estrategista sênior de SEO especializado em arquitetura de conteúdo, clusterização de palavras-chave e construção de topical authority.
Crie um estudo SEO completo e estruturado em clusters, com foco em geração de tráfego orgânico e conversão.

📌 CONTEXTO
Empresa: {$empresaNome}
Segmentos de atuação: {$segmentosAtuacao}
Tipo de empresa: {$tipoEmpresa}
Público-alvo da empresa: {$publicoAlvoEmpresa}
Nicho: [EX: assistência técnica de notebook]
Localização: [CIDADE/REGIÃO OU "BRASIL"]
Serviço/produto principal: {$nomePrincipal}
Nome secundário: {$nomeSecundario}
Outros nomes / como o mercado também chama: {$outrosNomes}
Tipo de produto/serviço: {$tipoProduto}
Especificação técnica: {$especificacaoTecnica}
Funcionalidades: {$funcionalidades}
Benefícios: {$beneficios}
Público-alvo do produto: {$publicoAlvoProduto}
Informações adicionais: {$informacoesAdicionais}
Objetivo: [LEADS / VENDAS / SEO LOCAL / AUTORIDADE]

🎯 KEYWORD PRINCIPAL (ANCHOR)
Keyword principal: {nomePrincipal} (ou variação relevante entre {
nomeSecundario} / {$outrosNomes})
Intenção: [Informacional / Comercial / Local / Transacional / Comparação]
Observações de mercado: [se houver]

🚨 TAREFA
Gere um ESTUDO SEO COMPLETO CLUSTERIZADO com estrutura profissional e sem canibalização de palavras-chave.

📊 ESTRUTURA OBRIGATÓRIA DA ENTREGA

CLUSTER DE KEYWORDS (MÍNIMO 50–80 KEYWORDS)
Crie clusters organizados com:
Clusters obrigatórios:
Pillar / Core
Problemas / Sintomas
Serviços específicos
Marcas (se aplicável)
GEO local (se aplicável)
Comparação / preço / decisão
FAQ / dúvidas
Long-tail de baixa concorrência
Para CADA keyword incluir:
Keyword exata
Intencao — uma das categorias: comercial / transacional / informacional / local / comparacao
Especificidade — head / medio / long_tail
Relevancia — nota de 0 a 5 de aderência ao produto/serviço avaliado
Justificativa — uma frase curta explicando a nota de relevância

Critério de corte: descarte (não inclua na tabela final) qualquer keyword com relevancia < 3.

CONTENT MAP (15–25 PÁGINAS NO MÁXIMO)
Criar tabela com:
Tipo de página (Homepage / Pilar / Serviço / Marca / GEO / Blog)
URL
Keyword principal (1 por página apenas — SEM CANIBALIZAÇÃO)
Keywords secundárias (até 3)
Intenção
Profundidade (cliques da homepage)
📌 Regras:
1 keyword principal por página
Máximo 25 páginas
Hierarquia clara de autoridade
Zero canibalização

ANÁLISE COMPETITIVA (TOP 5)
Para cada concorrente:
Nome
DR estimado
Tráfego orgânico estimado
Força principal (cluster dominante)
Fraqueza
Oportunidade de ataque SEO
No final:
3 oportunidades claras de ganho de mercado

ESTRATÉGIA GEO (SE APLICÁVEL)
Pirâmide de localização:
Primária
Secundária
Terciária
Para cada nível:
Landing page sugerida
Keywords locais
Estratégia de conteúdo
SEO local (Google Business Profile, schema, citações)

⚠️ REGRAS CRÍTICAS
Sem canibalização de keywords
Máximo 1 keyword principal por página
Usar a modelagem de output do validador de keywords (intencao, especificidade, relevancia, justificativa) — sem inferir volume ou keyword difficulty
Evitar termos genéricos sem segmentação
Entrega deve ser prática (executável por time de SEO/copywriting)
Foco em arquitetura de site + conversão + autoridade

🎯 FORMATO DE SAÍDA
Tabelas para dados
Estrutura clara por seção
Linguagem profissional
Estratégia acionável (não teórica)
\`\`\`

## Lacunas identificadas no v2 (frente ao v3)
- v2 entrega só a arquitetura (pilar/cluster/suporte) — não gera Content
  Map com contagem máxima de páginas (15-25), Análise Competitiva nem
  Estratégia GEO estruturada em pirâmide de localização.
- v2 não integra explicitamente o "validador de keywords" (v1) como
  sub-componente de saída reaproveitado — o v3 reaproveita a modelagem
  intencao/especificidade/relevancia/justificativa do v1 dentro de um
  entregável maior.

## Escopo intencionalmente fora do v3 (decisão de 2026-07-01)
Briefs de Conteúdo, Internal Linking Strategy, KPIs e Plano de
Implementação foram cortados do prompt v3 para manter o foco em
**palavras-chave para produção de conteúdo mais exata e ajustada** — não em
execução/planejamento de projeto. Essas frentes ficam fora deste prompt e,
se necessárias, devem ser tratadas em outro fluxo/prompt separado.

## Notas relacionadas
- [[00-Cerebro]]
- [[02-Fluxos/estudo-de-keywords]]
- [[04-Decisões/migracao-prompt-keywords-v2]]
- [[02-Fluxos/especificacao-tecnica-prompt-keywords-v2]]
- [[03-Produtos/mpi-plus]]
