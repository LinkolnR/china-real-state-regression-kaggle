# Comparacao dos Modelos

## Visao Geral

Analise comparativa detalhada entre v1, v2 e v3 usando multiplas dimensoes.

## Resultados Aggregados

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| RMSE | 38.937,57 | 7.547,03 | 19.991,72 |
| MAE | 13.565,70 | 1.626,75 | - |
| R2 | 0,5513 | 0,9763 | - |
| Competition Score | - | 0,9530 | 0,7821 |

## Ganhos de Performance

### v1 -> v2: Feature Engineering

```
Melhoria RMSE:  -80,6%  (de 38.938 para 7.547)
Melhoria MAE:   -88,0%  (de 13.566 para 1.627)
Melhoria R2:    +77,0pp (de 0,55 para 0,98)
```

**Causas principais:**
1. Lags capturam dependencias temporais
2. Medias moveis suavizam ruido
3. Validacao por setor garante representacao regional

### v2 -> v3: Otimizacao

```
Piora RMSE:     +165%  (de 7.547 para 19.992)
Piora Comp Score: -16,9pp (de 0,9530 para 0,7821)
```

**Causas principais:**
1. Mudanca para TimeSeriesSplit (menos apropriado)
2. Regularizacao excessiva
3. Overfitting da busca de hiperparametros

## Estabilidade Entre Folds

### v2: Consistencia Alta

| Fold | R2 | Desvio |
|------|----|----|
| 0-4 | 0,96-0,99 | Baixo |

Variacao esperada por setor (folds com setores distintos).

### v3: Dados Incompletos

Falta de detalhe por fold em v3, mas Competition Score variava significativamente.

## Tempo de Computacao

| Modelo | Tempo Estimado |
|--------|------|
| v1 | 10-15 min |
| v2 | 15-20 min |
| v3 | 2-3 horas |

v3 nao justifica 10x mais tempo pela piora de performance.

## Analise por Dimensoes

### Feature Space

- v1: 63 features (muito ruido)
- v2: 27 features engineered (sinal/ruido otimizado)
- v3: 27 features (mesmo de v2)

**Conclusao:** Reducao de features em v2 foi acertada.

### Validacao

- v1: TimeSeriesSplit (generico)
- v2: GroupKFold por setor (apropriado) ✅
- v3: TimeSeriesSplit (volta para pior opcao)

**Conclusao:** v2 escolheu melhor metodo de validacao.

### Arquitetura

- v1: Fixa (256, 128, 64)
- v2: Fixa (256, 128, 64)
- v3: Busca 12 combinacoes

**Conclusao:** Arquitetura de v1/v2 foi suficiente.

## Diagnosticos

### Resíduos (v2)

- Distribuicao aproximadamente normal
- Sem vieses sistematicos
- Variancia aproximadamente constante

### Predito vs Real (v2)

- Pontos proximos a diagonal
- Bom ajuste em toda faixa de valores

## Interpretacao Academica

### Descoberta Principal

O feature engineering apropriado (lags, medias moveis, validacao hierarquica) produziu ganho massivo. Busca ulteriore de hiperparametros nao trouxe melhorias.

### Implicacao

Nem sempre mais sofisticacao = melhor desempenho. Escolhas fundamentais importam mais que otimizacao fina.

---

**Proxima Secao**: [Resultados Finais](results.md)
