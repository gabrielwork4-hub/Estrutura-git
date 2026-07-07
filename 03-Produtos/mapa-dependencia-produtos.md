---
tipo: produto
status: vivo
criado: 2026-07-02
ultima-revisao: 2026-07-02
tags: [mapa, dependencia, prioridade]
---

# Mapa de Dependência entre Produtos

> Visão única de "quem depende de quem" — cada produto individual já
> menciona isso em frases soltas dentro do próprio texto; esta nota existe
> para não obrigar quem chega agora a montar esse quebra-cabeça lendo nota
> por nota.

## Cadeia de dependência

```
Cliente novo
    │
    ▼
[[03-Produtos/mpi-plus]] (MPI Plus)
    — pré-requisito de carteira (RN-108). Todo cliente monitorado pelo
    Growth Machine precisa estar aqui primeiro. Gera o Estudo (briefing →
    termos → cluster/arquitetura de site) e o Conteúdo (artigo SEO).
    │
    ▼
[[03-Produtos/growth-machine]] (Growth Machine)
    — só atende clientes já no MPI Plus. Diagnostica (10 dimensões),
    prioriza ações, exporta para o Salesforce. Não gera conteúdo — aciona
    o MPI Plus para gerar/refazer quando necessário.
    │
    ▼
Salesforce (execução técnica real, fora do escopo deste cofre)


[[03-Produtos/ideal-tracker]] (Ideal Track)
    — produto independente da cadeia acima. Não depende de MPI Plus nem
    de Growth Machine. Mede visibilidade em LLMs (GEO/AEO), não SEO
    tradicional. Roda em paralelo, sem dependência de carteira.
```

## Por produto

| Produto | Depende de | Do que depende dele | Status de documentação |
|---|---|---|---|
| [[03-Produtos/mpi-plus]] | Nada (é a base) | [[03-Produtos/growth-machine]] (RN-108) | Sem PRD próprio no Drive; 2 histórias oficiais de prompt documentadas |
| [[03-Produtos/growth-machine]] | [[03-Produtos/mpi-plus]] (carteira) | Salesforce (execução, fora do cofre) | PRD completo (v1.9.14) + avaliação crítica + 10 itens de backlog |
| [[03-Produtos/ideal-tracker]] | Nada | Nada (independente) | PRD + funcionalidades + UX documentados; 6 pontos críticos em aberto ([[05-Backlog/ideal-track-definir-metodologia-sov]]) |

## Prioridade de foco atual
Definida pelo PO em 2026-07-02: **Growth Machine é a prioridade corrente**
— é onde a maior parte do aprofundamento (PRD completo, avaliação crítica,
backlog) já aconteceu. MPI Plus vem em seguida por ser pré-requisito
técnico direto do Growth Machine (RN-108) — mudanças nos prompts do MPI
Plus afetam diretamente a Dimensão 1 e 2 da auditoria do Growth Machine.
Ideal Tracker fica em terceiro por não ter dependência cruzada com os
outros dois — pode ser retomado a qualquer momento sem destravar/travar as
outras frentes.

Esta ordem deve ser revisitada sempre que a prioridade de negócio mudar —
atualizar esta seção em vez de deixar a informação implícita em outra nota.

## 13 pastas do Drive ainda não avaliadas
Fora da cadeia acima, existem 13 pastas de projeto no Drive nunca
aprofundadas (ver [[00-Cerebro]], seção "Outras pastas de projeto"). Não
têm prioridade definida — tratar como backlog de descoberta, não de
execução, até que o PO decida investigar alguma.

## Notas relacionadas
- [[00-Cerebro]]
- [[03-Produtos/mpi-plus]]
- [[03-Produtos/growth-machine]]
- [[03-Produtos/ideal-tracker]]
