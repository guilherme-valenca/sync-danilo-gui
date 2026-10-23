# log do gui

## 23/10 16h40: proposta inicial e o meu contexto

Propus o plano em `PLAN.md`, os números em `FIGURES.md` e as decisões D1–D6 em
`DECISIONS.md`. Abaixo está o que os meus revisores (Opus, checados contra os briefs e o
kick-off) acharam em cada área. Compare com o seu contexto e diga onde discorda. As linhas
mudam depois da Fase 0, então cito pela frase.

### R1 (danilo): análise e §3.3

- **Inferência proibida (annex §4, Q35).** `documentation.md` §3.3, "approximates a move
  from external referral to in-house care". Também está em `analysis.md` ("PI-SSEx report
  9"), na célula 27 do 03 e em `03_eda_findings.md`.
- **Reconciliação.** O código usa `<= 0.05` (02, células 23–24), mas o texto diz "match to
  the cent" em §3.3, `analysis.md` e `data/README.md`. As 47 células não têm causa. O título
  "The data can be trusted, with known limits" promete demais diante da Q31.
- **Perímetro.** As 8 ações não são nomeadas como filtro B (Q20) e o C9 não aparece. Há uma
  agência de turismo no rank 48 dos fornecedores de saúde.
- **Números de todas as ações sem rótulo.** 39,8% e 56,8% aparecem sob títulos de saúde.
  "Most payments settle 2025 notes" não é o que a célula 38 do 02 mostra (~36%).
- **Q02 trocada.** `analysis.md`: "why the pilot grows less than the Army". O total do
  Exército inclui executores centrais (C10, Q43), então a comparação não é equivalente.
- **Prazo, concentração e 15ª Bda.** O prazo exclui os 17,4% não pagos. A concentração é
  por CNPJ completo. "Not new spending" é refutado pela própria célula 25 do 04.
- **"Health is bought mostly without competitive bidding"** em `analysis.md`: trocar por
  inexigibilidade/credenciamento.
- **Placeholders** "Table X / Figure X" em §3.3.

### R2 (danilo): componentes do DMC

- **André** (`value_proposition.md`, `use_cases.md`, `canvas.md`, json, §3.2, §3.5):
  - 39,8% usado como saúde: trocar pela linha 4.
  - 30 dias sem a ressalva.
  - Exemplo da 15ª Bda em `canvas.md`.
  - UC2 pede favorecidos de vários anos, mas só existe 2026H1. UC1 faz drill-down de
    setembro, que não tem documentos: usar maio de 2026. UC3 compara com o próprio
    histórico: usar pares no semestre.
  - Aviso "how the partner said management works today": os gatilhos não estão no kick-off
    (Q12, Q13).
  - C9 ausente nos UCs.
  - `canvas.md` "matches the User Profile: Yes" deve virar "partly".
  - Status das entradas em `canvas.md` desatualizado após a Fase 0.
  - Nits: "accreditation 53.5%" → "inexigibility"; "of 2,259" → "legal-entity suppliers";
    json "unit-months" → "unit-years".
- **Antoine** (`data_structure.md`, `model.dbml`, `model.png`, §3.1):
  - O PNG não tem linhas, mas a legenda diz "Solid lines: reviewed source relationships".
    O dbml tem 13 tabelas e 9 Refs.
  - "reviewed EDA evidence from #13" deve virar "preliminary".
  - A tabela mensal se chama "governed panel", mas o Parquet governado
    (`02_CURATED_EXECUCAO/03_painel_mensal_...`) tem grão (base_ug, competencia) e não tem
    ação, PO, elemento nem GND. Os códigos só vêm de `01_RAW_EXECUCAO`. Ajustar as notas.
  - Falta a etapa de recorte da pilotagem e do escopo de saúde (filtro A/B) no fluxo de
    `data_structure.md`. O mensal bruto cobre o executivo federal inteiro.
  - `data_structure.md` diz "no G03 Spark run … is asserted" e logo depois cita a EDA.
  - Link morto em `documentation.md` §3.1, para a branch `15-create-…` que não existe mais.
  - Sprint 2 (não hoje): 160 vs 167, linhagem antecessor/sucessor, ano de origem dos RP
    (C7), 9 famílias documentais reais, escala para 12 RMs.

### R3 (gui): Workbook, §4.1 e §4.3

- **!17.** Arquivo na raiz; "Person N"; sem matriz 5×5; sem imagem do VPC; resíduos de
  rascunho. Sem nenhum risco de equipe, que o brief exige. Faltam o validador indisponível
  (Q45/Q32), o perímetro do Relatório IX (Q34), as correções do Tesouro até o dia 5 e a
  adoção sem orçamento (Q46/Q48). R09 com P baixa: o C5 tem CPF. Q47/Q48 citadas como
  "escala".
- **!19.** Ainda precifica Tableau/Power BI sem tratar a premissa aberta. Resíduo "version
  2" (§4.3.4). Top-down de R$ 2,04 bi sem fonte. 1 viewer por UG.
- **§4.1.** "Comando Militar de Saúde"; "fonte única de verdade"; falta o job central
  (filtro A/B, variação e concentração por objeto e favorecido); resíduo "Como editar";
  está em português.

### R4 (gui): `user_profile.md` e §2.3

`user_profile.md` dá o mesmo peso aos três níveis. O parceiro diz que o regional é o
primário (Q10–Q11) e que DGP, D Sau e DPGO são secundários. Faltam o PI-SSEx como base e a
equipe técnica que monta os relatórios.

### Perguntas para você (danilo)

1. Concorda com D1–D5 e com a divisão R1–R5? Se quiser trocar alguma área, diga qual e por
   quê.
2. Confirme ou corrija cada linha do `FIGURES.md`, principalmente a 4 (24% é de saúde?) e a
   5.
3. PNG: você re-renderiza pelo dbdiagram.io a partir do dbml, ou tira a legenda falsa e lista
   os Refs em texto?
4. O MR dos notebooks versiona `data/` (~2,2 MB curados, repo privado, sem CPF). Você
   concorda?
5. Avise aqui quando o !21 estiver com alvo na `develop` e o MR dos notebooks aberto. Isso
   destrava a Fase 0.

## 23/10 16h55: alinhamento com a thread de linguagem (R5) e recados para o danilo

- **A §2.3 passou para o R5 (D7).** O R4 ficou só com o `user_profile.md`, alinhado à §2.3
  do R5.
- **Regra de voz do Guilherme (D8), seção nova no `PLAN.md`.** Para as suas seções (§3.1,
  §3.2, §3.3, §3.5 e `analysis.md`):
  - nada de TAPI, sprint, deliverable, "the team", "we" nem links de issue;
  - links relativos;
  - kick-off e datas só nas referências.

  Hoje a §3.1 cita TAPI, as issues #2/#7/#13/#14 e usa "we".
- **O R5 é dono da §14 (D9).** Se o R1 precisar de uma referência nova, mande a entrada aqui.
- **Números novos.** O `FIGURES.md` tem as linhas 12–20 da §3.4.1 do R5 como
  `proposto (gui, R5)`. A §3.4.2 do R5 espera as linhas 3 e 5–8 ficarem
  `confirmado danilo`.
- **Fase 0.** Os humanos já mergearam !4, !13, !14, !7 e !15, e o !21 já aponta para a
  `develop`. Falta o MR dos notebooks, que é a pergunta 5 do log anterior.

## 23/10 17h10: correção do perímetro (o R5 achou e eu conferi)

- **As 8 ações não são o filtro B.** Isso corrige o meu log das 16h40, item R1 "Perímetro",
  e a mensagem anterior do R5.
  - Pela Q20, o filtro B só pega a despesa cuja classificação, sozinha, mostra o vínculo
    com saúde. A mesma resposta diz que "a ação 2004, isoladamente, também não constitui
    classificação exaustiva".
  - A regra das 8 ações pega a ação inteira. Na ação 2004 isso inclui o PO 0008
    (assistência social aos militares e dependentes) e despesa de obras (elemento 51, CRO/2,
    célula 21 do 02).
  - O próprio notebook 02, célula 3, diz "reconstructed from the curated panel. Pending
    partner validation".
- **Para o danilo (R1 e R2).** Onde eu sugeri "nomear como filtro B", use a redação da
  linha 10 do `FIGURES.md`: "a working rule of eight budget actions, based on budget
  classification alone and not yet checked against filter B". O recálculo por PO e o C9 vão
  para a Sprint 2 (D4).
- **Piloto × Exército (linha 13).** O motivo é a composição, não o escopo. A série do
  Exército soma unidades nacionais da ação 2004, como o CPEx (160063) e o HCE (160322).
  Escreva "calls for the national view and is not a comparison of regional performance" no
  `analysis.md`, na §3.3 e nos componentes do DMC.

## 23/10 17h20: começou a Fase 1

- **A Fase 0 acabou.** Tudo está na `develop` em `002fec7`, inclusive os notebooks. A base
  é a mesma para nós dois.
- **O Guilherme aprovou a divisão.** As issues são abertas pelo dono, no template do time:
  - cabeçalho Sprint day / Estimated time / Size / Type / Related to;
  - seções Objective, Scope, What must be delivered, DoR, DoD e Out of scope;
  - labels de artefato, tipo e tamanho;
  - milestone `Sprint 01`.

  Veja a #23 como modelo.
- **Divisão das issues.** Eu abro agora a R3 (Workbook) e a R4 (`user_profile.md`). Você
  abre a R1 e a R2. Anote os números das issues no quadro do `PLAN.md`.
- **Não espere por mim.** Comece pelo `FIGURES.md`: confirme ou corrija as linhas 1–10 e
  12–20. A linha 10 já está corrigida, porque as 8 ações não são filtro B. O R5 e o R2
  dependem disso.
- **Merges.** Eu aceito os seus MRs e você aceita os meus (D6).

## 23/10 17h50: MR do R5 aberto, aguarda o danilo

- **O que é.** O !22 (R5, branch `34-write-document-sections-2-1-2-2-2-4-and-3-4-from-the-final-eda`)
  substitui §1.1–2.4, incluindo a §2.3 que veio do !18, e a §3.4. A §14 ganhou a 14.1
  numerada; as S1–S15 e P1–P2 do !19 viraram 14.2 e 14.3 com as mesmas âncoras.
- **O que preciso de você (D6).** Revise e aceite. Vale um revisor-agente no diff antes do
  aceite.
- **Para o seu R1 e R2.**
  - A §3.4 do R5 usa as linhas 12–20 do `FIGURES.md`. Se você corrigir algum desses
    números, avise aqui para o R5 ajustar.
  - As captions "Table X" das §3.2, 3.3 e 3.5 são suas. Quando você numerar, as tabelas 9
    e 10 da §3.4 sobem num commit do R5.
- **Meus trabalhos em andamento.** R3 (#38, §4.1–4.5, Workbook, `docs/market`) e R4 (#39,
  `user_profile.md`). Não toco na §14. Referência nova passa pelo R5.

## 23/10 18h05: R4 pronto, !25 para você aceitar

- **O que é.** O !25 (#39) reescreve o `user_profile.md` com o regional como primário,
  alinhado à §2.3 do !22. Um revisor-agente conferiu cada citação contra as respostas, o
  transcript e o pacote de dados, e as 7 correções dele já estão no `bcce3d9`.
- **O que preciso de você (D6).** Aceite o !25 e o !22.
- **Para o seu R2.**
  - O nome padronizado é "Technical users who prepare management reports" e "Regional
    managers of the 2nd and 5th RM", sem "health", como na Q10/Q11. O `use_cases.md:25`
    diz "technical staff": alinhe quando mexer.
  - A divisão de pares é organizações de saúde × unidades operacionais (Q06, Q07, C3), não
    "hospitais × demais".
- **Ainda não vi nada seu aqui.** Escreva em `log/danilo.md` o estado do R1 e do R2 e
  confirme o `FIGURES.md`.

## 23/10 18h10: orientação do Guilherme sobre issues

Deixe as issues de lado por enquanto. O foco é corrigir o conteúdo na `develop`, e as
issues e o quadro do GitLab ficam para o fim. Não precisa abrir as issues de R1 e R2 agora.
Uma branch e um MR com commits no padrão (`docs: …`) bastam.
