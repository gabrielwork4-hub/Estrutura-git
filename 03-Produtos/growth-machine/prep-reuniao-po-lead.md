---
tipo: produto
status: vivo
criado: 2026-07-03
ultima-revisao: 2026-07-10
tags: [growth-machine, reuniao, po, preparacao]
---

# Preparação — Reunião com responsável pelos POs (2026-07-03)

> Nota de preparo, não de debate. Objetivo: chegar estruturado com RN e
> PRD, confirmar alinhamento — **não reabrir discussão técnica já
> mapeada**. Base: [[03-Produtos/growth-machine/cheat-sheet]],
> [[03-Produtos/growth-machine/catalogo-regras-negocio]] e
> [[03-Produtos/growth-machine/avaliacao-fluxo]].

## Postura na reunião
Dev já rodando, líder já tocando execução. Papel aqui é **confirmar**, não
questionar arquitetura. As 3 perguntas da seção final são as únicas que
valem levantar — o resto é domínio de contexto para responder com
segurança se perguntado.

---

## 1. O produto em 1 frase (se pedirem para situar)
Growth Machine diagnostica ~2.500 clientes MPI automaticamente (hoje
~90h/analista/mês manual), gera fila de ações priorizada. Não publica nada
sozinho — Front-end executa via Salesforce.

## 2. Números que preciso ter na ponta da língua

| O quê | Valor |
|---|---|
| Pré-requisito de carteira | **RN-108** — só atende quem já está no MPI Plus |
| Pesos do Índice de Performance | **40 posicionamento / 40 tráfego / 20 leads** — ⚠️ sob revisão (achado F-30: diverge do Gregory e da ata; ver [[04-Decisões/adr-camada-calibracao-continua]]) |
| Thresholds de status | Ruim &lt;0,60 · Regular 0,60–0,79 · Bom 0,80–0,89 · Ótimo ≥0,90 |
| Janela de maturação | **60 dias fixos**, começa só após OK do analista (RN-27, RN-79) |
| Gatilho do ciclo | Relatório mensal MPI Plus, ~dia 1º/2 (RN-106) |
| Travamento da auditoria | Só a Dimensão 1 (Estudo) trava tudo; as outras 9 rodam em paralelo (RN-88) |
| Aprovação humana | Nada é publicado automaticamente, sempre (RN-47) |
| Modelo padrão dos agentes | GPT-5 (RN-99) |

## 3. RNs mais prováveis de aparecer numa conversa de PO (por tema)

**Elegibilidade e integração MPI Plus**
- RN-100 — GM detecta o gap, não gera; geração só após clique do analista (Gate 1) e revisão (Gate 2)
- RN-104 — GM é 100% interno, cliente nunca acessa
- RN-108 — pré-requisito de carteira

**Governança/aprovação**
- RN-47 — aprovação humana obrigatória
- RN-49 — Analista acumula aprovação inicial + validação final (persona "Revisor" extinta)
- RN-73 — proibido expor custo/token/precificação de API na interface

**Ciclo e cadência**
- RN-02 — cadência Ruim/Regular mensal, Bom/Ótimo trimestral
- RN-27 — 60 dias de maturação
- RN-59 — conteúdo só reavaliado a cada 6 meses (salvo força do analista)

**Integração Salesforce**
- RN-74 — Salesforce é fonte única de gestão de atividades, GM não duplica
- RN-78 — só título e escopo trafegam pro Salesforce, nada de detalhe técnico

Catálogo completo (todas as 122) em
[[03-Produtos/growth-machine/catalogo-regras-negocio]] — se o responsável
citar um número específico e eu não souber de cabeça, consulto ali na hora.

## 4. Estrutura do PRD, se pedirem visão geral
- **Parte I** — Visão Executiva (problema, solução, 4 fases, impacto esperado)
- **Parte II** — Processo Operacional (as 4 fases + Sentinela em detalhe)
- **Parte III** — Especificação Técnica (122 RNs, 11 telas, 24 NFRs, 30 questões em aberto)

**As 4 fases, em ordem:** Briefing → Motor de Percepção (mensal) → Auditoria (10 dimensões) → Aprovação/Execução/Validação.

**Os 3 sistemas, papéis que nunca se misturam:** Growth Machine diagnostica · MPI Plus gera+aprova cliente · Salesforce executa.

## 5. As 3 perguntas que valem levar (confirmação, não debate)
1. **As 7 questões de integração Salesforce/MPI Plus (Q18–21, Q27–30) já foram resolvidas na prática?** Se sim, só preciso registrar como ficou decidido.
2. **Quem está escrevendo os prompts dos 9 agentes de IA, e em que prazo relativo ao código?** É o único ponto que pode virar gargalo de entrega se ninguém estiver dono disso agora.
3. **Existe algo sendo construído que diverge do PRD original por decisão de prazo?** Não para reverter — só para eu manter a documentação do cofre alinhada com o que está sendo entregue de verdade.

## 6. O que **não** levar para esta reunião
- Calibração dos thresholds (70%, 50%, 40/40/20 etc.) — sem origem documentada, mas não é pauta agora.
- Oportunidades de GEO/AEO e integração com Ideal Tracker — registradas como ideia futura, não escopo atual.
- Qualquer um dos 10 itens de backlog de média/baixa prioridade — só o item de alta (integração) é o que pode justificar menção.

## Notas relacionadas
- [[03-Produtos/growth-machine/cheat-sheet]]
- [[03-Produtos/growth-machine/catalogo-regras-negocio]]
- [[03-Produtos/growth-machine/avaliacao-fluxo]]
- [[00-Painel-Estado]]
