# Modelos de Training - Visão Geral

## Abordagem Geral

Foram desenvolvidas três versões de modelos MLPRegressor (redes neurais artificiais) com complexidade e sofisticação crescentes.

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| Features | 63 básicas | 27 engineered | 27 engineered |
| Validação | TimeSeriesSplit | GroupKFold | TimeSeriesSplit + Seeds |
| Arquitetura | Fixa | Fixa | Busca automática |
| Tempo Treino | ~10 min | ~15 min | ~2-3 horas |

## Arquitetura Base (MLP)

```
Entrada (N features)
  |
  v
Camada Oculta 1: 256 neurônios (ReLU/Tanh)
  |
  v
Camada Oculta 2: 128 neurônios (ReLU/Tanh)
  |
  v
Camada Oculta 3: 64 neurônios (ReLU/Tanh)
  |
  v
Saída (1 neurônio - regressão)
```

## Mecanismo de Validação

### v1: TimeSeriesSplit

- Respeita ordem temporal
- Sem data leakage entre treino/teste
- Menos adequado para dados hierárquicos

### v2: GroupKFold

- Agrupa por setor (sector_id)
- Garante representação de todos os 95 setores
- Evita data leakage setorial
- 5 folds balanceados

### v3: TimeSeriesSplit + Multiple Seeds

- Validação temporal 
- 3 seeds distintos (42, 123, 456)
- Avalia robustez e reprodutibilidade

## Transformações de Dados

- **Alvo**: log1p(amount_new_house_transactions)
- **Reverso para predições**: expm1(predições)
- **Features**: StandardScaler normaliza para média 0, desvio 1

## Comparação Resumida

| Modelo | Validação | Features | RMSE | MAE | R² | Competition Score |
|--------|-----------|----------|------|-----|----|--------------------|
| v1 | TimeSeriesSplit | 27 | 38.937,57 | 13.565,70 | 0,5513 | - |
| v2 | GroupKFold | 27 + lags | 7.547,03 | 1.626,75 | 0,9763 | 0,9530 |
| v3 | TimeSeriesSplit | 27 | 19.991,72 | 863,65 | 0,9942 | 0,7821 |

**Resultado Final:** v2 é superior em métrica de competição e generalização, apesar de v3 ter R² mais alta (OVERFITTING).

---

Próximas seções:
- [Modelo v1 - Baseline](v1.md)
- [Modelo v2 - Feature Engineering](v2.md)
- [Modelo v3 - Otimização](v3.md)
