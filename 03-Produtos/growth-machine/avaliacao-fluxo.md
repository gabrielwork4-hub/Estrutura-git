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
> _A preencher na próxima etapa da revisão._

## Fase 4 — Workflow de Aprovação, Execução e Validação
> _A preencher na próxima etapa da revisão._

---

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[00-Cerebro]]
