## Métricas de Desempenho

## Introdução

Este documento padroniza as métricas usadas para avaliar os modelos e orienta a interpretação de resultados.

## RMSE (Root Mean Squared Error)

Fórmula:
$$
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_{\text{true}} - y_{\text{pred}})^2}
$$

- Penaliza erros grandes
- Mesma escala da variável alvo
- Menor é melhor

## MAE (Mean Absolute Error)

Fórmula:
$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_{\text{true}} - y_{\text{pred}}|
$$

- Erro típico, robusto a outliers
- Mesma escala da variável alvo
- Menor é melhor

## $R^2$ (Coeficiente de Determinação)

Fórmula:
$$
R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}
$$

- Proporção da variância explicada
- Intervalo típico [0, 1]
- Maior é melhor

## Competition Score (métrica customizada)

Pseudo-código:
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

- Específica do domínio da competição
- Intervalo [0, 1]
- Maior é melhor

## Como comparar modelos sem a competição

- Priorize $R^2$ para comparação universal
- Use RMSE e MAE para interpretar a magnitude e robustez do erro
- Avalie a estabilidade entre folds (desvio padrão das métricas)

## Tabela de referência

| Métrica | Escala | Melhor |
|---------|--------|--------|
| RMSE | Mesma da variável | Menor |
| MAE | Mesma da variável | Menor |
| $R^2$ | [0,1] | Maior |
| Competition Score | [0,1] | Maior |
