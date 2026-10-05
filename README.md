# Dashboard de Vendas — Power BI

## Objetivo

Criar um dashboard comercial para uma empresa fictícia, permitindo acompanhar faturamento, pedidos, ticket médio, produtos e vendedores.

> Os arquivos de dados são fictícios. O projeto é entregue sem `.pbix` para manter o repositório versionável e permitir a recriação do dashboard no Power BI Desktop.

## Modelo dimensional

```text
             DimDate
                |
DimCustomer -- FactSales -- DimProduct
                |
            DimSeller
```

## Medidas DAX

```DAX
Faturamento =
SUMX(
    FactSales,
    FactSales[Quantity] * FactSales[UnitPrice]
)
```

```DAX
Pedidos =
DISTINCTCOUNT(FactSales[SaleID])
```

```DAX
Itens Vendidos =
SUM(FactSales[Quantity])
```

```DAX
Ticket Médio =
DIVIDE([Faturamento], [Pedidos])
```

```DAX
Preço Médio =
DIVIDE([Faturamento], [Itens Vendidos])
```

```DAX
Faturamento Ano Anterior =
CALCULATE(
    [Faturamento],
    SAMEPERIODLASTYEAR(DimDate[Date])
)
```

```DAX
Crescimento YoY =
DIVIDE(
    [Faturamento] - [Faturamento Ano Anterior],
    [Faturamento Ano Anterior]
)
```

## Como recriar

1. Abra o Power BI Desktop.
2. Importe os CSVs da pasta `data`.
3. Crie os relacionamentos conforme o modelo.
4. Crie as medidas DAX.
5. Monte uma página com:
   - cartões de KPI;
   - linha de faturamento por mês;
   - barras por categoria;
   - ranking de produtos;
   - ranking de vendedores;
   - filtros de período, estado e categoria.

## Estrutura sugerida

```text
+------------------------------------------------------+
| FATURAMENTO | PEDIDOS | TICKET MÉDIO | ITENS        |
+------------------------------------------------------+
| Evolução do faturamento       | Faturamento categoria|
+-------------------------------+---------------------+
| Ranking produtos              | Ranking vendedores  |
+-------------------------------+---------------------+
| Filtros: Data | Estado | Categoria | Vendedor       |
+------------------------------------------------------+
```

## Competências

`Power BI` `DAX` `Power Query` `Star Schema` `Data Modeling` `Business Intelligence`
