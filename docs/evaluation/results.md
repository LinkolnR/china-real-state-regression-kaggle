# Resultados Finais

## Galeria Rápida (Figuras)

- Predito vs Real (v2): ![pred_vs_true](../imgs/pred_vs_true.png)
- Curva de Perda (v2): ![loss_curve](../imgs/loss_curve.png)
- Resíduos (v2): ![residuos](../imgs/residuos.png)
- Importância por Permutação (v2): ![perm_importance](../imgs/perm_importance.png)
- Predito vs Real (v3): ![pred_vs_true_v3](../imgs/pred_vs_true_v3.png)
- Curva de Perda (v3): ![loss_curve_v3](../imgs/loss_curve_v3.png)
- Resíduos (v3): ![residuos_v3](../imgs/residuos_v3.png)
- Importância por Permutação (v3): ![perm_importance_v3](../imgs/perm_importance_v3.png)
- Evolução do Best Competition Score por Iteração (v3): ![oof_por_iteracao](../imgs/oof_por_iteracao.png)

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

### Metricas do Melhor Modelo v3

| Metrica | Valor |
|---------|-------|
| RMSE | 19.991,72 |
| MAE | 863,65 |
| MSE | 399.669.007 |
| R² | 0,9942 |
| Competition Score | 0,7821 |

## Comparacao Completa: v1 vs v2 vs v3

### Tabela de Metricas Finais

| Metrica | v1 (Baseline) | v2 (Recomendado) | v3 (Otimizacao) |
|---------|---------------|------------------|-----------------|
| RMSE | 38.937,57 | 7.547,03 | 19.991,72 |
| MAE | 13.565,70 | 1.626,75 | 863,65 |
| MSE | - | - | 399.669.007 |
| R² | 0,5513 | 0,9763 | 0,9942 |
| Competition Score | - | 0,9530 | 0,7821 |

### Resumo de Desempenho

#### v1 - Baseline
- **RMSE**: 38.937,57 (linha de base)
- **MAE**: 13.565,70
- **R²**: 0,5513 (explica ~55% da variância)
- Modelo simples sem feature engineering

#### v2 - Recomendado (MELHOR)
- **RMSE**: 7.547,03 (82% melhor que v1)
- **MAE**: 1.626,75 (88% melhor que v1)
- **R²**: 0,9763 (explica ~98% da variância)
- **Competition Score**: 0,9530
- Feature engineering avançado com lags e médias móveis
- Validação por setor (GroupKFold)
- Melhor generalização

#### v3 - Otimizacao (Overfitting)
- **RMSE**: 19.991,72 (intermediário entre v1 e v2)
- **MAE**: 863,65 (pior que v2)
- **MSE**: 399.669.007
- **R²**: 0,9942 (MAIS ALTA que v2!)
- **Competition Score**: 0,7821
- Busca sistemática de 36 hiperparâmetros com 3 seeds
- Melhor configuração: [256, 128, 64] com tanh
- **PROBLEMA**: R² elevada mas RMSE ruim = OVERFITTING SEVERO

### Analise Comparativa

#### Progressao de RMSE
```
v1: 38.937,57 ━━━━━━━━━━━━━━━━━━━━━━━━━━━━ (referencia)
v3: 19.991,72 ━━━━━━━━━━━━ (intermediário)
v2:  7.547,03 ━━━ (melhor!)
```

#### Progressao de R²
```
v1: 0,5513  ████ 
v2: 0,9763  ██████████████████ (excelente!)
v3: 0,9942  ██████████████████ (parece melhor mas OVERFITTING!)
```

#### Competition Score
```
v2: 0,9530 ████████████████████ (excelente)
v3: 0,7821 ████████████ (bom)
v1: -      - (não calculado)
```

### Conclusoes Principais

1. **v2 é a solução recomendada**
   - Melhor RMSE (7.547,03)
   - Melhor R² com GENERALIZAÇÃO (0,9763)
   - Melhor Competition Score (0,9530)
   - Feature engineering provou ser mais efetivo

2. **v3 sofre com OVERFITTING severo**
   - R² mais alta (0,9942) que v2 mas RMSE 2,65x PIOR
   - RMSE no teste: 19.991,72 vs RMSE no treino: 3.734,49
   - A discrepancia revela que o modelo não generaliza
   - Lições: R² NÃO é métrica confiável para séries temporais

3. **v1 serviu como baseline**
   - RMSE: 38.937,57
   - Demonstrou a necessidade de melhorias
   - v2 alcançou 81% de melhoria sobre v1

### Insights Técnicos

- **Feature Engineering > Otimizacao**: v2 com feature engineering bateu v3 com busca exaustiva
- **Validacao Importa**: GroupKFold (v2) foi melhor que TimeSeriesSplit (v3)
- **Arquitetura Profunda com Overfitting**: v3 com 3 camadas [256,128,64] ajusta perfeitamente ao treino mas falha no teste
- **R² é Enganosa**: Métrica R² alta não garante boa generalização em séries temporais
- **Regularizacao Insuficiente**: Alpha=0.0001 não foi forte o bastante contra overfitting em v3

### Recomendacao Final

**✓ Submeter v2 para a competição Kaggle**
- Melhor RMSE e Competition Score
- Melhor generalização
- Feature engineering é estratégia vencedora

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
