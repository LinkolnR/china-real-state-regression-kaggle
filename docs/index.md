# Previsão de Demanda Imobiliária Chinesa

## Disciplina

**Redes Neurais 2025.2**  
Projeto de Conclusão: Previsão de Demanda Imobiliária Chinesa via Competição Kaggle

## Introdução

Este trabalho apresenta uma análise comparativa de três modelos de regressão neural desenvolvidos para prever a demanda de transações imobiliárias no mercado chinês. Participação na competição Kaggle "Real Estate Demand Prediction Challenge".

## Contexto da Competição

- **Objetivo**: Prever volume mensal de vendas (em 10 mil Yuan) para o mercado chinês
- **Horizonte Temporal**: Janeiro 2019 - Julho 2024
- **Granularidade**: Setor + Mês (95 setores distintos)
- **Métrica**: Score customizado baseado em MAPE (Mean Absolute Percentage Error)

## Objetivos Principais

1. Estabelecer um modelo baseline (v1) simples como referência
2. Implementar feature engineering avançado com lags e médias móveis (v2)
3. Explorar busca automatizada de hiperparâmetros (v3)
4. Comparar desempenho através de métricas padronizadas

## Estrutura do Documento

A documentação está organizada em seções temáticas:

- **Contexto do Projeto**: Descrição da competição e desafios
- **Dataset**: Análise exploratória e preparação dos dados
- **Modelos**: Detalhes técnicos de cada versão
- **Avaliação**: Métricas, comparações e resultados
- **Workflow**: Guia de execução e reprodução
- **Referências**: Bibliografias e recursos

## Resumo

O modelo v3 (com otimização de hiperparâmetros) demonstrou o melhor desempenho na competição, alcançando Competition Score = 0,46482 e $R^2$ = 0,9942. O modelo v2 (com feature engineering avançado) segue de perto com Competition Score = 0,46430 e melhor estabilidade (RMSE = 7.547,03). Ambos são modelos de excelente qualidade, com v3 recomendado para máxima performance e v2 para melhor generalização.

### Resultados Principais

| Versão | RMSE | MAE | $R^2$ | Competition Score |
|--------|------|-----|----|--------------------|
| v1 (Baseline) | 38.937,57 | 13.565,70 | 0,5513 |0,0000 |
| v2 (Recomendado) | 7.547,03 | 1.626,75 | 0,9763 |  0,46430 |
| v3 (Otimização) | 19.991,72 | 863,65 | 0,9942 | 0,46482 |

**Ranking Final (Scores Oficiais da Competição):**

1.  **v3**: Maior Competition Score (0,46482), $R^2$ mais alto (0,9942)
2.  **v2**: Competition Score (0,46430), melhor generalização com RMSE mais baixo
3.  **v1**: Baseline com RMSE 38.937,57

**Nota Importante**:
- v3 obtém score ligeiramente melhor na competição (0,46482 vs 0,46430)
- Apesar de v2 ter RMSE mais baixo, v3 tem $R^2$ superior e vence por uma pequena margem


---

**Versão**: 1.0  
**Data**: 2025-10-25  
**Status**: Completo
