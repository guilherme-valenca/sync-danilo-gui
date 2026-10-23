# Plano: fechar a Sprint 1

**Estado: Fase 0 concluída (23/10, 17h20). Fase 1 começou. Guilherme aprovou a divisão. O danilo dá ok ou contesta no `log/danilo.md`.**

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

**Progresso (23/10, 17h20):** concluída. Todos os MRs foram mergeados pelos humanos; os notebooks, o `analysis.md` e os `outputs/` estão na `develop`; o !16 foi fechado. Base da Fase 1 = `origin/develop` em `002fec7`.

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
| R4 | gui | Prioritise the regional managers in the User Profile | `user_profile.md`, alinhado à §2.3 do R5 |
| R5 | gui (thread de linguagem) | Issues #34 (fecha) e #33 (referencia) | `documentation.md` §1.1–1.3, §2.1–2.4, §3.4 e §14 References; no fim, o `README.md` do DMC |

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

## Voz da documentação (regra do Guilherme, vale para todas as seções e para o Workbook)

- O texto é a entrega de um contratado ao Exército e é tudo o que o leitor do Exército recebe.
- Nunca mencionar número de grupo, sprint, entrega/deliverable, TAPI, Inteli como relação
  de curso, "the team" nem links de issue.
- Kick-off e datas reais aparecem só na lista de referências (§14). Citação inline por
  Q-número é aceita.
- Escopo e objetivos aparecem como dados do projeto, não como "o parceiro definiu". Só a
  §2.2 fala das necessidades do parceiro.
- Sem travessões, sem dois-pontos no meio da frase, voz ativa.
- Links relativos. As URLs do GitLab contêm o nome do grupo.
- Exceção do Workbook: o brief exige um membro responsável por risco, então os nomes ficam
  como donos. O que se evita é a forma "the team".

## Dono da §14 References

É o R5. Ao recriar a branch a partir da `develop` pós-Fase 0, o R5 **mantém todas as
referências que já estiverem lá**, como as S1–S15 e P1–P2 do !19 (âncoras `#ref-s*` e
`#ref-p*`, que a §4.3 usa) e as que o R1 ou o R3 acrescentarem. Quem precisar de uma
referência nova manda a entrada pelo log.

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
| F0 | humanos | — | — | todos | concluída (`002fec7`) |
| R1 | danilo | | | | |
| R2 | danilo | | | | |
| R3 | gui | #38 | `38-consolidate-the-market-and-risk-analysis-workbook-at-docs-against-the-brief-and-the-partner-s-premises` | | Doing (worktree `g03-r3`) |
| R4 | gui | #39 | `39-prioritise-the-regional-managers-in-the-user-profile` | | Doing (worktree `g03-r4`) |
| R5 | gui (linguagem) | #34 fecha, #33 ref | `34-…` a criar pós-Fase 0 | | seções reescritas na worktree `g03-docs`, sem commit; 3ª revisão rodando (§2.3) |
