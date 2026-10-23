# Sprint 01: general correction plan for `develop`

**Snapshot:** `origin/develop` at commit `002fec7` (2026-10-23, after the merge of !4, !7, !11, !13, !14, !15, !17, !18, !19, !20, !21).
**Purpose:** list everything that must be corrected, completed or reconciled on `develop` so that (1) every part meets the two official briefs (Data Model Canvas, in [artifact.md](artifact.md); Market and Risk Analysis Workbook, in [artifact_workbook.md](artifact_workbook.md)), (2) every part applies the concepts of Prof. Afonso's Lessons 1, 2 and 3, and (3) no section contradicts another and no section is left discontinuous (placeholder, stale status, dead link, number that differs from its source).
**How to use:** Part 1 is the reference frame. Part 2 lists the cross cutting corrections (they touch several files; do them first or in the same MR as the file they touch). Part 3 goes file by file. Part 4 is the table of canonical numbers and wording that every section must use. Part 5 is the execution order. Each item has an ID (`X-n`), the file, what is wrong today, what to do, the basis (brief or lesson) and the owner by role (the Sprint 1 role division in [roles.md](roles.md) is kept as is).

---

## Part 1. Reference frame: what has to be true at the end

### 1.1 Data Model Canvas brief (weight 4)

| Requirement | Where it must be satisfied | State on `develop` |
| --- | --- | --- |
| Deliverables under `/docs/data_model_canvas/`: `.ipynb` with Spark, Markdown doc of approach, assumptions and results, the Canvas with all components | `docs/data_model_canvas/` | Present (4 notebooks, `analysis.md`, `canvas.md`, `data_model_canvas.json`) |
| 1.1 Value Proposition aligned with partner needs and supported by analysis insights | `value_proposition.md`, `canvas.md`, Section 3.2 | Present; stale "under review" wording; conflicts with VPC 4.1 (see H) |
| 1.2 Data Structure: collection, storage, use, sources, formats; **high level data architecture diagram (dbdiagram.io or equivalent)**; how data flows to support the value | `data_structure.md`, `model.dbml`, `model.png` | `model.png` has **no relationship lines**; no data flow diagram; text still says "no Spark run is asserted here" |
| 1.3 User Profile: end users, needs, how they interact with data | `user_profile.md`, Section 2.3 | Section 2.3 says regional managers are primary; `user_profile.md` still treats the three perspectives as equal |
| 1.4 Data Analysis: comprehensive Spark notebook, new ideas and data combinations, well structured, justified, results feed the Canvas | notebooks 01 to 04, `analysis.md`, `data_quality_log.md`, Section 3.3 | Present; first cells lack the Lesson 2 "question, grain, invariants" header; `Table X` placeholders |
| 1.5 Use Cases: practical scenarios, storytelling, insights turned into actions | `use_cases.md`, Section 3.5 | Present; stale references; two wording errors flagged in review and not applied |
| Completeness: all components integrated into one coherent Canvas | `canvas.md`, `data_model_canvas.json`, Section 3.2 | JSON has KPIs without formula/unit/periodicity, governance roles "to be defined", cube 1 empty, open decisions without owner |

### 1.2 Market and Risk Analysis Workbook brief (weight 3)

| Requirement | Where it must be satisfied | State on `develop` |
| --- | --- | --- |
| File at **`/docs/Market-and-Risk-Analysis-Workbook.md`** | `docs/` | File is at the **repository root** (`Market-and-Risk-Analysis-Workbook.md`) |
| 1. VPC with all sections filled, explicit problem solution fit | Workbook §2, Section 4.1 | 4.1 complete but in Portuguese and with evidence from an early 20 line sample; Workbook has a 3 row summary only |
| 2. TAM, SAM, SOM consistent, data backed, with segmentation logic and competitive justification | Workbook §3, Section 4.3 | Present and consistent with 4.3; source codes differ (G1 to G9 vs S1 to S15); SAM and SOM use different unit definitions (156 UG vs 65 UGE) |
| 3. Risk Matrix with the official template, at least 10 risks covering **team, technology, complexity, operational**, owner per risk, position by probability and impact, realistic mitigation, partner oriented | Workbook §4, `docs/market/risk_matrix.md`, `docs/market/risk_mitigation.md`, Section 4.4 | 10 risks, scored and mitigated; **no team risk**; owners are "Person N" instead of names; Section 4.4 is `[Fill in]`; 4.5 is `[Link to Workbook]` |

### 1.3 Lesson 1 (Data Model Canvas, RM-ODP enterprise and information viewpoints)

* Model the problem before the data: community, decision maker, decision, frequency, policies (blocks 1 to 3).
* Objectives verifiable; each objective reaches a KPI; each KPI has **formula, unit and periodicity** and refers to information objects found in the data.
* Each analytical question is supported by at least one table or recorded as a risk in block 6; open decisions written as a question **with an owner**.
* Governance blocks 7 to 9 not left empty: owner, steward, custodian, technical lead named; LGPD classification of personal and sensitive data.
* **Grain of the first cube stated in one sentence and checked with a query**; first cube (blocks a to f) written in Sprint 1.
* Correspondence chain objective → question → KPI → grain and objects → source tables, readable in both directions (traceability).
* Orphan rows, null rates and invariant violations recorded with volume.
* ETL and tactics blocks only provisional and marked as such.
* Canvas exported as JSON and committed under `/docs/data_model_canvas/`.
* The VPC customers are the community of the enterprise viewpoint and their decisions are the analytical questions of block 2 (the two deliverables must be derived from the same description of the partner).
* Toolchain: Python 3.12, Java 17, Poetry, Docker, MkDocs.

### 1.4 Lesson 2 (Advanced EDA)

* Eight steps in fixed order: 1 start from the canvas (markdown cell with question, grain, invariants), 2 inventory, 3 grain, 4 completeness (null rates by column **and by dimension or period**), 5 univariate profile (summary, cardinality, IQR outliers), 6 relationships (time, categories, rank correlation between measures), 7 consistency across tables (orphans, invariants), 8 record and decide.
* Nothing is corrected, imputed or deleted during exploration.
* Data quality log with `ID | Table | Check | Finding and volume | Probable cause | Decision | Canvas block`, next to the canvas; findings without a decision go to block 6 with an owner.
* Every chart kept supports a sentence in the log or the canvas.
* Sample stored in the raw zone as Parquet, partitioned by `ingestion_date`, with an **idempotent write** (dynamic partition overwrite), read back and compared.
* Partner extracts not committed; `data/` in `.gitignore`.
* AI assistant: only schema and aggregates sent; prompts saved in `/docs/data_model_canvas/prompts.md`.
* `pyproject.toml` with `requires-python` pinned to 3.12 and `pandas<3`, committed `poetry.lock`.

### 1.5 Lesson 3 (Architectural tactics, medallion, component diagrams)

Not a Sprint 1 graded deliverable by itself, but it governs how the Data Structure block and Section 3.3 describe the flow:

* Each medallion layer defined by the **guarantee it gives to the next** (Bronze: kept as received with provenance; Silver: declared grain without duplicates, types fixed, invariants enforced, sensitive fields treated; Gold: indicators with the formula of block 4).
* Quality checks placed per layer with an action on failure.
* Data flow drawn as a **component diagram** (functions and interfaces, no servers), ideally PlantUML versioned in the repo; text explains components in the same order as the diagram.
* The five Vs written as requirements with a response measure, and tactics stated **with their cost** (partitioning, idempotent reruns, decoupling through layers, quarantine, schema contracts).

---

## Part 2. Cross cutting corrections (do first)

**X-1. Move the Workbook to the required path.** `git mv Market-and-Risk-Analysis-Workbook.md docs/Market-and-Risk-Analysis-Workbook.md`; update every link (Section 4.5, Workbook §5, risk files, `tmp`). Basis: Workbook brief ("must be delivered as `/docs/Market-and-Risk-Analysis-Workbook.md`"), Lesson 1 §11. Owner: Mélina (#22). Branch `38-consolidate-the-market-and-risk-analysis-workbook-at-docs-...` already exists on the remote; finish it there.

**X-2. One language for the project document.** `documents/documentation.md` is in English except Section 4.1 (Portuguese, including headings "Visão geral", "Perfil do cliente"). Translate 4.1 to English (keep Portuguese terms in italics where they are domain terms: *empenho*, *restos a pagar*). The Workbook, canvas and risk files are already in English. Owner: Leticia (#23).

**X-3. Remove every placeholder from the project document.** Still `[Fill in]` or template text: Team Members list, Institution, Module, Class, Repository (header); 1.1, 1.2, 1.3; 2.1, 2.2, 2.4; 3.4; 4.4; 4.5 (`[Link to Workbook]`); 15 (`[Links to Files]`, add at least the links to the two artifacts). Sections 5 to 13 are later sprints and may stay as placeholders, but say so once at the top of the document ("Sections 5 to 13 are filled in Sprints 2 to 5"). Owners: Gui (1, 2.1, 2.2, 2.4, 3.4), Mélina (4.4, 4.5), Johlan (header, 15).

**X-4. One formatting convention and real numbering.** Today three conventions coexist: Section 4.1 (plain Markdown table, italic caption `*Figura: ...*`), Sections 3.2, 3.3, 3.5 (`<div align="center">`, `<p>Table X - ...</p>`, `&ensp;` indent, `<p>Source: ...</p>`), Sections 2.3, 3.1, 4.2, 4.3 (plain tables, no captions). Placeholders to replace: `Table X` (3 in 3.2, 1 in 3.5), `Table X0`, `Table X0.1`, `Table X` (3.3.3), `Table G1`, `Table Y`, `Table D1`, `Figure X1` to `Figure X4`. Decide one convention (the `<div align="center">` + `<p>Table n</p>` + `<p>Source</p>` one is the majority and matches the style guide of #3), apply it to every table and figure, and number sequentially (Table 1…, Figure 1…). Drop `&ensp;` (it does not indent in GitLab Markdown). Owner: Johlan (#30), after every section is final.

**X-5. Remove stale "in review / pending merge" wording everywhere.** All MRs are merged, so the following must be rewritten as final statements:

* `canvas.md`: paragraph "Status of the inputs on 23/10" (talks about !7, !18, `feat/notebooks-analise-dados` waiting for review), and the closing sentence "resolve once the notebook branch is merged".
* `value_proposition.md`: "Preliminary results … still under peer review"; Sources: "branch `feat/notebooks-analise-dados`, under review".
* `use_cases.md`: "the detailed persona will come from the User Profile (#15)"; "exact files and columns will be confirmed against the Data Structure (#9)"; Sources "under review"; every "(preliminary)" tag in the evidence boxes.
* `documents/documentation.md` 3.2: "Consistent once the #26 update of the model (!18, in review) is merged"; "The figures from the data analysis are preliminary until the notebooks are reviewed".
* `documents/documentation.md` 3.1: "no repository notebook generated them. Issues #2, #7, #13 and #14 will provide the reproducible Spark notebooks"; "We have not independently inspected all monthly ZIPs … run Spark reconciliation"; link to `model.dbml` on the deleted #15 branch.
* `data_structure.md`: "It did **not** independently download and parse all 150 financial ZIPs … no G03 Spark run or financial reconciliation is asserted here"; "Spark implementation belongs to the notebook issues"; "proposed landing area … not an implemented or tested infrastructure claim".
* `docs/data_model_canvas/README.md`: every row links to branch URLs (`26-data-structure-eda-final`, `feat/notebooks-analise-dados`, `20-refine-…`) and says "awaiting review"; the "Final review still required" list is done.
* `docs/market/risk_matrix.md`: "D3 (#28) mitigation plans are not included in this version"; "pending team review".
* `docs/market/risk_mitigation.md`: "Baseline: … on the D2 branch … Since #12/#18 may not yet be merged"; "Leticia reports … must be checked before asserting" (now checked by the notebooks, see J-4).
* Workbook: "Status: Consolidated draft for peer review"; "Do not claim Issue #17 is merged without checking GitLab"; "`docs/market/market_sizing.md` … verify branch/merge status"; "`risk_mitigation.md` if merged there"; §6 unchecked peer review checklist.

What stays: the facts that are genuinely open with the partner (health rule, UGE–OM bridge, 2026 IPCA, the 47 residual cells), each written once as an open decision with an owner (see D-4).

**X-6. Source code collision between the market and the risk files.** Section 14 uses `S1` = ANS, `S2` = Futuro da Saúde, `S3` = FGVcia. `risk_matrix.md`, `risk_mitigation.md` and (through them) the future Section 4.4 use `S1` = TAPI, `S2` = kick-off answers, `S3` = indicators annex. The Workbook uses yet another set (`G1` to `G9`). When Section 4.4 and the consolidated Section 14 are written the codes will clash. Decide one scheme now: keep `S1` to `S15` for the public market sources, add `P1` TAPI, `P2` kick-off answers (already `P1`/`P2` in Section 14 but with P1 = answers and P2 = transcript), `P3` indicators annex, `P4` kick-off transcript, `P5` Data Package README, `P6` Portaria DGP/C Ex 444/2023, and renumber the risk files and the Workbook to the same codes. Owner: Johlan (#30) defines the scheme; Mélina and Leticia apply it to their files.

**X-7. One wording for what the solution delivers (no "dashboard" contradiction).** The TAPI says the partner wants a reproducible, auditable pipeline with validated descriptive analyses, not a dashboard; the DMC JSON (block 5) says "a production dashboard is not required"; `canvas.md` says the Canvas "keeps to comparisons between peer units"; but Section 4.1 lists "Painel analítico de execução" and "Painéis por região, OM e função/subfunção" as products and gains, the Workbook VPC says "accessible dashboards", and 3.2 only notes the contradiction instead of resolving it. Adopt one wording everywhere: *"analytical outputs (infographic sets A and B, reproducible notebooks and documented tables) that can later feed a dashboard"*, and apply it in 4.1, the Workbook §2, `value_proposition.md`, `data_model_canvas.json` block 5 and the 3.2 consistency row. Owners: Leticia (4.1), Mélina (Workbook), Andre (canvas files).

**X-8. One expansion of CMSE.** Section 4.1.3 says "gestores do Comando Militar de **Saúde** (CMSE)". CMSE is the Southeastern Military Command (Comando Militar do Sudeste). Fix in 4.1 and check the Workbook and slides. Owner: Leticia.

**X-9. Every number traces to one source.** Part 4 lists the canonical values. Sections that still carry figures from the early 20 line samples (4.1.6: "79.180 linhas", "amostras documentais têm só 20 linhas", "144 competências") must be replaced by the notebook figures. Owner: Leticia for 4.1; Johlan checks the whole document in #30.

**X-10. Repository hygiene that the briefs and lessons expect.**

* `README.md` at the root is GitLab boilerplate. Replace it with the project README: partner and scope in five lines, map of deliverables (document, `docs/data_model_canvas/`, `docs/Market-and-Risk-Analysis-Workbook.md`, `docs/market/`, `docs/sprint1/`), how to run the notebooks (link to `analysis.md` §5), branch and commit rules. Owner: Johlan (#30).
* `data/` is versioned (78 files: curated Parquet, reference CSVs, validation, text fixtures, manifests). Lesson 2 §5: "Partner extracts must not be committed … keep them in a folder listed in `.gitignore`, such as `data/`". The raw CSVs are ignored, but curated and fixture files are partner material. Decide with the partner (or the professor) whether the non raw package files may stay versioned; if not, ignore `data/` entirely and keep only `data/README.md`, `data/schemas/` and `data/scripts/`. Record the decision as an open decision in block 6 (owner: Danilo) and in risk R09.
* Toolchain: `requirements.txt` says "Python 3.11+" and `pandas>=2.2`; Lesson 2 asks for `pyproject.toml` with `requires-python ">=3.12,<3.13"`, `pandas<3`, and a committed `poetry.lock`. Add them (keep `requirements.txt` as a convenience export) and update `analysis.md` §5 to `poetry install` / `poetry run jupyter notebook`. Owner: Danilo.
* MkDocs: Lesson 1 §11 publishes `/docs` with MkDocs (`mkdocs new .`). Add a minimal `mkdocs.yml` with the document, the canvas folder and the Workbook in the nav, or state in the README why it is deferred. Owner: Johlan.
* `main` has direct commits (template merged into `main`, architecture activity added and reverted) and the presentation files (`docs/sprint1/`, `assets/templates/`, `assets/figures/`) exist **only on `main`**, not on `develop`. Merge `main` into `develop` (or cherry pick the template commit) so the release at the end of the sprint does not lose or duplicate files, and apply the rule "`main` only receives `develop`" from now on. Owner: Johlan with Gui.

---

## Part 3. Corrections file by file

### A. `documents/documentation.md`: header, Sections 1, 2.1, 2.2, 2.4 (Gui, #33 and #34; header: Johlan, #30)

**A-1. Header.** Fill Team Members (seven names and Sprint 1 roles from [roles.md](roles.md)), Institution (Inteli), Module (Module 8, Information Systems), Class (T18, 2026-2B), Repository (`https://git.inteli.edu.br/graduacao/2026-2b/t18/g03`). Partner: "Brazilian Army, Southeastern Military Command (CMSE)".

**A-2. Section 1 (1.1 to 1.3).** Write from the TAPI and the facts already used elsewhere: 1.1 overview (partner, SSEx, public financial and documentary execution, 150 months Jan 2014 to Jun 2026, pilot 2nd and 5th RM with 65 current UGE and 69 historical executors, three perspectives); 1.2 main objective in a verifiable form (Lesson 1 §9: result with direction and measure), e.g. "deliver a reproducible and auditable view of the healthcare expenditure identified in the public data of the 2nd and 5th RM, reconciled to the cent with the partner's control totals, extensible to the 12 RM by configuration"; 1.3 specific objectives = the five objectives of block 1 of `data_model_canvas.json`, so that Section 1 and the Canvas say the same thing.

**A-3. Section 2.1 Problem Statement and 2.2 Partner Needs.** Use the enterprise viewpoint vocabulary of Lesson 1 §5: community (D Sau and DGP; regional managers of the 2nd and 5th RM; hospitals, OMS and UGE), objective, decision at stake and its frequency (weekly regional briefing, fortnightly national meeting, twice weekly hospital meetings, already in 2.3 and in the JSON block 5), process that produces the data (credit → commitment → liquidation → payment → carried over payables, JSON block 3), policies (LGPD, public data only, no clinical data, no inference of quality of care or irregularity, no production system integration). 2.2 must list the partner needs exactly as the TAPI and kick-off answers state them (reproducible pipeline, control totals, institutional history, 12 RM scalability) and point to the VPC (4.1) for pains and gains, so the two do not drift.

**A-4. Section 2.4 Business Questions.** List the three MVP questions of the partner (Q02) with the same wording used in `value_proposition.md`, `use_cases.md`, 3.3 and the JSON block 2, plus the three derived questions of the JSON (supplier dependency and modality; lead time and carry over; which PI-SSEx questions the public data answers). Add the correspondence table of Lesson 1 §7: question → KPI (block 4) → grain and objects → source tables → use case. This table is the backbone that 3.2, 3.5 and the Workbook VPC must agree with.

**A-5. Section 3.4 Main Findings.** Today `[Fill in]` while the findings live in 3.3.5, 3.3.6, `outputs/03_eda_findings.md` (8) and `outputs/04_combination_findings.md` (6). Write 3.4 as the consolidated table of the 14 findings: finding, evidence (canonical number from Part 4), log ID (E1…, C1…), Canvas block it changes (template block number **and** our five block name), figure. Keep 3.3 as the method and 3.4 as the results, so they do not repeat each other. Basis: DMC brief 1.4 ("results should feed back into the Canvas design"), Lesson 2 §12 and §18.

### B. Section 2.3 and `user_profile.md` (Antoine, #26 and #39)

**B-1. `user_profile.md` contradicts 2.3 and the Canvas.** 2.3, `canvas.md`, `value_proposition.md` and the JSON make the regional managers the priority users; `user_profile.md` presents the three perspectives as equal and its status line still says "Sprint 01 draft for issue #15". Rewrite the table with "Regional (priority)" first, add the kick-off context (managers not from medicine; technical staff prepare slides; meeting cadence) that 2.3 and `canvas.md` already use, and add the "how they interact with data and which insights they need" column required by brief 1.3 (today the table has "information needed" but not the channel or form of consumption; take it from JSON block 5). Branch `39-prioritise-the-regional-managers-in-the-user-profile` exists; finish it.

**B-2. Section 2.3 wording.** "the reviewed logical model" and "reviewed EDA evidence" are now true; keep. Replace the paragraph "The partner still needs to confirm …" by a pointer to the open decisions list (D-4) so the same open items are not listed in four places with different wording.

**B-3. Add the data access rules to the User Profile as policies.** Lesson 1 block 8 and Lesson 3 §12 ("policies are implemented"): the five interpretation and access rules of `user_profile.md` are policies of the enterprise viewpoint; label them as such and reference them from the JSON governance block (`lgpd`, `etico`) so the three places say the same.

### C. Section 3.1, `data_structure.md`, `model.dbml`, `model.png` (Antoine, #8, #9, #15, #26, #27)

**C-1. `model.png` is a regression and must be regenerated (blocking).** The legend says "Solid lines: reviewed source relationships" but the image has no lines, no relationship list and no colour legend; the nine `Ref` entries of `model.dbml` are invisible. Brief 1.2 requires a "high level data architecture diagram". Regenerate from the DBML (dbdiagram.io export, or a renderer that draws the refs), with the three semantic groups (financial execution; institutional identity and bridges; documentary candidates), the lines for the nine refs, and the colour legend. Keep the previous `develop` version as reference if useful.

**C-2. `model.dbml` must reflect the grain the notebooks verified.** Lesson 1 §6 and §12: "declare a grain and check it". `execution_monthly_2014_2026` has no PK "until checked", but notebook 02 checked it: the raw monthly file has 1.5% split postings (Q3), and the silver grain is **month × base UG × budget plan × expense element × investment flag** (3.3.2). Either (a) model the silver fact with that composite PK and a note "verified in `02_data_quality.ipynb` (Q3)", adding `investment_flag` (GND 4) and `real_value_basis` handled as the real measures (`*_real_dec2025`) instead of a string, or (b) keep the raw candidate and add the silver fact as a second table. Also add the relationships that notebook 04 validated (`04_join_catalogue.csv`: 9 work, 5 partial, 2 do not) as `Ref` lines with a note on status, and rename `execution_monthly_2014_2026` if the PK is not asserted (reviewer point 8). Update the header comment date.

**C-3. `data_structure.md` must describe the flow as implemented, with layer contracts (Lesson 3 §14).** Today it describes a *proposed* five stage flow and states that no Spark run exists. Rewrite the "Collection and current storage" and "Proposed batch data flow" sections as: sources (bulk download files of the Portal da Transparência via the partner's Data Package; API only to fill gaps), landing (ZIPs as received, SHA-256 in the manifest), **Bronze** (Army slice, Parquet partitioned by month, `base_ug` merge, source file for lineage; guarantee: kept as received, typed values only), **Silver** (health rule A1, 69 executors, declared grain, signed values, real values; guarantee: one row per grain, invariants checked, reconciled 99.5% to the cent), **Outputs** (findings, figures, log; the Gold of Sprint 1), each with the quality checks of that layer and the action on failure (Lesson 3 §15). Then keep one short "future automated flow" paragraph that points to 3.3.1 instead of repeating it. Remove the duplicate blank line before "EDA alignment".

**C-4. Add the data flow diagram the brief asks for.** `model.png` is a logical ER diagram; brief 1.2 also asks to "show how data flows through the system to support the value proposition". Add `docs/data_model_canvas/data_flow.puml` (PlantUML component diagram, Lesson 3 §8: components = connectors, landing, bronze, silver, outputs, notebooks; interfaces = RawFiles, RawPartitions, ConformedEntities, Findings; no servers) and its PNG, referenced from `data_structure.md`, `canvas.md` and 3.2. The architecture activity that was pushed to `main` and reverted on 2026-10-22 (commits "add G03 healthcare data architecture proposal") probably already contains this diagram; reuse it.

**C-5. Section 3.1 must stop pointing to the future.** Replace the "Validation status and reproducibility" paragraph by: the keys checked at discovery (curated and reference files) **and** the grains verified afterwards in Spark (Table G1 of 3.3.2, with a cross reference, not a copy). Replace the link to `model.dbml` on the deleted #15 branch by the relative path. Keep the "UGE–OM join control" paragraph but add its result (C3: the bridge has one row; no OM view is possible yet).

**C-6. `docs/data_model_canvas/README.md` becomes the folder index and the review record.** Replace every branch URL by relative links; one row per file (notebooks, outputs, `analysis.md`, `data_quality_log.md`, `canvas.md`, `data_model_canvas.json`, `value_proposition.md`, `user_profile.md`, `data_structure.md`, `model.dbml`, `model.png`, `data_flow.*`, `prompts.md`); add the "Findings of the review" section that #27 asks for (what was checked on the PNG, whether it matches the DBML table by table, defects found and fixed: C-1). Normalise line endings to LF.

### D. Section 3.2, `canvas.md`, `data_model_canvas.json` (Andre, #16, #20, #21)

**D-1. KPIs with formula, unit and periodicity (Lesson 1 §9, checklist item 3; recurring mistake 1).** JSON block 4 (`indicadoresConsumo`) lists indicator names. Rewrite each as `name = formula; unit; periodicity; objects`, for example: "Committed healthcare expenditure = Σ committed over the silver grain, filtered by the eight health actions; BRL (nominal, and real Dec 2025 for 2014 to 2025); monthly, by RM and base UG; objects: execution_monthly, current_uge"; "Supplier concentration = share of the top 10 legal entity payees in healthcare commitment; %; 2026H1 and yearly when the document layer grows; objects: commitment note, payee"; "Commitment to first payment lead time = median and p90 of days between NE issue date and first bank order; days; quarterly cohort of NE issued in the first quarter; objects: NE, payment ↔ NE relation"; "Reconciliation difference = |recomputed − control| per unit × month; BRL and % of cells within R$ 0.05; every load". Every KPI must trace to one objective of block 1 and one question of block 2 (add the id in the text).

**D-2. Governance blocks 7 to 9 cannot stay "To be defined by G03" (Lesson 1 recurring mistake 3).** Name them: data owner = partner focal point (Lt Col Tarso Ramalho, CMSE; backup Col Eduardo Migon), data steward = Antoine (Data Structure role), data custodian = Danilo (notebooks, bronze and silver), technical lead = Danilo or Andre (team decision). Block 8: list the policies (LGPD art. 5 and 11 context: no clinical data; public financial data with masked CPF of individual payees; individuals counted but never listed; no credentials or internal documents in the repo) and classify the data: public, contains personal data (payee names of individuals, masked CPF), no sensitive data. Block 9: catalogue = `data/README.md` + `data/schemas/` + the partner dictionary; governance KPIs = reconciliation difference, coverage of the health classification, share of verified document links (already listed as candidates: promote them); maturity = "initial, assessed again in Sprint 5".

**D-3. First cube (blocks a to f, plus h, j, m) must be filled (Lesson 1 §8 and §9: "In Sprint 1 the group writes … a first cube").** `cubo-1` is empty. Fill from 3.3.2 and the log: name "Healthcare execution, monthly"; grain "one row per month, base UG, budget plan, expense element and investment flag (GND 4), 2014-01 to 2026-06" (checked in notebook 02, Q3); structure star schema; fact type periodic snapshot (monthly flows aggregated by the source); facts committed, liquidated, paid_current, paid_rp (BRL, signed); metrics = the KPIs of D-1; dimensions date (month), unit (base UG with RM, organisation type hospital / other, historical and current identity, predecessor and successor), budget plan, expense element, GND, action; sources (block h) = `01_RAW_EXECUCAO` through bronze and silver, references `04_REFERENCE`; transformations = A3, A4, A6, A8 of `analysis.md`; quality (block j) = the rules of the log (Q3 sum never dedupe, Q5 signed values, R1 reconciliation ≤ R$ 0.05, coverage of 150 months); history (SCD) = unit identity with validity periods; classification (block m) = public, no sensitive data. Leave `cubo-2` (documentary layer) as a provisional entry with its grain (one NE, one item, one payment, 2026H1) marked "provisional, Sprint 2". Export the JSON again from the template so it stays importable, and bump `metadata.data` and `versao`.

**D-4. One list of open decisions with owners (block 6).** The same open items appear with different wording in `canvas.md`, 2.3, `data_structure.md`, `analysis.md` §4, the log ("**Open**" rows) and the risk files. Make block 6 the single list, each entry as a question with an owner and the log ID: health rule and action 21C0 (R1, owner Danilo with the partner), UGE–OM bridge and the six health posts (C3, Antoine), 2026 IPCA factors (R7, Danilo), the 47 residual cells and the document vs monthly gap (R1, R5, Danilo), atypical months May 2020 and September 2021 (E2, Andre to ask the partner), expense mix interpretation (E5, Andre), validation sessions with regional managers (Q10, Leticia), storage and processing infrastructure (Sprint 2, Antoine), versioning of `data/` (X-10, Danilo). Every other file then links to block 6 instead of restating.

**D-5. Traceability chain in `canvas.md` and 3.2 (Lesson 1 §7).** Add one table: objective (block 1) → analytical question (block 2) → KPI (block 4) → grain and objects (cube a, d, f) → source tables → use case → finding IDs that support it. Mark any objective without a KPI as open in block 6 (rule of thumb of Lesson 1). This replaces the generic "Consistency review" table, which should keep only the four checks but with final verdicts (see X-5).

**D-6. Section 3.2 text fixes.** "Consistent once the #26 update … is merged" → "Consistent: the model carries execution by UGE and month, budget classification (action, PO, expense element, GND), payee and commitment item as candidates". "The VPC mentions an analytical dashboard and rankings, while the canvas keeps to comparisons" → after X-7 this row states that both use the same wording. Apply the two review corrections not yet applied: "2,259 suppliers" → "2,259 legal entity suppliers" (3.2 and 3.5); "bought mostly through accreditation (inexigibility, 53.5%)" → "53.5% of the 2026H1 healthcare commitment is contracted by inexigibility (37% in hospitals, 82% in the other units); accreditation contracts with OCS and PSA are the main channel". Add the provisional ETL entries (block 10 sources, 11 layers bronze/silver, 14 checks) marked "provisional, from Section 3.3.1", as Lesson 1 §8 allows; leave tactics empty or add the three tactics already used with their cost (partition by month, idempotent overwrite, decoupling through layers; cost: small files, rerun time, duplicated storage).

**D-7. `canvas.md` "Data Structure" block must match C-3 and C-4** (bronze, silver, contracts, link to the flow diagram) and the "Open relationships" bullet must cite the join catalogue IDs.

### E. Section 3.3, notebooks, `analysis.md`, `data_quality_log.md` (Danilo, #2, #7, #13, #14, #25)

**E-1. First cell of each notebook = Lesson 2 step 1.** Add, at the top of 01 to 04, the markdown cell with: analytical question (block 2 id), table(s), declared grain, key columns, invariants expected, related tables and join keys. Notebook 02 and 03 state part of this in prose; make it the explicit header the reviewer looks for.

**E-2. Completeness by dimension and period (step 4).** Null rates are reported by column only. Add the breakdown by base UG and by year for the columns that matter (at least `municipio`/`uf` and the six values), and record whether missingness concentrates in a unit or period (Lesson 2 §8). One cell, one log row if something appears.

**E-3. Relationships between measures (step 6).** No rank correlation is computed. Add one Spearman correlation between measures selected by name (for example committed vs paid_rp share by unit and year, or committed vs lead time by unit) and record it as a hypothesis in the log; or state in 3.3.5 why it is omitted. Keep the MAD outlier rule but say in one sentence that it plays the role of Tukey's IQR fence (3.3.7 already does).

**E-4. Idempotent, convention based Parquet writes (Lesson 2 §14 and §15; Lesson 3 §19).** Bronze is written with `mode("overwrite")` partitioned by month; there is no `ingestion_date` partition and `spark.sql.sources.partitionOverwriteMode` is not set to `dynamic`. Either align with the convention 3.3.1 itself proposes (`raw/<source>/<entity>/ingestion_date=…`, dynamic overwrite, read back and compare types and counts) or state the deviation and its cost in 3.3.3 and in the tactics block. Add the read back check (row count and dtypes equal to the inventory).

**E-5. Invariant named but not tested.** 3.3 says each invariant "(for example … 'a payment cannot exceed what was committed') becomes a count of violations". No such check exists in notebook 02 or in the log. Either add the check (paid ≤ committed per unit × year, and liquidated ≤ committed, counting violations) or change the example to one that was tested (every month present; keys unique; stages never summed).

**E-6. `data_quality_log.md`: add the template block numbers and the owners.** Lesson 2 §12 and §16 destination blocks are 4, 6, 14 and cube j (plus 8 and m for personal data). Add a column or suffix with the template block (for example "Data Structure (cube j, 14)", "Open → block 6, owner Danilo"). Every **Open** row must carry the owner that D-4 assigns. Add the LGPD finding (masked CPF in the document layer, names of individual payees: block 8 and cube m) and the data/ versioning decision (X-10).

**E-7. `prompts.md`.** Lesson 2 §16: save the four prompts filled in for each table in `/docs/data_model_canvas/prompts.md`, and state that only schema and aggregates were sent. The MRs declare AI assistance ("Generated with Claude Code"), so this file must exist; it also feeds Section 10 (AI usage) later.

**E-8. Section 3.3 text.** Replace `Table X0`, `Table X0.1`, `Table X`, `Table G1`, `Table Y`, `Table D1`, `Figure X1` to `X4` by sequential numbers (X-4). Keep 3.3.1 to 3.3.7 but move the result tables that 3.4 will consolidate (A-5) into cross references, so 3.3 and 3.4 do not duplicate. In 3.3.3 state the Bronze guarantee and in 3.3.4 the Silver guarantee (Lesson 3 §14) in one sentence each. 3.3.1 "future automated flow" is the only place that describes the future flow; `data_structure.md` points to it (C-3).

**E-9. `analysis.md` and toolchain.** §5 "How to reproduce" uses `venv` + `requirements.txt`; after X-10 use Poetry (Python 3.12, `pandas<3`, Java 17). State the run time and memory as the Volume response measure (about two minutes, 16 GB) so Lesson 3 §17 has a tested figure. Remove "under review" from the Sources of the findings files.

### F. Section 3.5, `use_cases.md`, `value_proposition.md` (Andre, #4, #10, #20, #21)

**F-1. Apply the review corrections.** 3.5 table UC2: "accreditation is 53.5%" → inexigibility wording (D-6); "2,259 suppliers" → "2,259 legal entity suppliers". `value_proposition.md` already has the right wording; copy it.

**F-2. Remove stale text (X-5)** in both files; in `use_cases.md` replace "Field names under Data used describe information families; the exact files and columns will be confirmed" by the actual silver and document columns (from `02_data_quality.ipynb` and `04_join_catalogue.csv`), since the Data Structure is now verified.

**F-3. Each use case must name the KPI of block 4 it uses** (after D-1) and the log IDs of its evidence, so the chain of D-5 can be read from the use case back to the objective. Brief 1.5: "insights translated into concrete actions": each story already ends with an action; add one line "Action recorded: …" in the table so it is explicit.

**F-4. `value_proposition.md` "Who receives the value"** must use the same three perspective table as `user_profile.md` after B-1 (one source, the others cite it).

### G. Section 3.3 ↔ 3.4 ↔ 3.5 continuity (Danilo, Gui, Andre)

**G-1.** After A-5, F-1 and E-8: 3.3 (method, assumptions, decisions) → 3.4 (14 findings, one table) → 3.5 (use cases citing finding IDs). Check that no number appears in 3.5 or 3.2 that is not in 3.4, and that 3.4 cites the log ID and figure for each.

### H. Section 4.1 Value Proposition Canvas (Leticia, #5, #23) and Workbook §2 (Mélina, #29)

**H-1. Translate 4.1 to English (X-2) and fix the CMSE expansion (X-8).**

**H-2. Align the VPC with the Canvas (Lesson 1 §11: same community, same decisions).** Customer segment: "managers of the Army Health System at the three perspectives, with the regional managers of the 2nd and 5th RM as priority users" (same as 2.3, `user_profile.md`, Workbook). Jobs must map to the business questions of block 2 (where did it change or concentrate; what explains it and with which evidence; what needs follow up) and to the decision cadence (weekly regional briefing). Add the mapping job → question → use case in 4.1.5.

**H-3. Update the evidence table 4.1.6 with the notebook figures (X-9).** Replace "79.180 linhas … agregado por mês, UG, função, subfunção e GND" by 10,227,887 rows in 150 monthly files (1,938,109 of the Army) at the grain month × UG × budget classification; "amostras documentais … 20 linhas" by the nine families and their row counts (34,197 NE; 60,532 items; 43,500 liquidations; 75,933 payments; 997 final beneficiaries; 5,106 invoices); "144 competências" stays but add "IPCA ends in December 2025, 2026 nominal (R7)"; add the reconciliation result (99.5% of 9,936 cells to the cent) as evidence for pain 7 and reliever 7; add the concentration and carry over findings as evidence for jobs 2 and 4. Remove the "Limite desta evidência" note about 20 line samples.

**H-4. Products, pain relievers and gain creators must not promise what the analysis showed does not work yet.** Reliever 6 "Sinais de NF e NUP extraídos" → the text signals match 0% (invoices) and 23.4% (process numbers) of documents (C6): reword as "candidate signals, not yet usable as dimensions; see risk R06". Reliever 4 "Pontes UGE↔OM com regra de alocação explícita" → the bridge has one row (C3): reword as "UGE–OM bridges with validity periods, pending the partner completing the bridge; until then expenditure stays with the executing UGE". Gain "Painéis por região, OM e função/subfunção" → "by RM, UGE, budget plan and expense element; by OM when the bridge is complete". Products "Painel analítico" → the wording of X-7. These are exactly the three VPC claims that the DMC consistency review (3.2) flags as different from the Canvas; after this change the row reads "same".

**H-5. Workbook §2 must contain the whole canvas, not a 3 row summary.** The brief says "fill in all sections of the canvas". Put in the Workbook the six lists (jobs, pains, gains, products, relievers, gain creators) in English, numbered 1 to 7 for pains and relievers, the image `assets/value_proposition_canvas.jpg`, and the problem solution fit table; Section 4.1 then summarises and links to the Workbook (or the reverse, but one of them is canonical: proposal, Workbook canonical, 4.1 = summary + evidence). Regenerate the canvas image after H-3 and H-4 if its text changes.

### I. Sections 4.2 and 4.3 Market Analysis and Sizing (Leticia, #11, #17, #32, #23) and Workbook §3 (Mélina)

**I-1. Same unit definition for SAM and SOM (brief 2.2 and 2.3: "SOM as a fraction of SAM").** SAM uses 156 FUSEx management units (2019); SOM uses the 65 pilot UGE, so the whole pilot (R$ 135,391) is 30% of the SAM although 2 RM are one sixth of 12. Limitation 8 admits it. Make it consistent: either compute the SAM with the pilot extrapolation (390 UGE, R$ 812,344, already in the sensitivity table) and keep the 156 UG value as the "published source" variant, or compute the SOM on the 156 UG pro rata (26 UG for 2 RM) and keep the 65 UGE figure as a variant. State the chosen base once in 4.3.2 and use it in the Workbook §3.3 and §1.

**I-2. TAM customers must be the customers of 4.2.2.** 4.2.2 presents two customer groups (ANS operators, R$ 305 billion; Armed Forces); 4.3 defines the TAM as the Armed Forces only and puts the 144 self managed operators in an "adjacent" line. Either present 4.2.2 as "the project's customer type is the Armed Forces health systems; self managed operators are the adjacent market used only to show expansion", or include them in the TAM. Keep one choice in 4.2, 4.3, the Workbook and the slides (Workbook calls it "Expanded TAM", 4.3 calls it "TAM + self-managed plans": one name).

**I-3. Source verification (#23 DoD).** The MR checklist left "Figures from public sources checked against each link" unchecked. Open every S1 to S15 link, confirm the figure, and record the check (date, who) in Section 14 or in `tmp`. Fix S8 (DOI issue number mismatch is documented; fine) and keep.

**I-4. Workbook §3 must be a faithful summary of 4.3**: same version date (4.3 says v3 dated 23/10; Workbook says 22/10), same names, same source codes after X-6 (replace G1 to G9 by S13, S12, S4, S14, P1/P2, S7, S8, S2, S15), replace "Teammate's TAM_SAM_SOM_bottom_up.pdf" and "docs/market/market_sizing.md" (file does not exist) by "Section 4.3 of `documents/documentation.md`". Remove the "Source-status caution" paragraph once I-3 is done.

### J. Risk Matrix and mitigation (Mélina, #12, #18, #28) and Section 4.4 (#22)

**J-1. Cover the four categories the brief names.** The ten risks are data and delivery risks; none is a **team** risk (turnover, availability, expertise, seven parallel branches and one reviewer bottleneck) and "technology" and "complexity" are only implicit (R10). Add at least R11 (team: member availability and review bottleneck; evidence: issues #1, #19, #33, #34, #35, #36, #24 had no deliverable on `develop` by D5) and R12 (technology and complexity: Spark on a laptop handles 8.7 GB in two minutes, but 12 RM and the full document history need a cluster or incremental processing; 16 joins tested, 7 partial or broken), and add a "Brief category" column (team / technology / complexity / operational) to the register so the evaluator sees the coverage. Score and mitigate them like the others.

**J-2. Owners by name.** Replace "Person 2/3/4/5/6/7" by Mélina, Danilo, Antoine, Andre, Gui, Johlan in `risk_matrix.md` §4A, `risk_mitigation.md` §2 and §5, and the Workbook §4. The brief asks for "a responsible team member".

**J-3. Official template.** The brief says "use the official Risk Matrix template available on the class drive". Confirm the template (probability × impact grid, colours, columns) and reproduce its layout in the Workbook §4 (the 5×5 grid of `risk_matrix.md` §4A.3 is the right content; make it the template's layout, with the risk IDs in the cells and the colour bands). If the template is a spreadsheet, export it to `docs/market/risk_matrix_template.xlsx` or an image and link it.

**J-4. Update the register with the EDA evidence (the register itself says "scores must be revisited after the EDA").** The reviewer observations in `risk_mitigation.md` ("Leticia reports … must be checked") are now verified in the notebooks: `06_bridge_uge_om.csv` has one row (C3); IPCA ends in 2025 and 2026 stays nominal (R7); the payment ↔ NE join inflates totals by 80% if misused (C1) which is R03 observed and controlled; reconciliation reached 99.5% of cells to the cent with 47 residual cells (R1) which is R07 partly retired; all 150 months present (R05 coverage confirmed for the monthly file, open for the document layer R5). Add an "Evidence after EDA (log ID)" column to §4A.2, re score where the evidence justifies (for example R07 probability from 4 to 2 or 3), and replace the "reported, to be checked" sentences by the verified statement. Residual scores may now be assessed for the controls that exist (grain test, signed values, reconciliation, join tests).

**J-5. Merge the two risk files into one register or make the cross references exact.** `risk_matrix.md` says "D3 mitigation plans are not included in this version" and `risk_mitigation.md` says its baseline is "on the D2 branch". Keep two files if preferred, but each header must link to the other, and the Workbook §4 must be the consolidated view (ID, event, category, cause, P, I, score, band, owner, mitigation summary, trigger, contingency, evidence).

**J-6. Section 4.4 Risk Assessment and Mitigation.** Write it from the consolidated register: method (scales, bands), the matrix grid, the table of 12 risks with owner and mitigation summary, the gates G1 to G5 of `risk_mitigation.md` §4, and the open items that are also in block 6 (D-4). Partner oriented justification per risk (the brief's criterion) is already in the register; cite it.

**J-7. Section 4.5.** One paragraph on what the Workbook is and the relative link `../docs/Market-and-Risk-Analysis-Workbook.md` (after X-1), plus the structure check the DoD of #22 asks for (three components present in order).

**J-8. Source codes (X-6)** in both risk files.

### K. Workbook (Mélina, #29 and #22; Leticia for §2 and §3)

**K-1.** Path (X-1), status line and §6 checklist (X-5), VPC in full (H-5), sizing aligned (I-4), risks with names, categories, matrix layout and EDA evidence (J-1 to J-4), source codes (X-6), wording of products (X-7). §5 traceability table: replace branch and "verify" wording by the final paths. §1 executive summary: the "Market" row must use the base chosen in I-1.

**K-2. Add the dependency the brief expects between the two deliverables (Lesson 1 §11).** One paragraph in §2 stating that the VPC customers are the community of the Canvas (Section 3.2) and the jobs are its analytical questions, with the mapping of H-2.

### L. Section 14, cover, table of contents, numbering (Johlan, #30)

**L-1. Section 14 consolidates everyone's references**, today only the market sources. Add, with the scheme of X-6: TAPI V1; kick-off transcript (16/10); kick-off answers (18/10); indicators annex; Portaria DGP/C Ex 444/2023 (EB30-N-10.006); Data Package README and manifests; Portal da Transparência (bulk download and API documentation, cited in 3.3.1); the module materials (Lessons 1, 2, 3 and the Data Model Canvas template, cited in 3.2); the standards and books the sections rely on (ISO/IEC 10746 RM-ODP, ISO/IEC 25010 and 25012, Kimball and Ross, Tukey, Reis and Housley, LGPD Lei 13.709/2018), in ABNT style like the existing entries. Every in text code in 2.x, 3.x, 4.x and the risk files must resolve to an anchor here.

**L-2. Cover and table of contents.** Fill the header (A-1); the TOC anchors are fine; add the list of tables and figures once X-4 is done.

**L-3. Numbering and formatting pass (X-4), final link check** (every relative link in `documents/`, `docs/data_model_canvas/`, `docs/market/`, the Workbook and the two findings files resolves on `develop`), and LF line endings.

### M. Beyond the two artifacts: repository and presentation (Johlan, Gui)

**M-1.** Root README, MkDocs, `main` ↔ `develop` (X-10).
**M-2.** `docs/sprint1/presentation.md` on `main` has no deck link and an unchecked DoD; the deck itself does not exist in the repository. Record the deck link and bring `docs/sprint1/` to `develop`. The slide numbers must come from Part 4.

---

## Part 4. Canonical values and wording (single source of truth)

Every section must use these values. The "Source" column is the file that computes or defines them; all other places cite, never recompute.

| Item | Canonical value | Source | Must appear in |
| --- | --- | --- | --- |
| Partner | Brazilian Army, Southeastern Military Command (CMSE); focal point Lt Col Tarso Ramalho, backup Col Eduardo Migon; D Sau under DGP directs the SSEx | TAPI | header, 1.1, 2.1, 4.1, Workbook, JSON block 7 |
| Scope | 2nd RM (SP, 29 UGE) and 5th RM (PR and SC, 36 UGE): 65 current UGE, 69 historical executors, 9 OMS; Jan 2014 to Jun 2026, 150 months; extensible to 12 RM | TAPI, `04_REFERENCE` | 1.1, 2.3, 3.1, 3.3, 4.1, 4.3, risk files, Workbook |
| Priority users | Regional managers of the 2nd and 5th RM; national (D Sau, DGP) and local (hospitals, OMS, UGE) complete the three perspectives | kick-off Q10, Q11 | 2.3, `user_profile.md`, `value_proposition.md`, `canvas.md`, JSON block 5, 4.1, Workbook §2 |
| Business questions | Q1 where did healthcare expenditure vary or concentrate; Q2 which units, objects, procurements and payees explain it and with which documents; Q3 which cases need follow up | kick-off Q02 | 2.4, `value_proposition.md`, `use_cases.md`, 3.3, JSON block 2, 4.1 jobs |
| What is delivered | Analytical outputs (infographic sets A and B, reproducible notebooks, documented tables) that complement PI-SSEx; not a dashboard, no internal system integration | TAPI | 4.1, Workbook §2, `value_proposition.md`, JSON block 5 |
| Volume | 1,195 files, 8.67 GB; 150 monthly files, single 47 column layout, 10,227,887 rows, 1,938,109 Army rows; 1,002 document files, 417,278 rows (NE 34,197; items 60,532; item history 69,364; liquidations 43,500; liq ↔ NE 51,897; payments 75,933; pay ↔ NE 75,752; final beneficiaries 997; invoices 5,106) | `01_setup_and_ingestion.ipynb`, `outputs/01_ingestion_summary.csv` | 3.1, 3.3.3, 4.1.6, risk R10 |
| Grain | Silver and EDA: month × base UG × budget plan × expense element × investment flag; raw monthly file has 1.5% split postings (sum, never dedupe); document keys unique; payment ↔ NE many to many (1 payment up to 27 NE; 1 NE up to 364 payments) | `02_data_quality.ipynb` (Q3, Q4), 3.3.2 | 3.1, 3.3.2, `model.dbml`, JSON cube a, `data_structure.md` |
| Health rule | Eight budget actions `2004, 2E74, 00P1, 20XL, 20YE, 00VL, 2887, 20G5`; pending partner validation (incl. 21C0) | `analysis.md` A1, log R1 | 3.3.4, `canvas.md`, JSON block 6, risk R01 |
| Reconciliation | 9,889 of 9,936 unit × month cells (99.5%) to the cent on four measures; 99.8% on committed; net committed difference R$ 13,094.53; 47 residual cells, mostly 2023; 2026H1 extension exact; 34 acceptance and 11 quality tests passed | log R1 to R3 | 3.3.4, 4.1.6, risk R07, Workbook §4 |
| Documents vs monthly, 2026H1 | committed −5.7%, liquidated −0.9%, paid −6.5%, RP paid −3.9%; 56.8% of paid value with identifiable NE; 10,829 of 31,958 cited NE absent | log R5, R6 | 3.3.4, 3.3.6, `data_structure.md`, block 6 |
| Totals | R$ 5.42 bn real (R$ 4.05 bn nominal) committed 2014 to 2025, about R$ 440 m per year; pilot +4.7% real (2nd RM +2.9%, 5th RM +7.3%) vs Army +19.0%; pilot share 17.2% → 15.1% | `03_eda_findings.md` #1 | 3.3.5, 3.4, `value_proposition.md`, `canvas.md` |
| Concentration by unit | HMASP 31%, HGeC 19%, HGuFl 6% of 2014 to 2025 (56%); hospitals 52% to 60% per year; 2nd RM HHI up to 3,786, HMASP 60% of the region | #2, log E4 | 2.3, 3.2, 3.3.5, 3.4, `value_proposition.md`, `use_cases.md` |
| Funding | PO 0007 65%, 0003 26%, 0004 5% | #3 | 3.3.5, 3.4, `value_proposition.md` |
| Expense mix | 2nd RM element 39: 81% → 61%; element 30: 13% → 29% (2014 → 2025) | #4, log E5 | 3.3.5, 3.4, `canvas.md` |
| Seasonality | December 10.9%, Q4 28.9% of annual commitment (uniform: 8.3%, 25%) | #5, log E1 | 2.3, 3.3.5, 3.4, `use_cases.md` |
| Carry over | RP paid 11% of 2025 payments, 20% Jan–Jun 2025, 24% Jan–Jun 2026; same year payment 73% to 91%; 39.8% of 2026H1 cash settles previous years (37.0% from 2025) | #6, log C4 | 2.3, 3.3.5, 3.3.6, 3.4, `value_proposition.md`, `use_cases.md` |
| Atypical | 2 pilot months (May 2020 low, Sep 2021 high); 37 material unit years in 20 units (MAD > 3.5 and ≥ R$ 1 m); 15th Brigade jump = 33rd Battalion execution moved (2019) | #7, log E2, E3, C5 | 3.3.5, 3.3.6, 3.4, `use_cases.md` |
| Investment | R$ 238 m real in 12 years, 4.4% of health commitment, peak 2020 | #8, log E6 | 3.3.5, `data_structure.md` |
| Procurement | Inexigibility 53.5%, electronic auction 42.8% of 2026H1 health commitment; inexigibility 37% in hospitals, 82% in other units | `04_combination_findings.md` #1 | 3.2, 3.3.6, 3.4, 3.5, `value_proposition.md` |
| Suppliers | 2,259 legal entity suppliers; top 10 28.8%, top 50 56.4%; 180 serve both RM; median top supplier share 32% in non hospital units (16 above 50%) vs 10% to 17% in hospitals | #2 | 3.2, 3.3.6, 3.4, 3.5 |
| Lead time | Median 30 days, p90 75 days NE to first bank order (NE of Jan–Mar 2026); hospitals 45 vs other units 27; consumables 58 vs services 24 | #3 | 3.3.6, 3.4, 3.5, `use_cases.md` |
| Joins | 16 tested: 9 work, 5 partial, 2 do not; header join after pay ↔ NE overstates by 80% (R$ 739.6 m vs R$ 411.8 m); UGE ↔ OM bridge one row; text signals 0% (invoices) and 23.4% (process) | `04_join_catalogue.csv`, log C1 to C6 | 3.3.6, `data_structure.md`, `model.dbml`, 4.1 relievers 4 and 6, risks R03, R06 |
| Real values | Dec 2025 BRL with the exact IPCA ratio for 2014 to 2025; 2026 nominal, compared with the same window of 2025 | log R4, R7 | 3.3.4, 3.3.5, `data_structure.md`, risk R07 |
| Market sizing (base) | L = R$ 259,091; SAM = R$ 444,810; TAM = R$ 659,547; TAM + self managed = R$ 3,283,174; SOM = R$ 45,628; whole pilot R$ 135,391; licence only SAM R$ 259,091 and SOM R$ 26,577; low/high TAM 273,985 / 2,854,829, SAM 184,781 / 892,134, SOM 15,206 / 90,967; version 3, 23/10/2026 | 4.3.6 and 4.3.7 | 4.3.2, Workbook §1 and §3, slides (subject to I-1) |
| Risks | R01 to R10 as in `risk_matrix.md` §4A.2 (six Critical, four High), plus R11 and R12 after J-1; owners by name | `risk_matrix.md` | 4.4, Workbook §4, `risk_mitigation.md` |

---

## Part 5. Execution order and suggested MRs (all into `develop`, branch `tipo/descricao-pt`)

1. **`fix/canvas-e-modelo-dados` (Antoine, Andre):** C-1, C-2, C-3, C-4, C-6, B-1, B-2, D-1 to D-7, F-1 to F-4, X-5 for their files. These define the KPIs, cube, owners and open decisions that every other section cites.
2. **`docs/analise-e-log` (Danilo):** E-1 to E-9, X-10 toolchain and `data/` decision, 3.3 numbering; depends on D-1 (KPI ids) and D-4 (owners).
3. **`docs/workbook-e-riscos` (Mélina, Leticia):** X-1, X-6 in their files, X-7, X-8, H-1 to H-5, I-1 to I-4, J-1 to J-8, K-1, K-2, Sections 4.4 and 4.5.
4. **`docs/secoes-1-2-e-3-4` (Gui):** A-2 to A-5, G-1; depends on 1 and 2 for the KPI table and the findings table.
5. **`docs/padronizacao-final` (Johlan):** A-1, X-3 header and Section 15, X-4, L-1 to L-3, M-1, M-2, root README, `main` ↔ `develop`; last, after 1 to 4 are merged.

Each MR: Conventional Commit in English ending with `#issue`, `Closes #N` for the issues it finishes, reviewer other than the author using the Approve button, and a link check before merge. Do not close or renumber issues; reuse the open cards (#22, #23, #27, #30, #33, #34, #38, #39) and add the correction items to their descriptions.
