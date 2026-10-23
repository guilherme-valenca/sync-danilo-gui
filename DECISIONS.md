# Decisões

Uma decisão vale quando tem `ok gui` e `ok danilo`, ou quando um humano a fechou. Só se
acrescenta; para mudar uma decisão, abre-se outra que a substitui.

| # | Decisão | Proposta por | ok gui | ok danilo | Humano |
|---|---|---|---|---|---|
| D1 | Integrar primeiro, revisar depois: mergear todos os MRs abertos como estão (Fase 0) e corrigir em MRs de revisão | gui | ok | | Guilherme sugeriu |
| D2 | Divisão por artefato e arquivo: danilo fica com a análise e os componentes do DMC (R1, R2); gui fica com o Workbook, o User Profile e §2.3, e a linguagem (R3, R4, R5) | gui | ok | | |
| D3 | O `FIGURES.md` é a única fonte de números; o danilo confirma cada linha | gui | ok | | |
| D4 | Hoje não se re-executa nenhum notebook: só células markdown, via `nbformat`. Os recálculos vão para issues da Sprint 2 (prazo com NE não pagas como censuradas, CNPJ raiz, cobertura C9, causa das 47 células, igualdade exata ao centavo) | gui | ok | | |
| D5 | O `model.png` é re-renderizado com os 9 Refs visíveis, ou a legenda falsa sai | gui | ok | | |
| D6 | Ninguém aceita o próprio MR | humanos | ok | | Guilherme |
| D7 | A §2.3 sai do R4 e vai para o R5. O R4 fica só com o `user_profile.md`, alinhado à §2.3 do R5 | R5 | ok | | |
| D8 | A regra de voz da documentação (seção em `PLAN.md`) vale para todas as seções e para o Workbook | Guilherme, via R5 | ok | | Guilherme |
| D9 | O R5 é dono da §14 e mantém todas as referências já presentes na `develop`, com as âncoras | gui | ok | | |
| D10 | A branch do R5 é `34-<slug>`, com um commit `Refs #33` (§1) e outro `Refs #34` (§2.x, §3.4, §14). O MR fecha a #34 e referencia a #33 | R5 | ok | | |
| D11 | Excepcionalmente, até o fim da correção não se acompanha issue nem quadro do GitLab. A coordenação acontece aqui; no fim tudo vai para Done de uma vez. Continuam valendo branch + MR para a `develop`, commits `docs: …` e ninguém aceitar o próprio MR | Guilherme | ok | | Guilherme |
