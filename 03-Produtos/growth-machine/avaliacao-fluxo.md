---
tipo: fluxo
status: revisao-completa-prd-v1-9-14
criado: 2026-07-01
ultima-revisao: 2026-07-01
tags: [growth-machine, avaliacao, revisao-critica, prd]
---

# Avaliação do Fluxo — Growth Machine (PRD v1.9.14)

> Documento avaliativo construído em paralelo, à medida que destrinchamos o
> PRD do Growth Machine fase a fase. Cada seção registra pontos fortes,
> pontos fracos/riscos identificados na revisão crítica e observações que
> podem virar item de [[05-Backlog]]. Fonte: [[03-Produtos/growth-machine]]
> (nota-mãe com o PRD completo).

## Objetivo deste documento
Servir de fonte avaliativa direta — não é o PRD em si (isso já está em
[[03-Produtos/growth-machine]]), é a nossa leitura crítica sobre ele,
fase por fase, para embasar decisões de ajuste antes/durante o
desenvolvimento. Construído do ponto de vista de **PO**, para consolidar
todo o diagnóstico num único lugar antes de decidir prioridade de ajuste.

---

## Síntese Executiva (visão de PO)

Revisão completa do PRD v1.9.14 concluída: 4 fases, Módulo Sentinela,
Agentes de IA, 11 Telas, Ferramentas Externas e Decisões
Técnicas/NFRs — 8 blocos avaliados. Esta síntese consolida o que atravessa
mais de um bloco, para orientar priorização.

### Diagnóstico geral
O PRD é **estruturalmente maduro**: fórmulas auditáveis, separação rígida
de papéis entre os 3 sistemas (GM/MPI Plus/Salesforce), dupla aprovação
humana em pontos críticos, e um contrato técnico padronizado (schema JSON,
versionamento) para os agentes de IA. Isso não é comum em v1 de PRD — é
sinal de que o desenho já passou por mais de uma rodada de maturação
(o próprio histórico de versões, de v1.0 a v1.9.17, confirma isso).

Mas o documento tem um padrão de lacuna que se repete e que, na minha
leitura, é o que mais merece atenção como PO — não são bugs de desenho,
são **decisões ainda não tomadas** disfarçadas de detalhe de implementação.

### Os 4 padrões que atravessam o PRD inteiro

1. **"Sem prazo automático" sem alerta de envelhecimento equivalente.**
   Aparece no briefing (Fase 1), na validação pós-execução (Fase 4) e,
   por extensão, no problema de fundo que o próprio produto quer resolver
   (briefing/cliente "esquecido" sem ninguém notar). É o risco mais
   recorrente do documento — mais do que qualquer risco técnico pontual.
2. **Números de negócio sem origem/calibração documentada.** 70% de
   similaridade, 50% de trava de pacote (Fase 1), 40/40/20 e taxa de
   conversão 5% (Fase 2), cota de 400 req/dia do PageSpeed (Ferramentas) —
   todos parecem definidos por julgamento de especialista, não por teste. Não
   é necessariamente errado, mas não está registrado *como* chegaram nesses
   números, o que dificulta revisar/calibrar depois.
3. **Concentração de responsabilidade em pontos de controle críticos.** CS
   sozinho valida briefing (Fase 1); Analista acumula aprovação inicial e
   validação final, extinguindo o papel de Revisor (Fase 4) — reduz
   segregação de funções em nome de agilidade, sem uma segunda camada de
   verificação independente.
4. **Fronteiras entre componentes sem critério de desempate explícito.**
   Dim 5 vs. Dim 9 (front-end vs. servidor), IA vs. Analista na validação
   (Fase 4) — quando dois lados divergem, o PRD não diz quem prevalece.
5. **17 de 30 questões em aberto (mais de 50%) sem dono nem prazo,**
   concentradas justamente na integração mais crítica do sistema (MPI Plus
   como SPOF reconhecido pelo próprio documento). Isso é o maior risco de
   cronograma do projeto — não um risco técnico, um risco de planejamento.

### O risco que mais pesa (na minha leitura como avaliação, não como PRD)
> *"A casa é entregue vazia; os móveis são os prompts."*

Toda a arquitetura ao redor dos agentes de IA está correta — contrato,
schema, versionamento, gates humanos. Mas a validade real do produto inteiro
depende de um trabalho (o conteúdo fino dos 9 prompts) que está fora do
escopo deste PRD, sem cronograma, dono ou processo de validação (golden-set)
atribuído a ele. Esse é o item que, se eu fosse priorizar como PO, eu
trataria como bloqueador de início de desenvolvimento — não como detalhe a
resolver depois.

### Recomendação de sequenciamento (se fosse decidir agora)
1. Fechar as 7 questões de integração (Q18–Q21 Salesforce; Q27–Q30 MPI
   Plus) — são pré-requisito técnico para qualquer coisa rodar de ponta a
   ponta.
2. Definir dono + prazo para as 17 questões em aberto restantes — transformar
   "a definir" em backlog rastreável.
3. Iniciar o desenho fino dos prompts em paralelo à Parte III técnica —
   não pode ser a última etapa, porque é o maior risco de qualidade do
   produto.
4. Resolver os 4 padrões recorrentes (acima) como ajustes de governança do
   PRD antes de congelar escopo para build — são baratos de corrigir agora
   e caros de corrigir depois de codificados.

Todos os pontos completos, fase a fase e bloco a bloco, estão detalhados
abaixo.

---

## Fase 1 — Entrada e Briefing

### Pontos fortes
1. **Validação mediada pelo CS, não pelo cliente sozinho.** Reduz o risco de
   aprovação displicente ("clique aceito sem ler") que aconteceria num
   painel de autoconfirmação direto ao cliente.
2. **Distinção clara entre os 3 cenários de entrada (A/B/C).** Reconhece que
   cliente legado ≠ cliente novo, evitando tratar todo mundo com o mesmo
   processo quando a necessidade de dado é diferente.
3. **Briefing auto-incrementado (RN-80).** Resolve o problema estrutural de
   briefings desatualizados (<20% da carteira) sem depender de mais um
   processo manual — o próprio uso do sistema mantém o dado vivo. É solução
   de causa raiz, não paliativo.
4. **Trava de bonificação em 50% do pacote + anti-canibalização.** Impede
   que a "sugestão inteligente de palavras" vire expansão de escopo
   descontrolada ou keyword duplicada.

### Pontos fracos / riscos
1. **Ausência de prazo automático (RN-01) sem alerta de envelhecimento.**
   O fluxo permite briefing pendente indefinidamente sem notificação
   proativa — existe alerta de 28 dias para ações não executadas (RN-04),
   mas nada equivalente para o próprio briefing parado. É o mesmo tipo de
   furo que gera "cliente ligando furioso", que o produto diz querer
   eliminar.
2. **"3ª rejeição" não diferencia gravidade do ajuste.** O fluxo conta
   rejeições (máx. 2 iterações, 3ª escala pro gerente) sem diferenciar se é
   um ajuste pequeno ou uma recusa total do estudo.
3. **Dependência total do FireCrawl no cenário B (legado), sem fallback.**
   Se o crawler falhar (bloqueio de robots.txt, site malformado), não há
   mecanismo alternativo descrito para complementar o briefing — ponto único
   de falha silencioso.
4. **Threshold de 70% de similaridade vetorial sem calibração documentada.**
   Não há explicação do porquê desse número, nem menção a teste/validação —
   parece definido sem dado por trás, assim como a trava de 50% do pacote.
5. **Sem SLA para o próprio CS.** A fase depende do CS "validar com o
   cliente", mas não há prazo interno definido para quando o CS deve rodar
   essa validação após o sistema gerar o briefing. Duas fontes de atraso
   somadas sem controle: cliente que não responde + CS que não prioriza.

### Observações candidatas a backlog
- Definir alerta de envelhecimento de briefing pendente (paralelo ao RN-04).
- Definir SLA interno de resposta do CS após geração do briefing.
- Documentar fallback para falha de FireCrawl no cenário B.
- Registrar a origem/calibração dos thresholds de 70% (similaridade) e 50% (pacote).

---

## Fase 2 — Motor de Percepção

### Pontos fortes
1. **Um único gatilho de calendário, para toda a carteira.** Simples,
   previsível, sem ambiguidade sobre quando o ciclo roda.
2. **Fórmula matemática explícita e determinística.** Índice calculado por
   fórmula, não por julgamento humano — dá auditabilidade e repetibilidade.
3. **Curva de maturidade e teto de crescimento contra "cliente novo mal
   avaliado".** Reconhece que um site de 2 meses não pode ser cobrado pela
   mesma régua de um site de 3 anos — evita punir cliente novo injustamente.
4. **Regra de fronteira sem arredondamento.** Elimina ambiguidade de "quase
   Top 10 conta como Top 10" — decisão de engenharia limpa.
5. **Remoção do Bright Data como integração direta (v1.9.16).** Boa decisão
   de simplificação: reconhecer que adicionar uma chamada redundante não
   elimina o SPOF real é maturidade arquitetural.

### Pontos fracos / riscos
1. **Hard Stop sem fallback é um SPOF assumido, não mitigado.** Se o MPI
   Plus atrasar a geração do relatório (~dia 1º/2 é aproximado, não
   garantido), toda a carteira trava ao mesmo tempo. Não há plano B além de
   "aguardar o relatório".
2. **Pesos 40/40/20 e taxa de conversão default de 5% carecem de
   origem/calibração documentada**, repetindo o padrão já visto na Fase 1
   (thresholds de 70%/50%) — números de negócio importantes sem rastro de
   como foram definidos.
3. **Curva de maturidade trata todo cliente do mesmo segmento igual.** Um
   e-commerce e um prestador de serviço local presumivelmente amadurecem em
   ritmos diferentes, mas a curva parece única e genérica — o próprio PRD
   reconhece isso como questão em aberto (Q23: régua de posicionamento por
   período ainda não calibrada com Growth), mas ainda não resolvida.
4. **`leads_real` multicanal (RN-107) depende inteiramente da qualidade do
   dado do relatório MPI Plus.** Se o relatório não capturar corretamente um
   canal (ex: WhatsApp mal instrumentado), o índice de leads fica
   sistematicamente errado sem que o GM tenha visibilidade disso — confia
   cegamente no relatório como fonte única.
5. **Reclassificação de cadência (mensal↔trimestral) pode oscilar nas
   bordas.** Um cliente que oscila entre 0,79 e 0,80 muda de cadência de
   análise a cada mês — não há menção de histerese/período de estabilização
   antes de mudar a cadência.

### Observações candidatas a backlog
- Definir plano de contingência para atraso/ausência do relatório mensal do
  MPI Plus (hoje é Hard Stop puro).
- Documentar a origem/calibração dos pesos 40/40/20 e da taxa de conversão
  default de 5%.
- Acompanhar a resolução da Q23 (régua de maturidade por segmento) — hoje é
  genérica para todo cliente.
- Avaliar mecanismo de histerese para evitar oscilação de cadência
  mensal/trimestral nas bordas do threshold.
- Definir validação de qualidade do dado de leads multicanal antes de
  confiar cegamente no relatório.

## Fase 3 — Auditoria em 10 Dimensões

### Pontos fortes
1. **Travamento condicional só na Dim 1 (RN-88) é uma decisão de design
   muito boa.** Evita o erro clássico de pipeline sequencial "trava tudo se
   qualquer coisa falhar" — só a causa raiz genuína (estudo errado) trava; o
   resto roda em paralelo, mais rápido e mais realista, já que as dimensões
   2–10 são majoritariamente independentes entre si.
2. **Separação rígida entre determinístico (Dim 4,5,6,7,9) e IA (Dim
   1,2,3,8,10).** Maturidade de arquitetura: não usar LLM para o que uma
   ferramenta determinística já resolve com 100% de precisão (W3C,
   PageSpeed, Schema validator) evita alucinação onde não precisa e reduz
   custo/latência.
3. **Score de Saúde Técnica com fórmula auditável e pesos versionáveis.**
   Assim como o Índice de Performance na Fase 2, dá rastreabilidade e
   permite recalibração sem reescrever lógica.
4. **Anti-duplicidade entre dimensões** (ex: Dim 8 não reage a algo já
   coberto pela Dim 7 ou Dim 5). Evita que o cliente receba a mesma ação
   recomendada por caminhos diferentes — problema comum em sistemas
   multiagente sem coordenação.
5. **Regra de direção de linkagem MPI (Dim 3) é tecnicamente correta e bem
   formalizada** — silo hierárquico clássico, bem implementado como regra
   auditável.

### Pontos fracos / riscos
1. **"Rodar em paralelo" não define como conflitos de recomendação entre
   dimensões são resolvidos antes do Parecer Consolidado.** Se a Dim 2
   recomenda "refazer conteúdo" e a Dim 3 recomenda "reestruturar
   arquitetura" na mesma página ao mesmo tempo, quem prioriza a ordem de
   execução na prática, além do Parecer (que é um agente de IA, não uma
   regra determinística)?
2. **Dependência de DataForSEO na Dim 2 é cara e recorrente** — rodar por
   página MPI elegível, todo ciclo, para ~2.500 clientes pode ter
   custo/rate-limit relevante. Não há menção de cache de resultado de SERP
   entre ciclos (reaproveitar o padrão SERP se ele não mudou muito em 30
   dias).
3. **Régua da Dim 2 (score 60–79% → "Complementar") depende de julgamento de
   IA sobre "cobertura de intenção/tópicos/entidades"**, inerentemente mais
   subjetivo que as dimensões determinísticas. O PRD não menciona auditoria
   de qualidade/amostragem humana periódica sobre os vereditos desse agente
   — é o mais arriscado de todos por operar num critério qualitativo.
4. **M3 (Dim 9) e Dim 5 têm fronteira que depende de julgamento — "problema
   predominante de servidor" vs "front-end".** Pode gerar disputa/ambiguidade
   de responsabilidade entre times técnicos sem um dono claro do critério de
   desempate.
5. **Nenhuma dimensão trata volume/priorização quando há muitas páginas MPI
   elegíveis ao mesmo tempo.** Para clientes com centenas de páginas, rodar
   9 dimensões (2–10) por página, todo ciclo, é uma carga de processamento
   (e possivelmente de custo de API) que o PRD não dimensiona — sem SLA de
   "quanto tempo leva para processar 1 cliente" nem estratégia de fila.

### Observações candidatas a backlog
- Definir regra de desempate/priorização quando duas ou mais dimensões
  recomendam ações conflitantes na mesma página, antes do Parecer
  Consolidado.
- Avaliar estratégia de cache/reaproveitamento de SERP (Dim 2) entre ciclos
  para reduzir custo/rate-limit de DataForSEO.
- Definir processo de auditoria de qualidade periódica sobre os vereditos
  qualitativos do Agente de Conteúdo (Dim 2), a dimensão mais subjetiva.
- Definir critério de desempate objetivo entre Dim 5 e Dim 9 (front-end vs.
  servidor) para evitar disputa de responsabilidade entre times.
- Dimensionar SLA de processamento por cliente/ciclo e estratégia de fila
  quando o volume de páginas MPI elegíveis for grande.

## Fase 4 — Workflow de Aprovação, Execução e Validação

### Pontos fortes
1. **Double-check com validação automática por IA (RN-81) é a melhor
   mitigação de risco do fluxo inteiro.** Em vez de confiar cegamente que "o
   Front-end marcou como concluído", o sistema relê o site e confere de
   fato — ataca diretamente o risco de tarefa marcada como feita sem ter
   sido feita.
2. **Gatilho da maturação atrelado à validação do analista, não à execução
   técnica.** Evita que o relógio de 60 dias comece a contar sobre uma ação
   que na prática não foi bem executada ou ainda está sendo ajustada.
3. **Ação desconsiderada exige motivo e escala para Supervisor/Líder
   (RN-45).** Fecha um vetor clássico de fluxo que "simplesmente evapora"
   sem ninguém saber por quê.
4. **Execução parcial tratada explicitamente (RN-46).** "2 de 6" não se
   perde — reentra no ciclo seguinte. Bom controle de continuidade.
5. **Separação de sistemas mantida rigidamente:** GM decide o quê,
   Salesforce gerencia quem/quando/status, execução real é manual —
   consistente com o resto do PRD e evita que o GM vire gestor de tarefas
   paralelo ao Salesforce (RN-74).

### Pontos fracos / riscos
1. **RN-49 concentra aprovação inicial + validação técnica final na mesma
   pessoa (o Analista), após extinguir a persona "Revisor".** Remove
   segregação de funções que existia antes — o mesmo analista que aprovou a
   ação é quem valida se ela foi bem executada, sem um segundo par de olhos
   independente (viés de confirmação).
2. **Sem SLA definido para o analista validar após a conclusão no
   Salesforce.** Existe RN-28 (28 dias) para ação gerada e não executada,
   mas não há regra equivalente para "ação concluída no Salesforce,
   esperando o analista clicar em Validar" — pode atrasar indefinidamente o
   início da maturação de 60 dias sem alerta.
3. **Sem limite de reprovações antes de escalar.** Diferente do briefing
   (máx. 2 iterações → escala gerência), quando IA+analista reprovam a ação
   volta pra fila com notas, sem teto documentado — risco de loop de
   reprovação sem escalonamento automático.
4. **Sem regra de desempate quando IA e Analista divergem na validação.** O
   PRD trata "IA + Analista reprovam" como bloco único, mas não descreve o
   caso onde a IA valida e o analista reprova (ou vice-versa) — quem
   prevalece não está definido.
5. **Dependência forte do Salesforce como fonte única de status de
   execução.** Se a sincronização falhar silenciosamente (bug de webhook,
   atraso de API), o GM pode nunca saber que uma ação foi concluída —
   travando a fila de "[!] Validar" sem visibilidade do problema técnico.

### Observações candidatas a backlog
- Avaliar reintrodução de segregação de papéis entre quem aprova a ação
  inicialmente e quem valida a execução final (hoje concentrado no mesmo
  Analista, RN-49).
- Definir SLA/alerta para o tempo entre "Salesforce sincroniza conclusão" e
  "Analista aciona Validar" — hoje sem prazo, análogo ao gap já visto no
  briefing (Fase 1).
- Definir limite de reprovações de uma mesma ação antes de escalar
  automaticamente para Supervisor/Líder.
- Documentar regra de desempate quando IA e Analista divergem no resultado
  da validação.
- Definir monitoramento/alerta de falha silenciosa de sincronização
  Salesforce↔GM, para não deixar ações "presas" sem visibilidade.

---

## Síntese consolidada — padrões que se repetem nas 4 fases

Ao longo da revisão das 4 fases, alguns padrões de risco aparecem de forma
recorrente, não isolada:

1. **"Sem prazo automático" aparece 3 vezes (Fase 1 — briefing; Fase 4 —
   validação do analista) sem mecanismo de alerta de envelhecimento
   equivalente ao RN-04/RN-28.** É o risco estrutural mais repetido do PRD.
2. **Thresholds/pesos de negócio sem origem documentada** (70%/50% na Fase
   1; 40/40/20 e taxa de conversão 5% na Fase 2) — sugere que a calibração
   foi definida por julgamento de especialista, não por teste/dado, o que é
   aceitável mas deveria ser registrado explicitamente como tal.
3. **Concentração de responsabilidade numa única pessoa em pontos de
   controle críticos** (CS na Fase 1; Analista acumulando aprovação +
   validação na Fase 4) — reduz segregação de funções em nome de agilidade.
4. **Fronteiras de responsabilidade entre componentes automatizados nem
   sempre têm critério de desempate explícito** (Dim 5 vs Dim 9 na Fase 3;
   IA vs Analista na Fase 4).

Esses 4 padrões, mais que os itens pontuais, são o principal insumo para
priorizar o que vira item de [[05-Backlog]] a partir desta avaliação.

---

## Módulo Sentinela

### Pontos fortes
1. **Cobrir 100% dos sites, inclusive os bloqueados/em maturação, é a
   decisão mais importante do módulo.** Resolve um furo real: um cliente
   "em maturação" (60 dias sem reanálise) poderia ter o site fora do ar por
   semanas sem que ninguém percebesse, já que o ciclo normal está pausado
   para ele. O Sentinela fecha exatamente essa lacuna.
2. **Separação de custo por design.** Reconhecer explicitamente que
   vigilância diária não pode usar APIs caras (DataForSEO, PageSpeed) é uma
   decisão de arquitetura consciente sobre escala.
3. **Sobreposição inteligente ao bloqueio de maturação (RN-68/RN-94).** A
   regra "não reprocessa com ações pendentes" é correta na maior parte do
   tempo, mas ter exceção clara para incidentes de infraestrutura crítica
   (site fora, SSL expirado) evita que a proteção contra reprocessamento
   vire proteção contra alertar sobre um problema real.
4. **Alerta escalonado de SSL (30/15/7 dias) em vez de aviso único.** Dá
   tempo real de reação antes do certificado expirar.
5. **Retry com 3 tentativas em horários diferentes antes de declarar "fora
   do ar".** Evita falso positivo por instabilidade momentânea de rede.

### Pontos fracos / riscos
1. **Cobertura de "home e principais MPIs" para uptime, mas sem definição
   precisa de quantas páginas por site são checadas.** Para 2.500 sites,
   rodar em toda página seria caro; rodar só a home pode não detectar uma
   página MPI específica fora do ar (relacionado à Q25 do PRD, ainda aberta).
2. **Escopo exato do Sentinela por projeto ainda é questão em aberto (Q25),**
   incluindo se há ping ativo do endpoint de formulário — o módulo já está
   especificado como se estivesse pronto, mas a própria definição de escopo
   está incompleta.
3. **Infraestrutura do cron (Laravel Horizon interno vs. serviço externo de
   uptime dedicado) também é questão em aberto (Q26).** Rodar monitoramento
   de disponibilidade na própria infraestrutura da aplicação tem risco
   lógico: se o problema for na infra/rede onde o próprio GM roda, o
   Sentinela pode falhar exatamente quando mais precisa funcionar (sem
   redundância geográfica óbvia mencionada).
4. **Canal único documentado (E-mail + WhatsApp API) sem escalonamento se o
   alerta não for visto.** Um "SSL expira em 7 dias" que ninguém abre não
   tem escalonamento automático até virar alerta extremo (só no dia em que
   já expirou/já caiu).
5. **Retenção de histórico de uptime/SSL de ≥90 dias (NFR-23) é curta para
   análise de tendência de longo prazo** — cliente de 2 anos de contrato não
   tem visibilidade histórica completa além de 3 meses.

### Observações candidatas a backlog
- Resolver a Q25 (escopo exato de páginas monitoradas por projeto, incluindo
  ping ativo de endpoint de formulário).
- Resolver a Q26 (infraestrutura do cron — Horizon interno vs. serviço
  externo dedicado — e redundância caso a própria infra do GM tenha
  problema).
- Definir escalonamento automático quando um alerta de SSL/uptime não é
  reconhecido/agido dentro de um prazo.
- Avaliar aumento do período de retenção de histórico de uptime/SSL além de
  90 dias para clientes de contrato longo.

---

## Agentes de IA

### Pontos fortes
1. **Contrato de prompt padronizado e schema JSON obrigatório para todo
   agente é a decisão de engenharia mais forte deste bloco.** Sem isso, cada
   agente viraria um "floco de neve" com prompt e saída próprios, impossível
   de auditar em escala. Padronizar `dimension`, `status`, `confidence`,
   `findings`, `recommended_actions` cria um contrato único que qualquer
   parte do sistema pode consumir de forma previsível.
2. **`requires_human_approval` e `do_not_act_reason` embutidos no schema, não
   como convenção externa.** Força todo agente a declarar explicitamente
   quando não vai agir e por quê — reduz o risco de "silêncio ambíguo"
   (agente não fez nada e ninguém sabe se foi decisão ou falha).
3. **Mecânica de entradas via context builder, proibindo o agente de buscar
   dados sozinho.** Elimina uma classe inteira de bugs/riscos de segurança —
   um agente não pode, por conta própria, consultar fonte fora do escopo ou
   vazar dados entre projetos.
4. **Log obrigatório com `ruleset_version_id` + `prompt_version_id` em toda
   execução.** Dá rastreabilidade real: qual versão de regra e de prompt
   gerou qualquer ação histórica — crítico para auditoria e debug de
   regressões quando um prompt for atualizado.
5. **Separação rígida detecção (GM) vs. geração (MPI Plus), com dois gates
   humanos (Gate 1 gerar, Gate 2 revisar).** Reduz a chance de conteúdo de
   baixa qualidade chegar ao cliente sem revisão — mesmo padrão de dupla
   aprovação já visto como ponto forte na Fase 4.

### Pontos fracos / riscos
1. **"A casa é entregue vazia; os móveis são os prompts" — frase textual do
   PRD, honesta e preocupante ao mesmo tempo.** O contrato/schema está
   pronto, mas o conteúdo fino de cada prompt (o que realmente faz o agente
   confiável) ainda não existe — risco de execução gigante não mitigado por
   nenhuma arquitetura, por melhor que seja.
2. **`confidence` é campo obrigatório no schema, mas sem regra documentada
   de uso.** Existe menção de "confiança abaixo do mínimo parametrizado"
   bloqueando execução, mas não está detalhado qual é esse mínimo, se é
   igual para todos os agentes, ou como calibrar a confiança declarada por
   um LLM (notoriamente mal calibrada — LLMs tendem a reportar confiança
   alta mesmo errando).
3. **Nenhum agente tem menção de teste de regressão antes de trocar de
   versão de prompt.** Existe versionamento e rollback na Tela 9, mas não há
   processo de validação/golden-set antes de promover um novo prompt para
   produção — o versionamento permite reverter depois do estrago, não
   previne.
4. **A Camada de Tradução de Diagnóstico atravessa todas as dimensões e não
   tem dono claro por dimensão.** Se ela traduzir errado o achado de uma
   dimensão determinística (ex: PageSpeed), o erro pode nunca ser percebido
   porque a fonte determinística estava certa — o erro está só na camada de
   IA em cima.
5. **Sem menção de limite de token/contexto por chamada**, considerando que
   alguns agentes recebem entradas grandes (ex: Auditor de Conteúdo SERP
   recebe conteúdo de múltiplos concorrentes + página do cliente +
   histórico) — sem estratégia de truncamento/priorização documentada.

### Observações candidatas a backlog
- Priorizar o desenho fino dos prompts reais como frente de trabalho própria
  e crítica — é o risco central do produto, segundo o próprio PRD.
- Definir o mínimo de `confidence` por agente/dimensão e o processo de
  calibração desse valor.
- Criar processo de validação com golden-set antes de promover nova versão
  de prompt para produção (hoje só existe rollback reativo).
- Definir dono/responsável por dimensão para auditar a Camada de Tradução de
  Diagnóstico, já que atravessa todas as dimensões e pode mascarar erro de
  tradução sobre uma fonte determinística correta.
- Definir estratégia de truncamento/priorização de conteúdo quando a entrada
  de um agente se aproximar do limite de contexto.

---

## As 11 Telas

### Pontos fortes
1. **Separação global vs. contextual (RN-98) é coerente com o resto da
   arquitetura.** Telas de projeto não poluem o menu principal — só aparecem
   quando um cliente é selecionado, reduzindo ruído de navegação para quem
   lida com 2.500 projetos.
2. **Tela 6 (Status de Execução) é somente leitura por design.** Reforça na
   UI a mesma regra de negócio da Fase 4: o GM não é gestor de tarefas, o
   Salesforce é. Evita que o Front-end tenha dois lugares para "marcar como
   feito".
3. **Sem campos de custo na Tela 8 (RN-73) é decisão de segurança/governança
   correta.** Impede que custo de API/token vaze para uma interface
   operacional onde não deveria estar visível.
4. **Tela 10 sem aprovação de cliente no GM (RN-104), reforçando "cliente
   nunca acessa o GM".** A UI segue rigorosamente a separação de papéis
   definida na arquitetura.
5. **As 5 jornadas críticas cobrem o ciclo de vida completo** (aprovação →
   execução → validação → alerta de infra) — bom conjunto mínimo para
   prototipagem, evitando telas soltas sem fluxo de uso definido.

### Pontos fracos / riscos
1. **Tela 2 (Painel Gerencial) não menciona granularidade de drill-down até
   o problema específico.** "Desempenho por analista e BU" é um resumo — não
   fica claro se o gerente chega diretamente à causa raiz de um cliente
   problemático sem passar pela Tela 1 do analista responsável.
2. **Nenhuma tela documentada para o CS especificamente**, apesar de ser
   peça central da Fase 1. A Tela 10 é "Analista + CS", mas não fica claro
   se o CS tem visão própria (ex: fila de briefings pendentes) ou opera
   dentro da mesma tela do analista.
3. **"Aprovar tudo" (Tela 4) como ação global é risco de governança** se não
   houver segunda confirmação ou amostragem mínima obrigatória antes de
   aprovar múltiplas ações de uma vez — risco de virar hábito sem revisão
   real, esvaziando o propósito da aprovação humana.
4. **Sem tela dedicada de auditoria/log para revisar decisões passadas dos
   agentes de IA** — o log obrigatório existe como dado, mas não aparece
   como tela explícita nas 11 listadas.
5. **Tela 11 (Sentinela) separada da Tela 1 (Carteira), mas o Sentinela
   alimenta badges na Tela 1** — pode gerar duplicação de UI/fonte de
   verdade se não houver clareza de que a Tela 1 é resumo e a Tela 11 é a
   fonte completa.

### Observações candidatas a backlog
- Definir se existe (ou deveria existir) visão/fila própria para o CS na
  Tela 10, separada da visão do Analista.
- Definir salvaguarda para o botão "Aprovar tudo" na Tela 4 (confirmação
  extra acima de N ações, ou amostragem obrigatória).
- Definir se existe tela/aba explícita de auditoria de decisões de agentes
  de IA, ou se fica implícito dentro do Prontuário/Tela 9.
- Detalhar granularidade de drill-down da Tela 2 até a causa raiz de um
  cliente específico.

---

## Ferramentas Externas Integradas

### Pontos fortes
1. **"Divisão de funções acordada" explícita é boa prática de arquitetura
   de integração.** Deixa claro, numa única lista, quem é dono de qual
   dado — evita a armadilha de duas ferramentas "quase" fazendo a mesma
   coisa sem hierarquia definida (o que quase aconteceu com Bright Data vs.
   relatório MPI Plus, e foi corrigido).
2. **Remoção consciente do Bright Data (v1.9.16) mostra maturidade de
   decisão técnica.** Reconhecer que uma integração redundante não elimina
   o SPOF real é economia de complexidade genuína, não só de custo.
3. **W3C Validator self-hosted em Docker, sem limite externo.** Elimina
   dependência de rate-limit/disponibilidade de terceiro para uma checagem
   que roda em volume alto.
4. **SendGrid com pull diário obrigatório e retenção local documentada
   (≥3 meses).** Evita depender só do plano atual do SendGrid (7 dias de
   log) — o GM se protege da limitação do provedor.
5. **Ferramentas condicionais bem marcadas (DataForSEO/KeywordTools na Dim
   1).** Evita gastar com API cara quando a auditoria nem indicou
   necessidade — controle de custo embutido na lógica de quando chamar.

### Pontos fracos / riscos
1. **PageSpeed API com cota de 400 req/dia é pequena perto da escala do
   produto.** Com ~2.500 clientes rodando páginas MPI elegíveis todo ciclo,
   400 req/dia parece insuficiente sem estratégia de fila/priorização
   explícita quantificada (quantos dias para cobrir a carteira inteira).
2. **Nenhuma ferramenta tem SLA de disponibilidade documentado do
   fornecedor, nem estratégia de circuit breaker/timeout padronizada entre
   elas** — cada dimensão trata falha de API de forma um pouco diferente.
3. **6 contas de Google Search Console para 2.500 clientes sem critério de
   distribuição explicado**, nem menção de limite de propriedades por conta
   que possa virar gargalo de escala.
4. **SemRush Business sem menção de rate-limit/cota**, diferente do cuidado
   dado ao PageSpeed (400/dia) — inconsistência no nível de detalhe de
   dimensionamento entre ferramentas.
5. **DataForSEO usado tanto para concorrentes (Dim 2, recorrente) quanto
   para expansão de estudo (Dim 1, condicional) sem teto de chamadas
   combinado** — pode gerar competição interna por cota entre dimensões do
   mesmo cliente.

### Observações candidatas a backlog
- Dimensionar a cota de 400 req/dia do PageSpeed contra o volume real de
  páginas MPI elegíveis da carteira.
- Definir estratégia padronizada de circuit breaker/timeout/retry por
  ferramenta externa.
- Documentar o critério de distribuição de clientes entre as 6 contas de
  Search Console e o limite de propriedades por conta.
- Definir cota/rate-limit para SemRush Business, no mesmo nível de detalhe
  já dado ao PageSpeed.
- Definir teto de orçamento/chamadas combinado do DataForSEO entre Dim 1 e
  Dim 2, evitando competição interna por cota.

---

## Decisões Técnicas e Requisitos Não-Funcionais (NFRs)

### Pontos fortes
1. **Modelo de dados "instância única, base compartilhada" é coerente com a
   necessidade de visão consolidada.** Como o Painel Gerencial (Tela 2)
   precisa agregar as ~2.500 posições das 3 empresas, um multi-tenant
   isolado tornaria essa visão consolidada muito mais cara de construir.
2. **Padrão assíncrono explícito para MPI Plus (`IntegrationJob` + webhook)
   em vez de chamada síncrona.** Correto para integração externa que pode
   demorar — evita acoplamento temporal forte entre os dois sistemas.
3. **RN-73 (sem custo na interface) reaparece como decisão de segurança
   consistente**, junto com "credenciais de API nunca expostas no
   frontend" — a preocupação de não vazar dado sensível permeia mais de uma
   camada do sistema.
4. **Migração de BullMQ (Node) para Laravel Horizon (Redis) é correção de
   inconsistência de stack bem registrada.** Evita dois runtimes (PHP+Node)
   para resolver o mesmo problema de fila.
5. **NFR-12 distingue claramente falha "normal" de falha "crítica"
   (ausência total de posicionamento).** Coerente com o Hard Stop da Fase 2
   — o sistema degrada graciosamente na maioria dos casos, reservando a
   parada total para o único cenário que realmente inviabiliza a análise.

### Pontos fracos / riscos
1. **Modelo de dados de instância única sem isolamento por tenant é também
   um risco de segurança concentrado.** Se houver falha de escopo
   (row-level access mal implementado), o vazamento potencial é entre as 3
   empresas inteiras — o "blast radius" de um bug de autorização é o
   sistema inteiro, não um tenant isolado.
2. **7 questões em aberto (Q18–Q21 Salesforce; Q27–Q30 MPI Plus) são todas
   sobre a camada de integração mais crítica do sistema — exatamente onde o
   PRD já reconhece o MPI Plus como SPOF.** O ponto mais frágil da
   arquitetura é também o ponto com mais perguntas não resolvidas — maior
   risco de cronograma do projeto todo.
3. **NFR-11 (≥99,5% disponibilidade em horário comercial) sem NFR
   equivalente fora do horário comercial**, mesmo o Sentinela rodando 24/7 e
   ações críticas (RN-94) precisando de reação a qualquer hora.
4. **Retenção de dados "definida" para LGPD sem prazo específico
   documentado nesta seção** (diferente do Sentinela, com 90 dias explícitos
   em NFR-23) — vago quanto tempo dados de diagnóstico/briefing/histórico
   são retidos.
5. **SSO integrado ao MPI Plus sem senha própria no GM cria dependência de
   disponibilidade cruzada:** se o MPI Plus cair, ninguém consegue logar no
   GM também, mesmo que o GM esteja saudável — SPOF adicional não mencionado
   explicitamente como tal.

### Observações candidatas a backlog
- Priorizar a resolução das 7 questões em aberto de integração (Q18–Q21,
  Q27–Q30) como frente crítica, no ponto de maior fragilidade arquitetural.
- Avaliar controles adicionais de auditoria/teste para o row-level access
  entre empresas, dado o alto blast radius de uma falha de escopo.
- Definir NFR de disponibilidade fora do horário comercial, coerente com o
  Sentinela 24/7 e RN-94.
- Documentar prazo específico de retenção de dados de
  diagnóstico/briefing/histórico para LGPD.
- Registrar e mitigar a dependência de disponibilidade cruzada do SSO — GM
  fica inacessível se o MPI Plus cair, mesmo estando saudável.

---

## Questões em Aberto e Riscos Consolidados (fechamento do PRD)

### Pontos fortes
1. **O PRD é honesto sobre seus próprios riscos.** Tabela de riscos com
   probabilidade e mitigação, e 30 questões em aberto numeradas e
   rastreáveis — incomum e valioso; dá para saber exatamente o que falta.
2. **"Dependência de dados legados (Scout/Kaique)" marcada como Alta
   probabilidade é a única linha da tabela de riscos que menciona risco de
   pessoa/processo, não de sistema** — reconhece que parte do risco é
   organizacional, não técnico.
3. **As mitigações propostas na tabela de riscos são, em sua maioria,
   consistentes com o que já vimos implementado nas fases** (retry,
   aprovação humana, alerta em N dias) — não é lista de boas intenções
   desconectada do resto do documento.

### Pontos fracos / riscos
1. **A mitigação para "MPI Plus indisponível" ("GM segue com dados em
   cache, ações pendentes") não tem duração máxima de cache definida.**
   Quão velho pode ficar o dado em cache antes de a análise deixar de fazer
   sentido? Não está quantificado.
2. **"Dependência de dados legados (Scout/Kaique)" é Alta probabilidade mas
   a mitigação é vaga** ("força-tarefa, prazo definido pela gestão") — sem
   prazo real nem plano B se a força-tarefa não completar a tempo.
3. **Nenhuma das 30 questões em aberto tem dono nem prazo atribuído no
   próprio documento** — todas dizem "a definir com X", sem data. Combina
   com o padrão já visto em vários blocos: o PRD é forte descrevendo o
   **o quê**, sistematicamente fraco em **quando** e **quem**.
4. **17 de 30 questões em aberto (mais da metade) ainda sem definição**,
   incluindo pontos que tocam integrações críticas (Salesforce, MPI Plus) —
   sinal de que o documento é melhor tratado como "v1 para validação", não
   como especificação pronta para construção sem mais rodadas.

### Observações candidatas a backlog
- Definir duração máxima aceitável do cache de dados do MPI Plus antes de a
  análise ser considerada obsoleta/inválida.
- Atribuir prazo real e plano B para a força-tarefa de importação de dados
  legados (Scout/Kaique) — hoje sem data.
- Atribuir dono e prazo para cada uma das 17 questões em aberto restantes,
  transformando-as de "a definir" em itens rastreáveis de backlog com
  responsável.
- Avaliar se o PRD deveria ter um ciclo formal de revisão/aprovação "v2"
  antes do início da construção, dado o volume de questões em aberto (mais
  de 50% do total).

---

## Alinhamento SEO/GEO/AEO com práticas atuais do Google (2026-07-02)

> Avaliação adicional, fora da revisão fase a fase original — cruza o
> fluxo do Growth Machine com práticas de SEO/GEO/AEO vigentes. Ideias e
> oportunidades derivadas ficam registradas separadamente em
> [[01-Ideias/growth-machine-geo-aeo-oportunidades]].

### Onde está alinhado
1. **E-E-A-T é princípio explícito nos prompts de conteúdo**, não
   afterthought — auditado na prática pela Dimensão 2.
2. **Dimensão 2C já cobre GEO/AEO de verdade**: "estrutura para mecanismos
   generativos, FAQ, headings, resumo objetivo, entidades relevantes,
   clareza contextual" — não é só SEO tradicional disfarçado.
3. **RN-82 (AI Instructions/LLM.txt) é prática à frente da curva** — a
   maioria das ferramentas de SEO do mercado ainda não oferece isso.
4. **Dados estruturados (Dimensão 6) levados a sério**, com regra
   anti-spam — importa mais agora, já que AI Overview e LLMs dependem de
   extração estruturada.
5. **Anti-canibalização + arquitetura em silo está alinhada com "topical
   authority"**, exatamente o que o Helpful Content System do Google
   recompensa.
6. **Regra anti-alucinação no conteúdo gerado é mais crítica agora** —
   erro factual citado por um LLM é erro visível na resposta da IA.

### Onde fica atrás
1. **Gap mais crítico: o GM prepara o site para ser citável, mas nunca
   mede se ele está sendo citado.** O Índice de Performance (40/40/20) é
   100% SEO tradicional (posicionamento/tráfego/leads) — nenhuma métrica
   de GEO/AEO real (frequência de citação, Share of Voice em LLM). Essa
   métrica **já existe no cofre**, isolada no [[03-Produtos/ideal-tracker]]
   — os dois produtos não estão conectados.
2. **Cadência de revisão de conteúdo (RN-59, 6 meses) é lenta** para o
   ritmo que busca generativa exige — recompensa frescor mais que SEO
   tradicional recompensava.
3. **Sem estratégia de autoridade de entidade (Knowledge Graph)** —
   Dimensão 2C cita "entidades relevantes" na estrutura da página, mas não
   há nada sobre presença de entidade fora do site (Wikidata, consistência
   de marca), cada vez mais decisivo para aparecer em AI Overview.
4. **Vídeo é ponto cego total** — nenhuma das 10 dimensões toca conteúdo
   em vídeo, que cresce em resultados de busca e respostas de IA.
5. **Sem incentivo a dado/pesquisa original** — audita cobertura da SERP,
   mas não há sinal para "informação exclusiva que só essa empresa tem",
   justamente o que motores generativos preferem citar.
6. **GA4 não segmenta tráfego de referência de IA** (ChatGPT, Perplexity
   como origem) — fonte de tráfego crescente e hoje invisível no
   diagnóstico.

### Observações candidatas a backlog
- Integrar sinal de citação em LLM (Ideal Tracker) ao diagnóstico do Growth Machine.
- Revisar a cadência de 6 meses da RN-59 frente ao ritmo de busca generativa.
- Adicionar segmentação de tráfego por origem de IA no GA4/Motor de Percepção.
- Criar sinal de conteúdo original/dado exclusivo na Dimensão 2.
- Criar checagem de presença de entidade (Knowledge Graph/Wikidata).
- Avaliar cobertura de vídeo como nova dimensão ou subcritério.
- Evoluir RN-82 de "existe sim/não" para avaliar qualidade/eficácia do AI Instructions/LLM.txt.

Todas as 6 observações acima foram formalizadas em
[[05-Backlog/gm-integrar-sinal-citacao-llm-ideal-tracker]] (alta),
[[05-Backlog/gm-segmentar-trafego-origem-ia]] (média),
[[05-Backlog/gm-sinal-conteudo-original]] (média),
[[05-Backlog/gm-evoluir-rn82-qualidade-ai-instructions]] (média),
[[05-Backlog/gm-checagem-presenca-entidade]] (baixa),
[[05-Backlog/gm-cobertura-video-como-dimensao]] (baixa).

---

## Itens de backlog formalizados
As observações candidatas a backlog de todos os blocos acima foram
agrupadas por tema e viraram 10 itens formais em [[05-Backlog]],
priorizados pela Síntese Executiva:
- [[05-Backlog/gm-fechar-questoes-integracao-salesforce-mpiplus]] (alta)
- [[05-Backlog/gm-atribuir-dono-prazo-questoes-abertas]] (alta)
- [[05-Backlog/gm-desenho-fino-prompts-agentes]] (alta)
- [[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]] (alta)
- [[05-Backlog/gm-calibracao-thresholds-numeros-negocio]] (média)
- [[05-Backlog/gm-segregacao-funcoes-pontos-controle]] (média)
- [[05-Backlog/gm-criterio-desempate-fronteiras-componentes]] (média)
- [[05-Backlog/gm-escopo-sentinela-infraestrutura-cron]] (média)
- [[05-Backlog/gm-dimensionamento-cotas-ferramentas-externas]] (média)
- [[05-Backlog/gm-salvaguarda-aprovacao-massa-telas]] (baixa)

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[00-Cerebro]]
