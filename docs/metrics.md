# Metricas de Desempenho

## Introducao

Este documento padroniza as metricas usadas para avaliar os modelos e orienta a interpretacao de resultados.

## RMSE (Root Mean Squared Error)

Formula:
```
RMSE = sqrt( (1/n) * sum( (y_true - y_pred)^2 ) )
```

- Penaliza erros grandes
- Mesma escala da variavel alvo
- Menor e melhor

## MAE (Mean Absolute Error)

Formula:
```
MAE = (1/n) * sum( |y_true - y_pred| )
```

- Erro tipico, robusto a outliers
- Mesma escala da variavel alvo
- Menor e melhor

## R2 (Coeficiente de Determinacao)

Formula:
```
R2 = 1 - (SS_res / SS_tot)
```

- Proporcao da variancia explicada
- Intervalo tipico [0, 1]
- Maior e melhor

## Competition Score (métrica customizada)

Pseudo-codigo:
```python
import numpy as np

def competition_score(y_true, y_pred):
    den = np.where(np.abs(y_true) < 1e-9, 1.0, np.abs(y_true))
    ape = np.abs(y_true - y_pred) / den
    frac_le1 = float(np.mean(ape <= 1.0))
    if 1.0 - frac_le1 > 0.30:
        return {"score": 0.0, "frac_le1": frac_le1, "scaled_mape": float('inf')}
    mask = ape <= 1.0
    if not np.any(mask):
        return {"score": 0.0, "frac_le1": 0.0, "scaled_mape": float('inf')}
    mape_subset = float(np.mean(ape[mask]))
    scaled_mape = float(mape_subset / max(frac_le1, 1e-12))
    return {"score": float(1.0 - scaled_mape), "frac_le1": frac_le1, "scaled_mape": scaled_mape}
```

- Especifica do dominio da competicao
- Intervalo [0, 1]
- Maior e melhor

## Como comparar modelos sem a competicao

- Priorize R2 para comparacao universal
- Use RMSE e MAE para interpretar magnitude e robustez do erro
- Avalie estabilidade entre folds (desvio padrao das metricas)

## Tabela de referencia

| Metrica | Escala | Melhor |
|---------|--------|--------|
| RMSE | Mesma da variavel | Menor |
| MAE | Mesma da variavel | Menor |
| R2 | [0,1] | Maior |
| Competition Score | [0,1] | Maior |
