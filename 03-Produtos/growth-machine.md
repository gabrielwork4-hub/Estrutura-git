---
tipo: produto
status: em-desenvolvimento
criado: 2026-06-30
origem:
  - "Notion — transcrição @hoje 10:39 (BRT)"
  - "Drive — PRD_Growth_Machine_v1_9_14.md (16/06/2026)"
  - "Drive — REUNIÕES - AUTOMAÇÃO / Kickoff - Growth Machine"
tags: [produto, growth-machine, keywords, seo]
---

# Growth Machine

## Visão geral
Plataforma interna de orquestração de SEO (Ideal Marketing · Busca Cliente ·
MPI Solutions) que automatiza o diagnóstico de ~2.500 projetos MPI de ponta
a ponta. Hoje cada analista gasta ~90h/mês diagnosticando manualmente
(Search Console, Excel, PageSpeed, SendGrid...). O método MPI funciona mas
vive na cabeça de especialistas sêniors — sem padronização nem escala.

**Pré-requisito:** o GM só atende clientes que já estão no **MPI Plus**
(RN-108). Cliente fora do MPI Plus entra primeiro nele.

## Como funciona — 4 fases
1. **Entrada e Briefing** — importa dados do MPI Plus (se existir) ou roda
   crawler FireCrawl no site e pré-preenche o briefing. Validação feita pelo
   **CS junto ao cliente** (não o cliente sozinho); sem validação ativa, o
   briefing fica pendente (RN-01).
2. **Motor de Percepção** (mensal) — posicionamento/tráfego/leads do
   relatório MPI Plus (fallback Bright Data) → CTR dinâmico por posição →
   Índice de Performance (**40 posicionamento / 40 tráfego / 20 leads**) →
   status Ruim/Regular/Bom/Ótimo.
3. **Auditoria em 10 dimensões** — Estudo/Auditoria MPI → Conteúdo/Imagem/GEO
   → Arquitetura MPI/Silo/Linkagem → W3C → PageSpeed/Performance Front-end →
   Schemas JSON-LD → Sitemap/Robots/Indexabilidade → Search Console/Sinais
   Externos → Servidor/TTFB/Infraestrutura → Captação/Entrega/Qualidade.
4. **Fila de ações** priorizada, exportada como atividades no **Salesforce**.
   O sistema não publica nada sozinho — a execução técnica/publicação é
   sempre manual.

## Impacto esperado
| Métrica | Hoje | Com Growth Machine |
|---|---|---|
| Horas de diagnóstico/analista/mês | ~90h | <10h |
| Cobertura da carteira | ~60 clientes/analista | 100% |
| Briefings atualizados | <20% | >80% em 6 meses |
| Taxa de aceitação de ações sugeridas | N/A | >70% |

## Status atual (10:39 — hoje, Notion)
- Conectar **Wiki Data ao fluxo** e definir os principais indicadores.
- Estudar a documentação da Growth Machine (PRD v1.9.14) para identificar
  melhorias de entrega.
- O **briefing preenchido** será a base de toda a estratégia.
- Implementação de blog (implementação + relatório).
- Trabalhar com o **conteúdo MPI Plus**.

## Funcionalidades
- [ ] Conectar Wiki Data ao fluxo
- [ ] Definir principais indicadores (pesos posicionamento/tráfego/leads)
- [ ] Estruturar briefing como base da estratégia (validação via CS)
- [ ] Implementar blog (implementação + relatório)
- [ ] Integrar conteúdo MPI Plus
- [ ] Exportação de fila de ações para Salesforce

## Regras de negócio chave (do PRD)
- RN-108: GM só atende clientes presentes no MPI Plus.
- RN-01: análise não avança sem validação ativa do cliente/CS — sem prazo automático, fica pendente.
- Pesos do Índice de Performance: 40% posicionamento, 40% tráfego, 20% leads.

## Cruzamento com outras notas
- A implementação de blog e o conteúdo MPI Plus dependem diretamente do
  fluxo de [[02-Fluxos/estudo-de-keywords]] (clusterização, anti-canibalização,
  variações locais) para não repetir o erro de keyword isolada — a dimensão
  1 da auditoria ("Estudo/Auditoria MPI") é exatamente onde isso se aplica.
- Faz parte do processo geral descrito em [[02-Fluxos/processo-kickoff-discovery]].
- Depende do **MPI Plus** como pré-requisito de carteira — ver [[03-Produtos/mpi-plus]].

## Decisões relacionadas
-

## Ideias relacionadas
-
