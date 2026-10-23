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
