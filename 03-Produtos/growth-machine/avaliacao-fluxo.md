---
tipo: fluxo
status: em-construcao
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
desenvolvimento.

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
> _A preencher na próxima etapa da revisão._

---

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[00-Cerebro]]
