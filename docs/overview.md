# Resumo Executivo

A evolução dos modelos de previsão de demanda imobiliária demonstra que o modelo v2 é o melhor candidato para produção. Ele representa uma melhoria substancial em relação ao baseline v1, enquanto o modelo v3, apesar de buscar hiperparâmetros, não superou o v2 em consistência e métricas principais.

## Comparação rápida

```
                    v1              v2              v3
                    -------------------------------
RMSE                38.937,57  ->   7.547,03   ->  19.991,72
MAE                 13.565,70  ->   1.626,75   ->  (não reportado)
$R^2$                  0,5513     ->   0,9763     ->  (não reportado)
Comp. Score         (N/A)      ->   0,9530     ->  0,7821

Features            63              27              27
Validação           TimeSeries      GroupKFold      TimeSeries
Hiperparâmetros     Fixo            Fixo            Otimizado (36)

Recomendação        Não             USAR ESTE       Não
```

## Métricas principais

- RMSE: v1 -> v2 reduz em 80,6%; v2 -> v3 piora
- MAE: v1 -> v2 reduz em 88,0%
- $R^2$: v2 explica 97,63% da variância
- Competition Score: v2 = 0,9530; v3 = 0,7821

## Por que o v2 é superior

1. Feature Engineering específico para séries temporais (defasagens, médias móveis, interações)
2. Validação por setor (GroupKFold), apropriada para dados hierárquicos
3. Arquitetura equilibrada e hiperparâmetros estáveis

## Por que o v3 não superou o v2

1. Mudança de validação para TimeSeriesSplit (menos adequada ao problema)
2. Regularização maior levou a possível underfitting
3. Busca de hiperparâmetros não generalizou

## Recomendação

Usar o modelo v2 em produção. Melhorias futuras devem focar em dados, features e modelos alternativos (p. ex., gradient boosting ou ensembles), não apenas em hiperparâmetros do MLP.
