---
tipo: produto
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-10
tags: [growth-machine, cheat-sheet, resumo]
---

# Cheat Sheet — Growth Machine

> Uma página. Só o que você citaria de cabeça numa reunião, sem abrir nada.
> Para contexto/explicação completa, ver [[03-Produtos/growth-machine]].

## O produto em 1 frase
Orquestração de SEO que diagnostica ~2.500 clientes MPI automaticamente
(hoje ~90h/analista/mês manual) e gera fila de ações priorizada — não
publica nada sozinho, quem executa é o Front-end via Salesforce.

## Pré-requisito
**RN-108** — só atende cliente já no **MPI Plus**. Fora do MPI Plus →
entra lá primeiro.

## Números que valem de cabeça

| O quê | Valor |
|---|---|
| Pesos do Índice de Performance | **35 posicionamento / 20 tráfego / 45 leads** (revisado 2026-07-10) |
| Thresholds de status | Ruim **&lt;0,60** · Regular **0,60–0,79** · Bom **0,80–0,89** · Ótimo **≥0,90** |
| Cadência de análise | Ruim/Regular → **mensal** · Bom/Ótimo → **trimestral** |
| Janela de maturação | **60 dias fixos**, começa só após OK do analista |
| CTR por posição | Top 3 → **20%** · Top 10 → **5%** · abaixo → **1%** (sem arredondar) |
| Escala | **~2.500 clientes**, 3 empresas (Ideal Marketing / Busca Cliente / MPI Solutions) |
| Gatilho do ciclo | Relatório mensal MPI Plus, **~dia 1º/2** |
| Retry site fora do ar | **3 tentativas**, dias diferentes, antes de alertar |
| Alerta lead zerado | **7 dias** consecutivos sem lead = alerta extremo |
| Alerta SSL | **30 / 15 / 7 dias** antes de expirar |

## As 4 fases (ordem)
**1. Briefing → 2. Motor de Percepção (mensal) → 3. Auditoria (10 dimensões) → 4. Aprovação/Execução/Validação**

## As 10 dimensões (ordem de prioridade MPI)
1. Estudo · 2. Conteúdo/GEO · 3. Arquitetura/Silo · 4. W3C · 5. PageSpeed ·
6. Schemas · 7. Sitemap/Robots · 8. Search Console · 9. Servidor/TTFB ·
10. Leads

**Regra de ouro (RN-88):** só a Dimensão 1 (Estudo) trava a auditoria
inteira. As outras 9 rodam em paralelo.

## 3 sistemas, 3 papéis — nunca se misturam
- **Growth Machine** = diagnostica. 100% interno. Cliente nunca acessa.
- **MPI Plus** = gera conteúdo/estudo + aprovação do cliente.
- **Salesforce** = executa/gerencia atividades.

## Módulo Sentinela (diferente das 10 dimensões)
Roda **todo dia**, à noite, em **100% dos sites** (até os bloqueados/em
maturação) — checa só uptime/SSL/DNS, nada caro. Se site cai ≥3 dias ou
SSL expira → reabre análise mesmo com maturação em curso.

## 9 agentes de IA
Modelo padrão: **GPT-5**. Detectam e recomendam — **nunca publicam**.
Toda ação passa por aprovação humana (RN-47).

## O risco #1 do PRD (citação literal)
> "A casa é entregue vazia; os móveis são os prompts."

Arquitetura pronta, conteúdo fino dos prompts ainda não.

## 5 padrões recorrentes de risco (aplicar em qualquer PRD, não só este)
1. "Sem prazo automático" sem alerta de envelhecimento
2. Números de negócio sem origem documentada
3. Concentração de responsabilidade num único ponto de controle
4. Fronteiras entre componentes sem critério de desempate
5. Questões em aberto sem dono/prazo

## Backlog aberto (10 itens) — ver [[00-Painel-Estado]]
4 alta / 5 média / 1 baixa. Prioridade #1: fechar as 7 questões de
integração Salesforce/MPI Plus (Q18-21, Q27-30) — é o que trava o início
de build de ponta a ponta.

## Notas relacionadas
- [[03-Produtos/growth-machine]] — nota completa
- [[03-Produtos/growth-machine/avaliacao-fluxo]] — avaliação crítica
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — todas as 122 RNs
- [[04-Decisões/adr-pesos-indice-performance-2026]] — origem dos pesos 35/20/45
- [[00-Painel-Estado]]
- [[00-Glossario]]
