# Previsao de Demanda Imobiliaria Chinesa

## Disciplina

**Redes Neurais 2025.2**  
Projeto de Conclusão: Previsão de Demanda Imobiliária Chinesa via Competição Kaggle

## Introducao

Este trabalho apresenta uma análise comparativa de três modelos de regressão neural desenvolvidos para prever a demanda de transações imobiliárias no mercado chinês. Participação na competição Kaggle "Real Estate Demand Prediction Challenge".

## Contexto da Competicao

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

## Resumo Executivo

O modelo v2 (com feature engineering avançado e validação por setor) demonstrou o melhor desempenho, explicando 97,6% da variância nos dados com R² = 0,9763. Este modelo é recomendado para a submissão final.

### Resultados Principais

| Versão | RMSE | MAE | R² | Competition Score |
|--------|------|-----|----|--------------------|
| v1 (Baseline) | 38.937,57 | 13.565,70 | 0,5513 | - |
| v2 (Recomendado) | 7.547,03 | 1.626,75 | 0,9763 | 0,9530 |
| v3 (Otimização) | 19.991,72 | - | - | 0,7821 |

---

**Versão**: 1.0  
**Data**: 2025-10-25  
**Status**: Completo
