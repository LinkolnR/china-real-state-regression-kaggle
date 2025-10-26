# Modelos de Training - Visao Geral

## Abordagem Geral

Foram desenvolvidas tres versoes de modelos MLPRegressor (redes neurais artificiais) com aumentando complexidade e sofisticacao.

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| Features | 63 basicas | 27 engineered | 27 engineered |
| Validacao | TimeSeriesSplit | GroupKFold | TimeSeriesSplit + Seeds |
| Arquitetura | Fixa | Fixa | Busca automatica |
| Tempo Treino | ~10 min | ~15 min | ~2-3 horas |

## Arquitetura Base (MLP)

```
Entrada (N features)
  |
  v
Camada Oculta 1: 256 neuronios (ReLU/Tanh)
  |
  v
Camada Oculta 2: 128 neuronios (ReLU/Tanh)
  |
  v
Camada Oculta 3: 64 neuronios (ReLU/Tanh)
  |
  v
Saida (1 neuronio - regressao)
```

## Mecanismo de Validacao

### v1: TimeSeriesSplit

- Respeita ordem temporal
- Sem data leakage entre treino/teste
- Menos adequado para dados hierarquicos

### v2: GroupKFold

- Agrupa por setor (sector_id)
- Garante representacao de todos os 95 setores
- Evita data leakage setorial
- 5 folds balanceados

### v3: TimeSeriesSplit + Multiple Seeds

- Validação temporal 
- 3 seeds distintos (42, 123, 456)
- Avalia robustez e reproducibilidade

## Transformacoes de Dados

- **Alvo**: log1p(amount_new_house_transactions)
- **Reverso para predicoes**: expm1(predicoes)
- **Features**: StandardScaler normaliza para media 0, desvio 1

## Comparacao Resumida

| Modelo | Validacao | Features | RMSE | MAE | R² | Competition Score |
|--------|-----------|----------|------|-----|----|--------------------|
| v1 | TimeSeriesSplit | 27 | 38.937,57 | 13.565,70 | 0,5513 | - |
| v2 | GroupKFold | 27 + lags | 7.547,03 | 1.626,75 | 0,9763 | 0,9530 |
| v3 | TimeSeriesSplit | 27 | 19.991,72 | 863,65 | 0,9942 | 0,7821 |

**Resultado Final:** v2 é superior em métrica de competição e generalização, apesar de v3 ter R² mais alta (OVERFITTING).

---

Proximas secoes:
- [Modelo v1 - Baseline](v1.md)
- [Modelo v2 - Feature Engineering](v2.md)
- [Modelo v3 - Otimizacao](v3.md)
