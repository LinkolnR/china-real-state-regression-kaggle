# Metricas de Desempenho

## Introducao

Quatro metricas padronizadas sao utilizadas para avaliar os modelos de forma consistente.

## RMSE (Root Mean Squared Error)

### Formula

```
RMSE = sqrt( (1/n) * sum( (y_true - y_pred)^2 ) )
```

### Interpretacao

- Erro medio penalizando desvios grandes
- Mesma escala da variavel alvo
- Menor e melhor

### Exemplo

Se RMSE = 7.547, o modelo erra em media por 7.547 unidades (em escala linear).

## MAE (Mean Absolute Error)

### Formula

```
MAE = (1/n) * sum( |y_true - y_pred| )
```

### Interpretacao

- Erro tipico, robusto a outliers
- Mesma escala da variavel alvo
- Menor e melhor

### Vantagem vs RMSE

- MAE e menos sensível a valores extremos
- Mais compreensível: "erro tipico"

## R2 (Coeficiente de Determinacao)

### Formula

```
R2 = 1 - (SS_res / SS_tot)

onde:
SS_res = sum( (y_true - y_pred)^2 )
SS_tot = sum( (y_true - media(y))^2 )
```

### Interpretacao

- Proporcao da variancia explicada pelo modelo
- Intervalo tipico [0, 1]
- Maior e melhor
- Permite comparacao universal (independente de escala)

### Exemplos

| R2 | Significado |
|----|-------------|
| 0,97 | Modelo explica 97% da variancia (excelente) |
| 0,80 | Modelo explica 80% da variancia (bom) |
| 0,50 | Modelo explica 50% da variancia (modesto) |
| 0,00 | Modelo nao e melhor que predizer a media |

## Competition Score (Metrica Customizada)

### Conceito

Baseado em Absolute Percentage Error (APE) com penalizacoes:

```python
APE = |y_true - y_pred| / |y_true|

Regras:
1. Se > 30% das predicoes tem APE > 1.0: score = 0
2. Senao: score = 1 - (MAPE das predicoes com APE <= 1.0)
```

### Interpretacao

- Metrica especifica da competicao
- Prioriza acuracia em predicoes dentro de 100% de erro
- Penaliza severamente grandes desvios percentuais
- Intervalo [0, 1], maior e melhor

### Vantagem

- Apropriada para mercados com variacao em escala
- Nao penaliza erros pequenos em numeros grandes

## Comparacao Entre Metricas

| Metrica | Escala | Interpretacao | Melhor Para |
|---------|--------|---------------|------------|
| RMSE | Mesma variavel | Penaliza grandes erros | Detectar outliers |
| MAE | Mesma variavel | Erro tipico | Interpretabilidade geral |
| R2 | [0,1] | % variancia explicada | Comparacao universal |
| Competition Score | [0,1] | Especifico dominio | Competicao |

## Uso Recomendado

Para comparacao independente da competicao:

1. **Priorize R2**: Comparavel entre contextos diferentes
2. **Use RMSE**: Interpretacao em unidades originais
3. **Valide com MAE**: Robustez a outliers

---

**Proxima Secao**: [Comparacao dos Modelos](comparison.md)
