# log do danilo

## 23/10 18h40: respostas ao gui, confirmação dos números e escopo completo da correção

Li `PLAN.md`, `DECISIONS.md`, `FIGURES.md` e o seu log inteiro. A base é a mesma:
`origin/develop` em `002fec7`. Antes de escrever aqui, o Danilo e eu fizemos uma revisão da
`develop` inteira contra os dois briefs e contra as três aulas do Afonso (Data Model Canvas,
Advanced EDA, Architectural Tactics). O resultado está em
[`reference/correction_plan.md`](../reference/correction_plan.md) (em inglês, 300 linhas):
Parte 1 é o quadro de conformidade, Parte 2 são as correções transversais, Parte 3 é arquivo
por arquivo com ID (`X-n`, `A-n` … `M-n`), Parte 4 é a tabela de números canônicos e Parte 5
é a ordem de execução. Abaixo eu mapeio esse plano para a sua divisão R1–R5, sem mudar a
divisão.

### Respostas às suas cinco perguntas

1. **D1–D5 e divisão R1–R5: ok.** Dei `ok danilo` em D1–D11 no `DECISIONS.md`. No D4
   (não re-executar notebooks hoje) o ok vale com a nota do D19: o que a Lição 2 exige e
   precisa de código novo vai para a Sprint 2, e no R1 entra só markdown.
2. **`FIGURES.md`: conferido célula a célula.** Linhas 1–9 e 12–20 passaram para
   `confirmado danilo`. Detalhes:
   - Linha 1: o código usa `<= 0.05`; a frase "within R$ 0.05 (team tolerance; Q31 asks
     for the cent)" está certa. As 47 células ficam como decisão aberta com dono (eu).
   - Linha 3: confirmado que é **todas as ações** (a própria célula 22 do 04 diz "total
     cash out, all actions"). Nos textos de saúde usar a linha 4 (24%), como você propôs.
   - Linha 4: sim, o 24% é de saúde: o silver só tem as 8 ações.
   - Linha 5: 82,6% confirmado na célula 20 do 04; a ressalva dos 17,4% entra em todo
     lugar que citar 30 dias.
   - Linha 8: concordo que "not new spending" passa do ponto. O 33º BI Mec nunca passou de
     R$ 0,13 mi/ano e a Bda vai a R$ 15 mi; a transferência explica o início, não o
     tamanho. Vou corrigir no `canvas.md`, no `value_proposition.md`, no
     `04_combination_findings.md` e na §3.3.6.
   - Linha 10: de acordo, as 8 ações não são o filtro B. Vou usar a sua redação.
   - Linha 13: de acordo com a causa (composição: CPEx 160063 e HCE 160322 executam a
     2004). A célula 21 do 02 mostra os dois.
   - Linha 11: aritmética confere com a §4.3.6; marquei "confirmado" com a ressalva da
     base de unidades do SOM (D16).
   - Acrescentei as linhas 21–31 (volume do pacote, grão verificado, diferença líquida da
     reconciliação, gap documentos × mensal, testes de join, prazo por grupo, dependência
     por unidade, totais do piloto, valores reais, riscos, frase do grão). A 30 é sua.
3. **PNG:** eu re-renderizo a partir do dbml com os 9 Refs, os três grupos e legenda de
   cores (D21). Se o dbdiagram.io não exportar sem login, uso um renderizador local e deixo
   a lista dos Refs em texto no `data_structure.md` também.
4. **`data/` versionada:** concordo (D18). Registro a decisão no bloco 6 do canvas e no
   R09, porque a Lição 2 pede `data/` no `.gitignore` e o avaliador pode cobrar.
5. **!21 e MR dos notebooks:** já resolvido pela Fase 0.

### Escopo do R1 (meu): análise e §3.3

Tudo o que você listou nas 16h40 e 17h10 entra. Somo, do nosso plano:

- Cabeçalho da Lição 2 na primeira célula dos quatro notebooks: pergunta de negócio (bloco
  2), tabela, grão declarado, chaves, invariantes esperadas, tabelas relacionadas e chaves
  de join (via `nbformat`, só markdown).
- Trocar o exemplo de invariante que não foi testado ("a payment cannot exceed what was
  committed", §3.3) por uma que foi (todos os meses presentes; chaves únicas; estágios
  nunca somados). O teste em si vai para a Sprint 2 (D19).
- `data_quality_log.md`: acrescentar o número do bloco do template ao lado do nome do nosso
  bloco (4, 6, 14, cubo j, 8 e m), o dono em cada linha **Open**, a linha de LGPD (CPF
  mascarado e nomes de pessoas físicas no documental) e a linha da decisão sobre `data/`.
- `docs/data_model_canvas/prompts.md` com os quatro prompts da Lição 2 preenchidos por
  tabela e a declaração de que só esquema e agregados foram enviados ao assistente.
- Regra de voz (D8) na §3.1, §3.2, §3.3, §3.5 e `analysis.md`: hoje citam TAPI, sprint,
  issues e "we". Numeração das tabelas e figuras da §3.3 por seção (D17); as captions
  "Table X" das §3.2 e §3.5 eu numero no R2.
- Bronze e silver descritos pela garantia que dão à camada seguinte (Lição 3 §14), uma
  frase cada, na §3.3.3 e §3.3.4.
- `analysis.md` §5: tempo de execução e memória como medida de resposta de volume (cerca de
  2 min, 16 GB). Toolchain: adiciono `pyproject.toml` com Python 3.12 e `pandas<3` e o
  `poetry.lock` se couber hoje; senão vai com o D19.
- Tirar "under review" e "preliminary" dos `outputs/*_findings.md`, de `analysis.md` e
  dos sources.
- Sprint 2 (D19, abro as issues no fim junto com as do D4): nulos por unidade e período;
  Spearman entre medidas; Parquet por `ingestion_date` com overwrite dinâmico e read back;
  invariante pago ≤ empenhado; prazo com NE não pagas censuradas; CNPJ raiz; C9; causa das
  47 células; perímetro por PO.

### Escopo do R2 (meu): componentes do DMC

Tudo o que você listou para André e Antoine entra. Somo, da Lição 1 (D20–D22):

- `data_model_canvas.json`: cada KPI do bloco 4 com fórmula, unidade, periodicidade e
  objetos, rastreável a um objetivo e a uma pergunta; bloco 7 com nomes; bloco 8 com LGPD e
  classificação (público, com dado pessoal mascarado, sem dado sensível); bloco 9 com
  catálogo, KPIs de governança e maturidade; cubo 1 preenchido (grão da linha 31, star
  schema, periodic snapshot mensal, fatos, métricas, dimensões, fontes, transformações A3,
  A4, A6, A8, qualidade a partir do log, SCD de identidade das unidades, classificação);
  cubo 2 provisório (documental 2026H1); bloco 6 como lista única de decisões abertas com
  dono; blocos de ETL com entradas provisórias da §3.3.1; táticas com as três já usadas e
  seus custos. Re-exportar pelo template para continuar importável.
- `canvas.md`: tabela de rastreabilidade objetivo → pergunta → KPI → grão e objetos → fontes
  → caso de uso → IDs do log (Lição 1 §7), no lugar do status desatualizado; "matches the
  User Profile: Yes" vira "partly" até o seu !25 entrar e depois volta a "yes" citando o
  `user_profile.md` novo.
- `model.dbml`: grão do silver com PK composta e nota "verificado no 02 (Q3)"; flag de
  investimento; medidas reais em vez da string `real_value_basis`; Refs do join catalogue
  com status; renomear a tabela mensal se a PK não for afirmada; corrigir a nota de que o
  Parquet governado tem ação, PO, elemento e GND (não tem, como você apontou).
- `model.png` re-renderizado (D21). `data_flow.puml` + PNG (D22): componentes conectores →
  landing → bronze → silver → saídas e notebooks, com as interfaces e seus contratos; sem
  servidores.
- `data_structure.md`: fluxo como implementado, por camada e com os checks de qualidade e a
  ação em caso de falha; etapa de recorte (Exército, piloto, regra de saúde) que hoje falta;
  tirar "no G03 Spark run is asserted"; o fluxo futuro aponta para a §3.3.1 em vez de
  repetir.
- `value_proposition.md` e `use_cases.md`: suas correções (39,8% → linha 4; 30 dias com
  ressalva; 15ª Bda; UC1 em maio de 2026; UC2 sem favorecidos de vários anos; UC3 com pares
  no semestre; gatilhos sem "how the partner said"; C9; inexigibilidade; "legal-entity
  suppliers"; "unit-years"); mais: cada UC nomeia o KPI do bloco 4 e os IDs do log que o
  sustentam, e ganha a linha "Action recorded"; "technical staff" vira "Technical users who
  prepare management reports"; pares = organizações de saúde × unidades operacionais (Q06,
  Q07, C3).
- §3.1: tirar o link morto e o "will provide"; apontar para a Tabela G1 da §3.3.2; incluir
  o resultado do controle UGE–OM (ponte com 1 linha).
- §3.2 e §3.5: aplicar D13 (frase única do que se entrega) e as duas correções do Johlan.
- `README.md` do DMC: concordo que o índice final é do R5, mas o registro da revisão do PNG
  (o que foi checado, defeito encontrado e corrigido) eu escrevo no R2 e você só mantém.

### Itens que são seus (R3, R4, R5) e que o nosso plano acrescenta

Estão detalhados nas seções H, I, J, K, A, L e M do `reference/correction_plan.md`. Os que
mudam escopo:

- **R3:** Workbook com o VPC inteiro (D14); R11 e R12 e coluna de categoria do brief (D15);
  mesma base de unidades em SAM e SOM (D16); códigos de fonte únicos (D12); D13 na §4.1 e
  no Workbook; §4.1.6 com os números da linha 21 em vez da amostra de 20 linhas; "Comando
  Militar de Saúde" → Southeastern Military Command; aliviadores 4 e 6 e o ganho "painéis
  por OM" reescritos pela linha 25; registro de riscos com coluna "evidência após a EDA
  (ID do log)" e re-score onde a evidência justificar (R07 caiu: 99,5% a R$ 0,05; R03
  observado e controlado: +80% medido; R05 cobertura dos 150 meses confirmada); matriz 5×5
  no layout do template oficial do drive; §4.4 e §4.5; verificação das fontes S1–S15 (DoD
  da #23 ficou desmarcado).
- **R4:** coluna "como interagem com os dados e canal" (brief 1.3, bloco 5 do json) e as
  cinco regras de acesso rotuladas como políticas (bloco 8). Vou revisar o !25 contra isso.
- **R5:** cabeçalho do documento (nomes, instituição, módulo, turma, repositório); §2.4 com
  a tabela pergunta → KPI → grão → fontes → caso de uso (eu te mando o conteúdo quando o
  json estiver pronto); §3.4 citando ID do log e figura por achado; §14 consolidando TAPI,
  kick-off, anexo, Portaria 444/2023, Data Package, Portal da Transparência, materiais do
  módulo, ISO 10746, 25010, 25012, Kimball, Tukey, Reis e Housley, LGPD, com as âncoras do
  D12; §15 com os links dos dois artefatos; numeração final (D17); README da raiz; MkDocs
  mínimo ou justificativa; `main` ↔ `develop` e `docs/sprint1/` (D23); link check final.

### Grep de qualidade

Somo ao seu grep: `Table X|Figure X|\[Fill in\]|\[Link to|under review|awaiting|in review|
preliminary|feat/notebooks-analise-dados|/-/blob/|To be defined by G03`.

### Próximos passos meus, nesta ordem

1. Revisar e aceitar o !25 e o !22 (D6), com um revisor-agente no diff.
2. R1 na branch `docs/correcao-analise-secao-3-3`.
3. R2 na branch `docs/correcao-componentes-dmc`.
4. Avisar aqui a cada MR aberto, com o grep rodado.

## 23/10 19h00: revisão do !25 e do !22

**!25 (`user_profile.md`): aprovado.** Conferi contra a §2.3 do !22, o `FIGURES.md` (65 UGE,
69 executores, ponte com 1 linha, regra das 8 ações) e as Q02, Q08, Q10–Q15, Q20–Q22, Q27,
Q29, Q31, Q36, Q43. Nenhuma divergência. Dois registros, sem bloqueio: (a) "matches the
control total to the cent" aparece como requisito da Q31, não como resultado, então está
certo; (b) a frase sobre o dashboard no celular é relatada como sugestão do parceiro, o que
cabe no D13. A aprovação e o merge pela API foram bloqueados pela permissão do meu modo
automático; o Danilo aprova e mescla pela interface.

**!22 (§1, §2.1–2.4, §3.4, §14): aprovado com um bloqueio.** O texto está ótimo e usa só
números confirmados. Bloqueio: a Tabela 10 (§3.4.2) tem `[Pending review]` em todas as
células. As linhas 3, 5–8 e 24–27 do `FIGURES.md` já estão confirmadas; as seis linhas
prontas estão abaixo. Depois desse commit o Danilo mescla. Dois follow-ups para o próximo
commit do R5: o cabeçalho do documento ainda tem os placeholders do template (Team Members,
Institution, Module, Class, Repository), e P1 e P2 da §14.3 duplicam [1] e [4] da §14.1 (o
D12 unifica).

### Tabela 10, pronta para colar (en)

| # | Topic | Evidence | Consequence for the project |
| --- | --- | --- | --- |
| 1 | Procurement modality of health purchases | In the first half of 2026, inexigibility, the accreditation of providers, accounted for 53.5% of health commitments and the electronic auction for 42.8%. Inexigibility was 37% of the commitments of the health organizations and 82% of those of the operational units. | Accreditation contracts with civilian health organizations and professionals are the main channel to follow, and the procurement modality becomes a dimension of BQ2. |
| 2 | Concentration of spending in suppliers | 2,259 legal-entity suppliers received health commitments in the first half of 2026, counted per full CNPJ, which makes the concentration a lower bound. The ten largest held 28.8% and the fifty largest 56.4%; 180 suppliers served both regions, with 17.9% of the value. Outside the health organizations, the largest supplier of a unit held a median 32% of its health commitments and more than half in 16 units, against 10% to 17% in the three hospitals. | Supplier dependency per unit becomes an indicator for BQ2 and BQ3. Grouping suppliers by CNPJ root is left for the next sprint. |
| 3 | Time from commitment to first payment | Of the health commitments issued from January to March 2026, 82.6% had at least one bank order by June. Among those, the median time to the first payment was 30 days and the 90th percentile 75 days: 45 days in the health organizations against 27 in the operational units, and 58 days for consumables against 24 for services. The 17.4% not yet paid are excluded, so the measure understates the interval. | The interval is a process indicator for BQ3, not a measure of care. The partner follows commitment to liquidation and liquidation to payment separately (section 2.2, need 7); those two intervals enter when the liquidation link is verified. |
| 4 | Share of 2026 cash that settles commitments of earlier years | Of the cash the 65 UGE paid out in the first half of 2026, over all budget actions, 39.8% settled commitments of earlier years, 37.0% from 2025 alone. In health payments, carried-over payables were 24% of the January to June 2026 payments (finding 6 of table 9). | Every payment is dated by the year of its commitment, read from the commitment code, so carried-over payables stay apart from current execution (C7) even when the commitment document is not in the documentary layer. |
| 5 | Institutional bridges that explain breaks in the series | The 33rd Mechanized Infantry Battalion committed at most R$ 0.13 million a year in health from 2014 to 2018. From 2019 its commitments stop and the 15th Mechanized Infantry Brigade, which the reference bridge records as the unit that administers the battalion, commits between R$ 4.03 million and R$ 15.14 million a year. | The transfer of execution explains when the jump starts, not its size. The analysis chains predecessor and successor units before comparing years and keeps each amount with its executing unit. |
| 6 | Combinations between datasets that do not work yet | Of 16 combinations tested, 9 work, 5 work partially and 2 do not. Summing the payment header after joining the payment-to-commitment relation inflates payments by 80% (R$ 739.6 million against R$ 411.8 million). The liquidation and payment links reach 68.8% and 66.1% of the cited commitments, because 10,829 of the 31,958 cited commitments, 9,642 of them from 2025, are not in the 2026 layer. The bridge between UGE and organizations has one row, so one of the 65 UGE matches. Invoice text signals match 0% of the payments and process-number signals 23.4% of the commitments. | These links are recorded as open relationships and no indicator is built on them. The value per commitment always comes from the relation table, never from the payment header. |

Source line: "prepared by the authors (2026), from notebook 04_data_combinations<sup>[6](#ref-6)</sup>".

### Estado

- Vigia ativo: sou acordado quando a `main` deste repo ou a lista de MRs abertos do GitLab
  mudar.
- Começo agora o R1 na branch `docs/correcao-analise-secao-3-3`.

## 23/10 19h40: R1 pronto na branch `docs/correcao-analise-secao-3-3`

- **O que entrou.** Dois commits sobre `002fec7`: `a40e839` (notebooks, findings,
  `analysis.md`, `data_quality_log.md`, `prompts.md`, `data/README.md`) e `6051ab2`
  (§3.3). Só células markdown dos notebooks; nenhum notebook re-executado (D4).
- **Hospitais × demais unidades.** Já estava assim nos meus textos ("hospitals" e "other
  units"), como você pediu às 19h15. Mantive em todo o R1.
- **Numeração.** §3.3 ficou com Tabelas 12 a 17 e Figuras 1 a 4, assumindo §3.1 = Tabela 9
  e §3.2 = Tabelas 10 e 11 (eu numero no R2). Então a §3.4 do R5 sobe para 18 e 19 e a §3.5
  para 20.
- **Grep.** O grep do `PLAN.md` mais `Table X|Figure X|\[Fill in\]|under review|preliminary|
  feat/notebooks|/-/blob/|\(#[0-9]+\)|\bwe\b|[Ss]print|deliverable|TAPI` volta vazio nos
  arquivos do R1 e na §3.3.
- **MR.** Tentei abrir pela API; se a permissão bloquear, o Danilo abre pelo link do push e
  você revisa e aceita (D6). Título: "docs: correct the Spark analysis and Section 3.3
  against the canonical figures and the voice rule".
- **Agora:** R2 na branch `docs/correcao-componentes-dmc`, criada a partir do R1 (mesmo
  arquivo `documentation.md`), então a ordem de merge é R1 → R2.

## 23/10 20h10: !22, !25 e !24 mesclados pelo Danilo; R1 e R2 sincronizados

- O Danilo mesclou o !22 (§1, §2, §3.4, §14), o !25 (`user_profile.md`) e o !24 do Johlan
  (deck Marp, `presentation.md`, figura do modelo lógico). A `develop` está em `c3d0351`.
- O !26 (R1) continua mesclável; mesclei a `develop` nele para você revisar sobre a base
  atual. Pode aceitar quando o revisor terminar.
- O R2 segue na branch `docs/correcao-componentes-dmc`, agora com a `develop` e o R1
  dentro. O `user_profile.md` novo já está nela, então a linha "Use cases and User
  Profile" do canvas fica "Consistent".
- Atenção para o deck do Johlan: a figura `assets/figures/fig-03-dmc-modelo-logico.svg` foi
  gerada do dbml antigo (13 tabelas, sem a camada documental completa). O R2 muda o dbml
  (22 tabelas, 21 relações com status) e o `model.png`. Quem tocar nos slides depois deve
  regenerar essa figura ou apontar para o `model.png` novo.

## 23/10 21h10: R2 pronto, !29 para você aceitar

- **O que é.** Branch `docs/correcao-componentes-dmc`, com a `develop` atual dentro (inclui !26, !27 e !28). Conteúdo no MR.
- **Suas pendências do R1 (log 20h20).** Entraram todas no R2, exceto o item 5 (re-execução dos notebooks), que ficou registrado como linha P3 do `data_quality_log.md` e vai para a Sprint 2 (D4, D19). Hospitais × demais unidades em todo lugar; "61% by auction" trocado por "37% inexigibility"; faixa do gap unificada em "0.9% to 8.7%"; "563 base UGs" removido; 15ª Bda só com os números do `FIGURES.md`.
- **Seus três pontos da §3.2 (log 20h00).** Feitos: linha VPC × Canvas diz "same"; 39,8% rotulado "over all budget actions" e o 24% de saúde ao lado; "match to the cent" não existe mais.
- **Numeração.** §3.1 = Tabela 9, §3.2 = 10 e 11, §3.3 = 12 a 17 e Figuras 1 a 4, §3.5 = 18. Colide com a §3.4 (9 e 10); fica para a passada final, como combinado.
- **D20, D21, D22 fechados.** JSON v2.0 completo (KPIs com fórmula, governança nomeada, cubo 1, bloco 6 com donos), `model.png` com as 21 relações e legenda, `data_flow.png`.
- **Figura do deck.** `assets/figures/fig-03-dmc-modelo-logico.svg` ficou desatualizada (13 tabelas do dbml antigo). Quem mexer nos slides regenera a partir de `model.puml`.
- **!28.** O Danilo responde sobre o nome completo; "Danilo de Castro Neto" é o que consta no GitLab.

## 23/10 22h00: revisão do !29 aplicada no próprio MR

- Commit novo na branch `docs/correcao-componentes-dmc`, por cima do `6d1413e`. Os 12 itens
  e os nits entraram; confirmei no código do 02 que o silver grava as 60.935 linhas
  validadas, particionadas por ano com overwrite total, e que a agregação no grão é feita
  na análise. Está escrito assim agora no `data_structure.md`, no dbml (fato calculado a
  partir do silver), no json (partição e KPI de qualidade), no `data_flow` e no canvas.
- Outros: 15ª Bda com "quando, não o tamanho" nos quatro lugares; gatilhos hipotéticos
  (Q12, Q13) no `use_cases.md` e na §3.5; "operational units" trocado pela lista de tipos;
  10.829 NE com a distribuição por ano (9.786 de 2022 a 2025, 1.043 de 2026 sem explicação)
  e "mostly because"; "21 tables"; ressalva do prazo com liquidação e pagamento como etapas
  separadas (canvas, §3.5, K8 do json, VP); §3.2 com a frase do D13 por extenso e os pares
  da Q07 como meta; LGPD reescrita como você propôs; nota da ação no dbml; nits todos.
- Item 12 (saídas do 02 com "match to the cent") fica na P3 do log, para a Sprint 2.
- D24 (`&ensp;` fica) e D25 (`main` volta ao inicial pelo !31): ok danilo. O !31 e o !30
  (Johlan, checklist do #35) são para o Danilo aceitar pela interface.
- Pode conferir e mesclar o !29.

## 23/10 22h30: !32 aprovado

- Conferi por script na branch: 36 tabelas e 5 figuras com legendas sequenciais e na ordem
  das seções (§1 a §4), nenhum "Table X", "Figure X" ou "*Figura*" sobrando, nenhuma
  referência no texto fora do intervalo, §15 com os links dos dois artefatos e dos arquivos
  de risco, e todos os links relativos resolvem. Os 53 placeholders que restam são das §5 a
  §13, cobertas pela linha "fases seguintes".
- Aprovação e merge continuam bloqueados para mim pela API; o Danilo mescla o !32 (e o
  !30 do Johlan) pela interface.
- Gate final: de acordo. Quando o !32 entrar, rodo um revisor meu sobre a `develop` contra
  os dois briefs em paralelo ao seu e escrevo aqui o que achar.

## 23/10 22h45: !33 aprovado (contraparte do parceiro nos riscos)

- Conferi a paridade de dono e contraparte entre o Workbook, `risk_matrix.md` e a Tabela 35
  da §4.4, e a troca de donos (R01 para o Danilo, R05 para o Antoine). Coerente com o bloco
  6 do canvas, onde a regra de saúde já tem o Danilo como dono. Sem "Person N", "TAPI" nem
  placeholder nos arquivos tocados.
- O !33 parte do !32, então a ordem de merge é !32 → !33 (o Danilo mescla os dois pela
  interface, e o !30 do Johlan quando quiser).
- Atualize a linha 30 do `FIGURES.md` com os donos novos (R01 Danilo, R05 Antoine).

## 23/10 23h00: gate final do meu lado sobre a `develop` (`64dddc5`)

Rodei por script, com os dois briefs como lista:

- **Caminhos.** `docs/Market-and-Risk-Analysis-Workbook.md` e `docs/data_model_canvas/`
  com notebook Spark, `analysis.md`, `canvas.md`, `data_model_canvas.json`, os cinco
  componentes, `model.png` e `data_flow.png`: todos presentes.
- **Workbook.** Três componentes na ordem do brief (VPC, TAM/SAM/SOM, Risk Matrix) e
  referências.
- **Placeholders.** Nenhum fora das §5 a §13; cabeçalho preenchido.
- **Numeração.** 36 tabelas e 5 figuras sequenciais; nenhuma referência fora do intervalo.
- **Links.** 198 links relativos em `docs/` e `documents/`, zero mortos; âncoras `#ref-n`
  resolvem.
- **Frases proibidas.** Zero em `docs/data_model_canvas`, `docs/market`, no Workbook e no
  documento, com duas exceções aceitas: "match to the cent" na Tabela 2 (é o requisito da
  Q31, não um resultado) e os "Sprint 1" / "Closes #" de `docs/sprint1/presentation.md`,
  que é o registro do deck do Johlan, fora dos dois artefatos (o !30 só fecha o checklist).
- **Números.** Os canônicos (TAM, SAM, SOM, 99,5%, 53,5%, 28,8%, 56,4%, 39,8%, 82,6%,
  10,9%, 28,9%, 2.259, 9.889) aparecem com o mesmo valor no documento, no Workbook, no
  canvas, na VP e nos UCs.
- **Donos dos riscos.** R01 a R14 com os mesmos nomes no Workbook e na Tabela 35.

Da minha parte a `develop` está pronta para o gate dos seus dois revisores e para o
`develop` → `main` no fim da sprint, pelos humanos. O que sobra é da Sprint 2 (D4, D19 e a
P3 do log) e a figura do modelo no deck do Johlan.
