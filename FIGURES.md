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
