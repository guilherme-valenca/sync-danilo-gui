# Números canônicos

O dono é o **danilo**. O gui semeou a tabela a partir das saídas dos notebooks na branch
`feat/notebooks-analise-dados`, commit `db8ac8d`. O estado de cada linha é `proposto`,
`confirmado danilo` ou `corrigido`. Nenhum documento cita um número que não esteja aqui
como `confirmado danilo`.

| # | Figura | Valor | Escopo (sempre dito no texto) | Fonte | Como pode ser escrito | Estado |
|---|---|---|---|---|---|---|
| 1 | Reconciliação do painel curado | 9.889 de 9.936 células unidade × mês (99,5%) nas 4 medidas; 99,8% em empenhado | Tolerância de R$ 0,05 escolhida pelo time; a Q31 pede centavo e causa para cada diferença; 47 células sem causa identificada | 02, células 23–24 | "agree within R$ 0.05 (team tolerance; Q31 asks for the cent)", nunca "match to the cent" | proposto |
| 2 | Pagamentos com NE na camada 2026 | 56,8% do valor pago; dos R$ 177,9 mi restantes, R$ 148,3 mi quitam NE de 2025 (~36% do pago) e R$ 18,1 mi citam NE de 2026 ausentes | Todas as ações orçamentárias | 02, células 37–38 | Sem "most payments settle 2025 notes" | proposto |
| 3 | Caixa de 2026H1 para empenhos de anos anteriores | 39,8% (37,0% de 2025) | Todas as ações, 65 UGE, 2026H1 | 04, células 22–23 | Só com o rótulo "all budget actions". Em texto de saúde usar a linha 4 | proposto |
| 4 | Restos a pagar em pagamentos de saúde | 11% em 2025 no ano; 20% em jan–jun 2025; 24% em jan–jun 2026 | Saúde (8 ações = filtro B) | `03_eda_findings.md` #6 | "carried-over payables are 24% of healthcare payments in Jan–Jun 2026" | proposto |
| 5 | Prazo NE → 1º pagamento | 82,6% das NE de saúde de jan–mar pagas até junho; entre essas, mediana 30 dias e p90 75 | Saúde, NE de jan–mar 2026; exclui os 17,4% não pagos, então subestima | 04, célula 20 | Sempre com a ressalva dos 17,4%; o parceiro acompanha NE→liquidação e liquidação→pagamento separadamente | proposto |
| 6 | Concentração de fornecedores | Top 10 com 28,8% e top 50 com 56,4%, de 2.259 fornecedores PJ | Saúde 2026H1, por CNPJ completo (14 dígitos), portanto limite inferior | 04, células 16 e 18 | "(per full CNPJ; lower bound)" | proposto |
| 7 | Modalidade de compra | Inexigibilidade 53,5% (37% em hospitais, 82% nas demais); pregão eletrônico 42,8% | Saúde 2026H1 | 04, célula 13 | "inexigibility (accreditation) is the main channel", nunca "without competitive bidding" | proposto |
| 8 | 15ª Bda | 33º BI Mec até R$ 0,13 mi/ano (2014–2018); Bda de R$ 4,03 a 15,14 mi/ano desde 2019 | Nominal | 04, célula 25 | A transferência explica quando o salto começa, não o tamanho; o gasto fica com a unidade executora (Q16). Nunca "not new spending" | proposto |
| 9 | Universo | 69 executores históricos, 65 UGE correntes (29 na 2ª RM, 36 na 5ª RM), 5 situações especiais | Referência do pacote | `04_REFERENCE` | 65 UGE é cobertura de dados, não número de usuários (Q15) | proposto |
| 10 | Perímetro de saúde | 8 ações orçamentárias | É o filtro B (Q20). Cobertura C9 não medida | `analysis.md` (tabela de regras) | Sempre nomear como filtro B e dizer que o C9 não foi medido | proposto |
| 11 | Mercado (do !19, aritmética conferida) | TAM R$ 659.547; SAM R$ 444.810; SOM R$ 45.628 (cenário base) | Preço de referência de capacidade proprietária equivalente; o projeto entrega código aberto (TAPI, transcript) | `documentation.md` §4.3 (!19) | Os mesmos valores no Workbook e na §4.3 | proposto (dono gui) |
| 12 | Executores com saúde | 67 dos 69 executores históricos executam ações de saúde | Saúde (8 ações), 2014–2026 | 03 / `03_eda_findings.md` | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 13 | Crescimento real 2014→2025 | Piloto +4,7%; 2ª RM +2,9%; 5ª RM +7,3%; Exército +19,0%. Participação do piloto 17,2% → 15,1% | Reais (IPCA, dez/2025). O total do Exército inclui executores centrais, então não é escopo equivalente (Q43) | 03, célula 9 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 14 | Peso dos hospitais | HMASP 31%, HGeC 19%, HGuFl 6%; hospitais entre 52% e 60% ao ano; HHI da 2ª RM 3.786 em 2025 | Saúde | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 15 | Fontes por plano orçamentário | PO 0007 65%, PO 0003 26%, PO 0004 5% | Saúde, empenhado | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 16 | Mix de despesa da 2ª RM | Elemento 39 de 81% para 61%; elemento 30 de 13% para 29% | Saúde, 2ª RM. Descreve o que se comprou, não como o atendimento foi feito (annex §4) | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 17 | Sazonalidade | Dezembro com 10,9% e 4º trimestre com 28,9% dos empenhos | Saúde | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 18 | Pagamento no mesmo ano | Entre 73% e 91% | Saúde | 03 / `03_eda_findings.md` #6 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 19 | Atipicidades | 2 meses atípicos (mai/2020, set/2021); 37 unidade-ano em 20 unidades (z robusto > 3,5 e ≥ R$ 1 mi) | Saúde | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
| 20 | Investimento (GND 4) | R$ 238 mi reais, 4,4% do empenhado em saúde, pico em 2020 | Saúde, reais | 03 | Citar como está, dentro da regra de voz | proposto (gui, R5) |
