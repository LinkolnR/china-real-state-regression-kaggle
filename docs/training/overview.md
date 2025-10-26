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

- Validacao temporal rigorosa
- 3 seeds distintos (42, 123, 456)
- Avalia robustez e reproducibilidade

## Transformacoes de Dados

- **Alvo**: log1p(amount_new_house_transactions)
- **Reverso para predicoes**: expm1(predicoes)
- **Features**: StandardScaler normaliza para media 0, desvio 1

## Resultados Resumidos

| Metrica | v1 | v2 | v3 |
|---------|----|----|-----|
| RMSE | 38,938 | 7,547 | 19,992 |
| MAE | 13,566 | 1,627 | - |
| R2 | 0,5513 | 0,9763 | - |
| Competition Score | - | 0,9530 | 0,7821 |

---

Proximas secoes:
- [Modelo v1 - Baseline](v1.md)
- [Modelo v2 - Feature Engineering](v2.md)
- [Modelo v3 - Otimizacao](v3.md)
