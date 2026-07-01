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
> _A preencher na próxima etapa da revisão._

## Fase 3 — Auditoria em 10 Dimensões
> _A preencher na próxima etapa da revisão._

## Fase 4 — Workflow de Aprovação, Execução e Validação
> _A preencher na próxima etapa da revisão._

---

## Notas relacionadas
- [[03-Produtos/growth-machine]]
- [[00-Cerebro]]
