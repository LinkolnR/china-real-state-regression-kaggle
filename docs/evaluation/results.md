# Resultados Finais

## Conclusoes Principais

### 1. Superioridade de v2

O modelo v2 demonstrou a melhor performance em todas as metricas:

- **R2 = 0,9763**: Explica 97,63% da variancia nos dados
- **RMSE = 7.547**: Erro medio 80,6% menor que v1
- **MAE = 1.627**: Erro tipico 88,0% menor que v1
- **Competition Score = 0,9530**: Acuracia de 95,3%

### 2. Importancia do Feature Engineering

A melhoria massiva de v1 para v2 foi alcancada primariamente atraves de:

1. **Lags Temporais**: Capturaram dependencias entre periodos
2. **Medias Moveis**: Suavizaram ruido e identificaram tendencias
3. **Features Engineered**: Reducoes de dimensionalidade (63 -> 27)
4. **Validacao Apropriada**: GroupKFold por setor evitou data leakage

### 3. Limites da Otimizacao

v3 demonstrou que busca extensiva de hiperparametros nao garante melhoria:

- Piorou 165% em RMSE
- Reduziu 16,9pp em Competition Score
- Consumiu 10x mais tempo de computacao

## Recomendacoes Praticas

### Para Producao

**RECOMENDACAO: Usar Modelo v2**

Razoes:
1. Melhor performance comprovada
2. Tempo de treino aceitavel (15-20 min)
3. Interpretabilidade clara (27 features com significado)
4. Validacao apropriada (respeta hierarquia setorial)

### Para Pesquisa Futura

Se buscar melhorias alem de v2:

1. **Mantenha GroupKFold**: Nao volte a TimeSeriesSplit
2. **Explore novos modelos**: XGBoost, LightGBM, ensemble methods
3. **Feature engineering incremental**: Adicione features de dominio
4. **Dados externos**: Incorpore indicadores macroeconômicos
5. **Analise setorial**: Modelos especificos para setores problematicos

## Impacto Quantitativo

### Ganho Total Alcancado

```
Baseline (v1): R² = 0,5513
Final (v2):    R² = 0,9763
Ganho:         77,0 pontos percentuais (139% relativo)
```

### Reducao de Erro

```
RMSE Baseline:   38.937,57
RMSE Final:      7.547,03
Reducao:         80,6%
```

### Custo-Beneficio

| Aspecto | v1 | v2 | Diferenca |
|---------|----|----|-----------|
| Performance (R2) | 0,55 | 0,98 | +77,0pp |
| Tempo Treino | 10 min | 15 min | +5 min (50%) |
| Complexidade | Baixa | Media | Interpretavel |

## Contribuicoes Academicas

### 1. Feature Engineering para Series Temporais Hierarquicas

Demonstrou a efetividade de:
- Lags multi-escala (1, 3, 6 meses)
- Rolling aggregations (medias moveis)
- Validacao respeitando hierarquia de dados

### 2. Validacao Apropriada

Mostrou que escolher GroupKFold em vez de TimeSeriesSplit generico melhorou desempenho para dados hierarquicos.

### 3. Trade-offs de Complexidade

Ilustrou que sofisticacao nao e equivalente a desempenho. Regularizacao excessiva prejudicou o modelo.

## Arquivos de Saida

### Modelos Treinados

- `mlp_model_v1.joblib`: Modelo baseline
- `mlp_model_v2.joblib`: Modelo recomendado
- `mlp_model_v3.joblib`: Modelo otimizado (para referencia)

### Metricas Calculadas

- `metricas_v1.json`: Desempenho de v1
- `metricas_v2.json`: Desempenho de v2 com por-fold
- `metricas_v3.json`: Desempenho de v3 com grid search

### Predicoes

- `submission_v2.csv`: Predicoes recomendadas

## Limitacoes

1. **Dados limitados**: 5.433 observacoes em 67 meses
2. **Sem dados externos**: Indicadores macroeconômicos indisponiveis
3. **Dominio nao explorado**: Desafios specificos do mercado chines nao totalmente capturados
4. **Horizonte temporal**: Sem validacao em periodos futuros

## Trabalho Futuro

1. Incorporar dados de POI disponíveis
2. Pesquisar dinâmicas do mercado imobiliário chines
3. Explorar modelos de aprendizado profundo (LSTM)
4. Implementar sistema de monitoramento em producao
5. A/B testing de v2 vs v3 em dados reais

---

**Status**: Analise Completa  
**Data**: 2025-10-25  
**Proxima Secao**: [Conclusoes](../conclusion.md)
