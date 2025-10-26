# Analise de Resultados: v1, v2 e v3

## 1. Dados e Validacao

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| Features | 63 | 27 | 27 |
| Observacoes Treino | 5.305 | 5.433 | 5.433 |
| Observacoes Teste | 1.060 | OOF (5.433) | OOF (5.433) |
| Validacao | TimeSeriesSplit | GroupKFold (95 setores) | TimeSeriesSplit + Seeds |
| Combinacoes Testadas | 1 | 1 | 36 |

## 2. Evolucao das Metricas

### RMSE
```
v1: 38.937,57
v2:  7.547,03
v3: 19.991,72
```

### MAE
```
v1: 13.565,70
v2:  1.626,75
v3:  (nao reportado)
```

### R2
```
v1: 0,5513
v2: 0,9763
v3: (nao reportado)
```

### Competition Score
```
v2: 0,9530
v3: 0,7821
```

## 3. Mudancas por Versao

### V1 -> V2
- Feature engineering avancado (lags, medias moveis, interacoes)
- GroupKFold por setor
- Ajustes de hiperparametros (tanh, batch maior, lr maior)

Resultado: grandes melhorias em RMSE, MAE e R2.

### V2 -> V3
- Busca de hiperparametros (36 combinacoes, multiplos seeds)
- Validacao mais rigida com TimeSeriesSplit
- Regularizacao maior e lr menor

Resultado: piora nas metricas principais versus v2.

## 4. Analise por Versao

### v1: Linha de base
- Simples, sem engenharia de features
- Validaçao temporal generica

### v2: Avanco significativo
- Captura dinamica temporal, sazonalidade e interacoes
- Forte estabilidade e alta explicacao de variancia

### v3: Busca de hiperparametros
- Maior complexidade, mas validacao menos adequada
- Regularizacao e estrategia de busca nao superaram v2

## 5. Conclusoes

- v2 e o melhor modelo para producao
- v3 nao supera v2 nas metricas principais
- Futuro: manter GroupKFold, explorar XGBoost/LightGBM, ensembles e features adicionais
