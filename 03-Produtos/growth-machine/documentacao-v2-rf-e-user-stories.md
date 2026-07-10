---
tipo: produto
status: rascunho
criado: 2026-07-08
ultima-revisao: 2026-07-08
tags: [growth-machine, prd, v2, requisitos-funcionais, user-story, criterio-aceite, demonstracao]
---

# Documentação v2 — Blocos 5 (RF) e 8 (User Stories + CA) · demonstração

> **Natureza desta nota:** rascunho de **demonstração de formato**, não a
> versão final. Nasceu para dar percepção de como ficam os dois blocos
> hoje ausentes do PRD (Requisitos Funcionais numerados e User Stories com
> Critérios de Aceite), antes de escalar para o PRD inteiro. Formato
> aprovado pelo PO em 2026-07-08. Fonte da lacuna e do plano:
> [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]]. As RNs
> citadas estão em [[03-Produtos/growth-machine/catalogo-regras-negocio]].
> O padrão de User Story/CA segue [[04-Decisões/padrao-historia-jira]].
>
> **Status (2026-07-08):** demonstração **absorvida** no PRD consolidado
> [[03-Produtos/growth-machine/prd-v2-mvp]] (Blocos 5 e 8). Mantida por
> rastreabilidade do formato aprovado. **Nota (2026-07-10):** o valor de
> RF-11 abaixo (40/40/20) é o default histórico da época — foi revisado
> para **35/20/45**, ver [[04-Decisões/adr-pesos-indice-performance-2026]].
>
> **Escopo do rascunho:** os RF abaixo são uma **fatia representativa**
> (cobre as 4 fases + Sentinela + transversais para mostrar a forma), não a
> lista completa. A extração total dos RF das 4 fases / 10 dimensões / 11
> telas fica para o próximo passo, quando o PO liberar.

## A corrente que estes dois blocos destravam
**RF (o quê o sistema faz) → RN (a restrição que governa) → CA (como o dev
prova que terminou).** O PRD atual tem só o elo do meio (as 122 RNs). Sem
as pontas, não há como afirmar "isto está pronto". Ao escrever os CA, os
buracos aparecem sozinhos: **RN sem RF** = regra sem lugar de aplicação;
**RF sem RN** = capacidade sem restrição (candidata a bug); **CA que não
fecha** = decisão de negócio que ainda falta tomar.

---

## Bloco 5 — Requisitos Funcionais (RF) · fatia representativa

Cada RF é uma capacidade ("o sistema deve…") e aponta a(s) RN que a
restringe. Na v2 isto vira a lista completa numerada.

### Fase 1 — Entrada e Briefing
| RF | O sistema deve… | RN que governa |
|---|---|---|
| **RF-01** | Importar briefing/estudo/histórico de cliente com dados completos via API do MPI Plus | RN-102, RN-101 |
| **RF-02** | Varrer todas as páginas do site via FireCrawl e pré-preencher o briefing quando o cliente for legado (`customer_type='old'`) | RN-69, RN-102 |
| **RF-03** | Conduzir a validação do briefing pelo CS junto ao cliente, bloqueando o avanço da análise até validação ativa | RN-01, RN-06 |
| **RF-04** | Calcular o score de aderência do estudo e aplicar a régua de decisão (manter / complementar / reformular) | RN-04 (régua Dim 1) |
| **RF-05** | Sugerir bonificação de palavras por similaridade vetorial, limitada a 50% do pacote e sem canibalização | RN-15, RN-85 |
| **RF-06** | Incrementar o briefing automaticamente a cada ação validada, sem substituir o aprovado | RN-80 |

### Fase 2 — Motor de Percepção
| RF | O sistema deve… | RN que governa |
|---|---|---|
| **RF-07** | Disparar o ciclo para toda a carteira na chegada do relatório mensal do MPI Plus | RN-106 |
| **RF-08** | Bloquear totalmente a análise (Hard Stop) quando o relatório mensal estiver ausente | RN-64 |
| **RF-09** | Converter posição média em CTR por faixa, sem arredondamento | RN-16 |
| **RF-10** | Calcular a maturidade por interpolação linear e aplicar o teto de crescimento | RN-17 |
| **RF-11** | Calcular o Índice de Performance com pesos parametrizáveis (default 40/40/20) | RN-18 |
| **RF-12** | Classificar o projeto em Ruim/Regular/Bom/Ótimo com thresholds inclusivos e definir a cadência | RN-19, RN-02 |

### Fase 3 — Auditoria em 10 Dimensões
| RF | O sistema deve… | RN que governa |
|---|---|---|
| **RF-13** | Interromper a auditoria **apenas** quando a Dimensão 1 (Estudo) for crítica; caso contrário, rodar as dimensões 2–10 em paralelo | RN-88 |
| **RF-14** | Calcular o Score de Saúde Técnica determinístico (0–100) a partir das dimensões estruturais | RN-96 |
| **RF-15** | Executar as checagens determinísticas (Dim 4, 5, 6, 7, 9) sem uso de IA | RN-99, RN-115–120 |
| **RF-16** | Bloquear sugestão de schema fabricado (reviews/ratings/preços/FAQ não verificáveis) | RN-117 |
| **RF-17** | Gerar o Parecer Consolidado por IA (1x/análise), mantendo Índice + Score + dimensões separados | RN-97 |

### Fase 4 — Aprovação, Execução e Validação
| RF | O sistema deve… | RN que governa |
|---|---|---|
| **RF-18** | Exportar ao Salesforce **apenas** ações aprovadas pelo analista, agrupadas por área, só título e escopo | RN-75, RN-76, RN-78 |
| **RF-19** | Sincronizar de volta o status quando a atividade é concluída no Salesforce | RN-77 |
| **RF-20** | Reler o site na validação e conferir cada ação executada (validação automática por IA) | RN-81 |
| **RF-21** | Iniciar a maturação de 60 dias somente após o OK final do analista | RN-27, RN-79 |
| **RF-22** | Registrar motivo e escalar ao Supervisor/Líder quando uma ação é desconsiderada | RN-45 |

### Sentinela + Transversais
| RF | O sistema deve… | RN que governa |
|---|---|---|
| **RF-23** | Rodar checagens diárias leves em 100% dos sites, inclusive bloqueados/em maturação | RN-90, RN-91, RN-93 |
| **RF-24** | Emitir alerta antecipado de SSL em 30/15/7 dias | RN-95 |
| **RF-25** | Reabrir a análise mesmo em maturação diante de incidente crítico de infra (site fora ≥3d, SSL expirado) | RN-94 |
| **RF-26** | Registrar em todo log de execução `prompt_version_id`, `ruleset_version_id`, entradas, saída JSON e confiança | RN-122 |
| **RF-27** | Nunca expor métricas financeiras / custo por token na interface ou logs públicos | RN-73 |

---

## Bloco 8 — User Stories + Critérios de Aceite (Gherkin) · exemplos

Uma história por RF (ou grupo), com CA em Dado/Quando/Então — cada CA
aponta **qual RN ele testa**. Essa amarração RN→CA é o que torna o PRD
auditável ponta a ponta.

### US-01 — Validação de briefing pelo CS *(cobre RF-03)*
> **Como** CS, **quero** validar o briefing pré-preenchido com o cliente
> antes de a análise seguir, **para** que nenhum diagnóstico rode sobre
> dado não confirmado.

1. **CA-01.1** — *Dado* um briefing pré-preenchido, *Quando* o CS marca
   "Confirmado", *Então* a análise avança para o Motor de Percepção.
   → testa **RN-01**
2. **CA-01.2** — *Dado* um briefing pendente, *Quando* o cliente não
   responde, *Então* a análise **não** avança e o briefing fica pendente
   **sem prazo automático**. → testa **RN-01**
3. **CA-01.3** — *Dado* que o cliente já rejeitou o estudo 2 vezes,
   *Quando* ocorre a 3ª rejeição, *Então* o caso é escalado ao Gerente.
   → testa **RN-06**

> ⚠️ **Gap exposto pelo CA:** não existe CA para "briefing parado há X
> dias" porque **não há regra de envelhecimento** (RN-01 = "sem prazo
> automático"). O CA que faltaria aqui é exatamente
> [[05-Backlog/gm-alerta-envelhecimento-sem-prazo-automatico]].

### US-02 — Classificação de performance do projeto *(cobre RF-11, RF-12)*
> **Como** analista, **quero** que o sistema classifique cada projeto por
> uma fórmula auditável, **para** priorizar a carteira sem julgamento
> manual.

1. **CA-02.1** — *Dado* índice final **0,80**, *Quando* o Motor classifica,
   *Então* o status é **Bom** (não Regular) — limite sobe de categoria.
   → testa **RN-19**
2. **CA-02.2** — *Dado* posição média **10,5**, *Quando* o CTR é calculado,
   *Então* o CTR é **1%** (sem arredondar para Top 10). → testa **RN-16**
3. **CA-02.3** — *Dado* status **Bom**, *Quando* a cadência é definida,
   *Então* a análise passa a **trimestral**. → testa **RN-02**

### US-03 — Travamento condicional da auditoria *(cobre RF-13)*
> **Como** analista, **quero** que só um estudo crítico trave a auditoria,
> **para** não segurar 9 dimensões independentes por causa de uma.

1. **CA-03.1** — *Dado* Dimensão 1 com score **crítico**, *Quando* a
   auditoria roda, *Então* as dimensões 2–10 são **bloqueadas**.
   → testa **RN-88**
2. **CA-03.2** — *Dado* Dimensão 1 **OK** e Dimensão 5 crítica, *Quando* a
   auditoria roda, *Então* as dimensões 2–10 rodam **em paralelo** e geram
   ações simultâneas. → testa **RN-88**

> ⚠️ **Gap exposto pelo CA:** e se Dim 2 e Dim 3 recomendarem ações
> conflitantes na mesma página? Não há RN de desempate — é
> [[05-Backlog/gm-criterio-desempate-fronteiras-componentes]]. Um CA "não
> escrevível" = decisão que falta tomar.

---

## O que fica provado nesta demonstração
1. **"Pronto para dev" deixa de ser opinião** — cada RF exige uma RN, cada
   RN exige um CA. O checklist vira mensurável.
2. **Escrever o CA revela a regra ausente** — os 2 avisos acima nasceram de
   tentar escrever o teste; viram backlog rastreável em vez de surpresa em
   produção.
3. **Reaproveita padrão que o cofre já tem** — Dado/Quando/Então do
   [[04-Decisões/padrao-historia-jira]], hoje usado só no MPI Plus.

## Próximo passo (aguardando liberação do PO)
- [ ] Extrair a lista **completa** de RF (4 fases / 10 dimensões / 11 telas).
- [ ] Uma User Story + CA por RF, cada CA amarrado a RN.
- [ ] Consolidar no PRD v2 junto aos demais 11 blocos (ver esqueleto em
  [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] Parte 4).

## Notas relacionadas
- [[03-Produtos/growth-machine/avaliacao-aderencia-doc-ideal]] — origem: aderência aos 13 blocos e plano da v2
- [[03-Produtos/growth-machine/catalogo-regras-negocio]] — as RNs citadas nos RF/CA
- [[04-Decisões/padrao-historia-jira]] — padrão de User Story/CA adotado aqui
- [[03-Produtos/growth-machine]] — nota-mãe do produto
- [[00-Painel-Estado]]
