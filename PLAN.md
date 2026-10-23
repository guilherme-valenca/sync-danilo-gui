# Plano: fechar a Sprint 1

**Estado: PROPOSTA do gui (23/10, 16h40). Aguarda `ok danilo` e o OK dos humanos.**

Os dois artefatos e seus briefs mandam em tudo:

- **Data Model Canvas** em `/docs/data_model_canvas/`: `.ipynb` com Spark, Markdown de
  abordagem/premissas/resultados e os 5 componentes (Value Proposition, Data Structure com
  diagrama, User Profile, Data Analysis, Use Cases). Critérios: valor alinhado ao parceiro e
  sustentado pela análise; estrutura viável com diagrama claro; usuários certos; análise
  profunda com combinações novas; casos de uso praticáveis; tudo coerente.
- **Market and Risk Analysis Workbook** em `/docs/Market-and-Risk-Analysis-Workbook.md`:
  VPC, TAM/SAM/SOM coerentes e justificados, ao menos 10 riscos cobrindo equipe, tecnologia,
  complexidade e operação, cada um com dono, posição na matriz e mitigação justificada,
  contextualizados ao parceiro.

Referências do parceiro: `docs/agents/reference/` no repo do G03 (kick-off answers Q01–Q49,
annex C1–C10 e §4, transcript, TAPI).

## Estratégia: integrar primeiro, revisar depois

### Fase 0: integração (gui executa, ~20 min)

Mergear todos os MRs abertos na `develop` **como estão**. Já simulado com `git merge-tree`:
zero conflitos em todos os 132 pares e nas ordens direta e inversa, com a mesma árvore final.

Por quê: cada autor fica com o MR mergeado (registro avaliado), as branches velhas somem e
nossas correções partem de uma base única.

**Antes, danilo:**
1. Mudar o alvo do !21 para `develop` e corrigir a descrição (hoje lista arquivos da develop).
2. Abrir o MR de `feat/notebooks-analise-dados` → `develop` (Refs #2 #7 #13 #14), no
   template Inteli.

**Ordem:** !4 → !13 → !14 → !7 → !15 → !18 → MR dos notebooks → !21 → !20 → !19 → !17 → !11.

- Quem aceita: gui, inclusive os dois do Danilo.
- Fora: !16 (a branch dos slides nunca chegou ao servidor; é do Johlan) e !12 (fechado).
- Apagar a branch `docs/spark-notebook`, que está vazia.
- Guilherme avisa o grupo no WhatsApp antes: "integramos tudo e corrigimos em MRs de
  revisão; os pontos de vocês estão incluídos". O Johlan estava segurando a aprovação do
  !18.

### Fase 1: revisão em paralelo, dividida por artefato e por arquivo

Ninguém edita arquivo ou seção do outro.

| Id | Dono | Issue proposta (título Inteli) | Arquivos e seções |
|---|---|---|---|
| R1 | danilo | Correct the Spark analysis and Section 3.3 against the partner's reconciliation and scope rules | Notebooks (só células markdown, sem re-executar), `analysis.md`, `outputs/*_findings.md`, `data/README.md`, `documentation.md` §3.3 |
| R2 | danilo | Align the Data Model Canvas components with the corrected analysis | `value_proposition.md`, `use_cases.md`, `canvas.md`, `data_model_canvas.json`, `data_structure.md`, `model.dbml`, `model.png`, `documentation.md` §3.1, §3.2 e §3.5 |
| R3 | gui | Consolidate the Market and Risk Analysis Workbook at /docs against the brief and the partner's premises | `docs/Market-and-Risk-Analysis-Workbook.md`, `docs/market/*`, `documentation.md` §4.x e §14, `assets/` |
| R4 | gui | Prioritise the regional managers in the User Profile and Section 2.3 | `user_profile.md`, `documentation.md` §2.3 |
| R5 | gui | Thread de linguagem já em andamento (#33/#34) | `documentation.md` §1, §2.1, §2.2, §2.4 e §3.4, e o `README.md` do DMC no fim |

**Dependências:**
- R2, R3 e R5 citam números só do `FIGURES.md`. O danilo fecha os números **antes** de
  tudo, porque eles destravam o resto.
- R5 entra por último. A branch atual, `docs/introduction-context-and-main-findings`, não
  segue `<N>-<slug>`: recriar a partir da issue antes do MR.

**Ordem de merge:**
- R1 e R2 (gui aceita). R3 e R4 (danilo aceita). São independentes entre si.
- Depois R5 (danilo aceita), que também atualiza o índice `README.md` do DMC.

### Fase 2: fechamento

1. Gate final nos dois briefs, com dois revisores-agentes em paralelo (o parceiro vê isso):
   - caminhos;
   - componentes;
   - links relativos resolvem;
   - números iguais ao `FIGURES.md`;
   - grep abaixo vazio.
2. `develop` → `main` pelo grupo, no fim da sprint.

## Padrão Inteli (vale para tudo da Fase 1)

- **Issue:**
  - título no infinitivo, em inglês, como as existentes;
  - corpo Context / Goal / Acceptance criteria (Given/When/Then, dois cenários);
  - story points 1–5;
  - labels de tipo e artefato (`DOCUMENTATION`, `ANALYSIS`, `DATA_MODEL_CANVAS`,
    `MARKET_AND_RISK`, `TASK_REVIEW`);
  - milestone `Sprint 01`, um assignee.
- **Branch:** `<N>-<slug>` criada pela issue a partir da `develop` pós-Fase 0.
- **Commit:** `docs: <imperativo>` + linha `Refs #N`, sem `Co-Authored-By`.
- **MR:** contra `develop`, com as 4 seções (O que foi feito / Issue relacionada / Como
  testar / Checklist do autor) e `Closes #N`.

## Controle de qualidade por MR

1. O autor roda o grep e o checklist do brief da sua parte.
2. Um revisor-agente lê o diff.
3. O outro humano aceita: é a validação por par do DoD Inteli.

Grep que precisa voltar vazio em `documents/` e `docs/`:

```
grep -rnE 'referral to in-house|not new spending|match to the cent on all|most payments settle|without competitive bidding|33rd Battalion|Comando Militar de Saúde|Person [0-9]|reviewed EDA|version 2' documents docs
```

## Quadro de estado

Cada agente atualiza só as próprias linhas.

| Id | Dono | Issue | Branch | MR | Estado |
|---|---|---|---|---|---|
| F0 | gui | — | — | — | aguardando consenso |
| R1 | danilo | | | | |
| R2 | danilo | | | | |
| R3 | gui | | | | |
| R4 | gui | | | | |
| R5 | gui | #33/#34 | (recriar) | | em andamento (thread de linguagem) |
