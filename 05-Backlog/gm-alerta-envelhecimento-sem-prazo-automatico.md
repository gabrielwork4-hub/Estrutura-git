---
tipo: backlog
status: aberto
prioridade: alta
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, padrao-recorrente, alerta, sla]
---

# Definir alerta de envelhecimento onde hoje não há prazo automático (Growth Machine)

## Problema
Padrão que se repete em pelo menos 2 pontos do fluxo: "sem prazo
automático" sem mecanismo de alerta equivalente.
- **Fase 1 (Briefing)**: RN-01 permite briefing pendente indefinidamente
  sem notificação proativa — existe alerta de 28 dias para ações não
  executadas (RN-04), mas nada equivalente para o briefing parado.
- **Fase 4 (Validação)**: sem SLA para o tempo entre "Salesforce sincroniza
  conclusão" e "Analista aciona Validar" — pode atrasar indefinidamente o
  início da maturação de 60 dias sem alerta.

## Impacto
É o risco estrutural mais recorrente do PRD — mais do que qualquer risco
técnico pontual. É exatamente o tipo de furo que gera "cliente ligando
furioso", o sintoma que o próprio produto foi criado para eliminar.

## Proposta de ajuste
Definir alerta de envelhecimento (equivalente ao RN-04, N dias sem ação)
para: (1) briefing pendente de validação do cliente/CS, (2) ação concluída
no Salesforce aguardando validação do analista no GM. Ver detalhamento em
[[03-Produtos/growth-machine/avaliacao-fluxo]], "Fase 1" e "Fase 4".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
