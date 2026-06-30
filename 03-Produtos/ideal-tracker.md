---
tipo: produto
status: em-desenvolvimento
criado: 2026-06-30
origem:
  - "Notion — transcrição @hoje 10:12 (BRT), conversa com Lucas"
  - "Drive — [IdealTrack] Documento de Produto Pt #1 e Pt #2"
  - "Drive — Pontos de Atenção - Ideal Track (MVP)"
  - "Drive — Briefing de UX — Visão e Referências"
tags: [produto, ideal-tracker, geo, llm-visibility]
---

# Ideal Track (IdealTrack)

## Visão geral
Ferramenta de **GEO (Generative Engine Optimization)** — monitora
continuamente como uma marca aparece nas respostas de LLMs (ChatGPT, Gemini,
Perplexity...) e transforma isso em visibilidade real: histórico, comparativo
com concorrentes e **Share of Voice (SoV)** por modelo. Além de mostrar onde
a marca falha, indica o que fazer (IdealAgent gera conteúdo para o gap).

Autor/Head: Luis Ottoni. Status dos docs: rascunho (04–07/05/2026).

**Para quem:** especialista de marketing digital (Solo/Pro/Expert), agências
(Authority/Operator/Growth), gerente de marketing, consultor independente.

## Loop de valor
Monitorar → IdealAgent acha o gap → gera conteúdo → publica → SoV sobe.

## Funcionalidades mapeadas
- [ ] Cadastro/login (e-mail+senha ou Google OAuth), projeto padrão criado automaticamente, trial inicia no cadastro.
- [ ] Onboarding guiado: marca, concorrentes, primeiros prompts de monitoramento.
- [ ] Dashboard: SoV por LLM, histórico, comparação com concorrentes.
- [ ] IdealReport — gerar/exportar relatórios.
- [ ] IdealAgent — gerar conteúdo a partir do gap identificado.
- [ ] PitchIdealTrack (planos Authority/Operator/Growth) — gerar pitch a partir de domínio prospect.
- [ ] WhiteLabel e integrações (Google Search Console, Ahrefs).

## ⚠️ Pontos de atenção levantados (revisão crítica, 29/05)
Esses pontos ainda não têm resposta definida — ficam como problemáticas em aberto:
1. **Metodologia de medição do SoV não está definida.** "ChatGPT" no MVP é o produto ou a API (GPT-4o via API ≠ ChatGPT que o cliente usa)? Quantos runs por prompt por coleta (não-determinismo dos LLMs vs. exigência de SoV "reproduzível e auditável")?
2. **Google AI Overview não tem API oficial** — depende de scrapers de terceiros (SerpApi, SERPHouse), o que é custo/risco de ToS não mapeado no PRD.
3. **Loop de valor pode não fechar no MVP**: ChatGPT responde do treino, não da web em tempo real — publicar conteúdo hoje não muda a resposta do ChatGPT no mês. Só modelos com retrieval (AIO, Perplexity, AI Mode, Copilot) refletem conteúdo novo, e estão em fases/planos superiores.
4. **Matemática de "prompts × respostas" não fecha** entre os planos (ex: Pro = 150 prompts × 5 LLMs × 30 dias = 22.500, mas teto declarado é 9.000) — falta definir o que conta como "uma resposta".
5. **Contradições entre documentos**: duração do trial (7 dias no PRD vs. 14 dias no RG-011/UX), política de cartão, política de retenção de dados (indefinida vs. 2 anos vs. 30 dias).
6. **Empacotamento dos planos com inversão**: plano de agência de entrada (Authority) tem menos projetos (2) que o plano de especialista mais barato (Pro, 4 projetos).

## Cruzamento com outras notas
- Citado na transcrição de kick-off ([[02-Fluxos/processo-kickoff-discovery]]) como um dos 3 projetos em andamento, ao lado de [[03-Produtos/mpi-plus]] e [[03-Produtos/growth-machine]].
- Os pontos de atenção acima (especialmente metodologia de medição e definição de prompts) deveriam virar itens formais em [[05-Backlog]] antes do MVP avançar.

## Decisões relacionadas
-

## Ideias relacionadas
-
