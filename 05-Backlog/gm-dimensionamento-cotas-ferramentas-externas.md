---
tipo: backlog
status: aberto
prioridade: media
criado: 2026-07-02
origem-fluxo: "[[03-Produtos/growth-machine/avaliacao-fluxo]]"
tags: [growth-machine, ferramentas-externas, rate-limit, escala]
---

# Dimensionar cotas/rate-limit das ferramentas externas contra a escala real (Growth Machine)

## Problema
A cota de 400 req/dia do PageSpeed parece pequena frente a ~2.500 clientes
rodando páginas MPI elegíveis todo ciclo, sem cálculo documentado de quantos
dias seriam necessários para cobrir a carteira inteira. SemRush Business não
tem cota/rate-limit documentado (diferente do cuidado dado ao PageSpeed).
DataForSEO é usado tanto na Dim 2 (recorrente) quanto na Dim 1 (condicional)
sem teto de chamadas combinado entre os dois usos — risco de competição
interna por cota entre dimensões do mesmo cliente. 6 contas de Google
Search Console para 2.500 clientes sem critério de distribuição explicado.

## Impacto
Sem esse dimensionamento, o sistema pode não conseguir processar a carteira
completa dentro da cadência esperada (mensal para Ruim/Regular, trimestral
para Bom/Ótimo), ou pode estourar limites de API sem aviso.

## Proposta de ajuste
Calcular volume real de chamadas necessárias por ciclo para cada ferramenta
externa e comparar contra a cota disponível, definindo fila/priorização
onde necessário. Ver [[03-Produtos/growth-machine/avaliacao-fluxo]], bloco
"Ferramentas Externas Integradas".

## Relacionados
- Fluxo: [[03-Produtos/growth-machine/avaliacao-fluxo]]
- Produto: [[03-Produtos/growth-machine]]
