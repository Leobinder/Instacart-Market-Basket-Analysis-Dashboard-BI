# Instacart Market Basket Analysis — Dashboard BI

Dashboard analítico completo construído com Python + Power BI
sobre os dados públicos do Instacart (3,2 milhões de pedidos).

## Visão geral do projeto

| Métrica | Valor |
|---|---|
| Pedidos analisados | 3,2 milhões |
| Clientes únicos | 206 mil |
| Itens vendidos | 32 milhões |
| Taxa de recompra | 59% |
| Regras de associação geradas | 30 |

## Páginas do dashboard

### 1. Visão Geral
KPIs principais, mapa de calor de pedidos por hora/dia,
ciclo de recompra e ranking de departamentos.

**Insight:** pico de pedidos nas manhãs de fim de semana
(sábado 9h-11h). Ciclo semanal e mensal identificados
via days_since_prior_order.

### 2. Produtos & Recompra
Análise de fidelização por produto e departamento,
matriz volume × recompra e identificação de produtos âncora.

**Insight:** apenas 9,13% dos produtos respondem por 80%
do volume (Lei de Pareto). Banana lidera com 84% de recompra.

### 3. Market Basket Analysis
Regras de associação via algoritmo Apriori (mlxtend),
com métricas de suporte, confiança e lift.

**Insight:** par Limes → Large Lemon tem lift de 3,2 —
ou seja, 3,2x mais provável de ser comprado junto
do que seria pelo acaso.

### 4. Segmentos de Clientes
Segmentação em 4 perfis baseada em frequência de pedidos
e tamanho de cesta (corte por mediana).

| Segmento | % Clientes |
|---|---|
| Fiéis intensos | 27,86% |
| Recorrentes leves | 25,83% |
| Esporádicos | 24,16% |
| Estoque mensal | 22,14% |

## Stack tecnológica

- **Python 3.14** — pandas, mlxtend (Apriori/FP-Growth)
- **Power BI** — modelagem estrela, DAX, Power Query
- **Fonte de dados:** [Instacart Market Basket Analysis — Kaggle](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)

## Como reproduzir

1. Baixe os dados originais no Kaggle (link acima)
2. Execute `scripts/market_basket.py` para gerar as regras
3. Execute `scripts/segmentacao.py` para segmentar clientes
4. Abra `dashboard.pbix` no Power BI Desktop
5. Atualize os caminhos das fontes de dados para sua máquina

## Decisões técnicas

- **Amostragem de 50k pedidos** para o Apriori: viabilidade
  computacional sem perda de significância estatística
- **Pré-agregação em Python** antes do Power BI: evita
  carregar 32M de linhas brutas no modelo
- **Corte por mediana** na segmentação: mais robusto que
  média em distribuições assimétricas como frequência de compra
- **Filtro de volume mínimo** (≥1000 compras) no ranking
  de produtos: elimina ruído de produtos com poucas ocorrências
