# Resumo Executivo

A evolucao dos modelos de previsao de demanda imobiliaria demonstra que o modelo v2 e o melhor candidato para producao. Ele representa uma melhoria substancial em relacao ao baseline v1, enquanto o modelo v3, apesar de buscar hiperparametros, nao superou v2 em consistencia e metricas principais.

## Comparacao rapida

```
                    v1              v2              v3
                    -------------------------------
RMSE                38.937,57  ->   7.547,03   ->  19.991,72
MAE                 13.565,70  ->   1.626,75   ->  (nao reportado)
R2                  0,5513     ->   0,9763     ->  (nao reportado)
Comp. Score         (N/A)      ->   0,9530     ->  0,7821

Features            63              27              27
Validacao           TimeSeries      GroupKFold      TimeSeries
Hiperparametros     Fixo            Fixo            Otimizado (36)

Recomendacao        Nao             USAR ESTE       Nao
```

## Metricas principais

- RMSE: v1 -> v2 reduz em 80,6%; v2 -> v3 piora
- MAE: v1 -> v2 reduz em 88,0%
- R2: v2 explica 97,63% da variancia
- Competition Score: v2 = 0,9530; v3 = 0,7821

## Por que v2 e superior

1. Feature Engineering especifico para series temporais (lags, medias moveis, interacoes)
2. Validacao por setor (GroupKFold), apropriada para dados hierarquicos
3. Arquitetura equilibrada e hiperparametros estaveis

## Por que v3 nao superou v2

1. Mudanca de validacao para TimeSeriesSplit (menos adequada ao problema)
2. Regularizacao maior levou a possivel underfitting
3. Busca de hiperparametros nao generalizou

## Recomendacao

Usar o modelo v2 em producao. Melhorias futuras devem focar em dados, features e modelos alternativos (p. ex., gradient boosting ou ensembles), nao apenas em hiperparametros do MLP.
