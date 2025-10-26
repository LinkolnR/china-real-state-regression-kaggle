# Comparacao dos Modelos

## Visao Geral

Analise comparativa detalhada entre v1, v2 e v3 usando multiplas dimensoes.

## Resultados Numericos

### Metricas Principais

| Modelo | RMSE | MAE | MSE | R² | Competition Score |
|--------|------|-----|-----|----|--------------------|
| v1 | 38.937,57 | 13.565,70 | - | 0,5513 | - |
| v2 | 7.547,03 | 1.626,75 | - | 0,9763 | 0,9530 |
| v3 | 19.991,72 | 863,65 | 399.669.007 | 0,9942 | 0,7821 |

### Ganhos de Desempenho

#### v1 → v2
- RMSE: 38.937,57 → 7.547,03 (-80,6%)
- MAE: 13.565,70 → 1.626,75 (-88,0%)
- R²: 0,5513 → 0,9763 (+77,1pp)

#### v1 → v3
- RMSE: 38.937,57 → 19.991,72 (-48,6%)
- MAE: 13.565,70 → 863,65 (-93,6%)
- R²: 0,5513 → 0,9942 (+44,3pp)
- Competition Score: - → 0,7821

#### v2 → v3
- RMSE: 7.547,03 → 19.991,72 (+165%) PIORA
- MAE: 1.626,75 → 863,65 MELHORA (-47%)
- R²: 0,9763 → 0,9942 (+0,18pp) MELHORA
- Competition Score: 0,9530 → 0,7821 (-17,1pp) PIORA

### Paradoxo de v3: R² Alta vs RMSE Ruim

A situação de v3 é peculiar:
- R² aumenta de 0,9763 (v2) para 0,9942 (v3)
- MAE melhora de 1.626,75 (v2) para 863,65 (v3)
- MAS RMSE piora drasticamente de 7.547,03 (v2) para 19.991,72 (v3)
- E Competition Score cai de 0,9530 (v2) para 0,7821 (v3)

**Explicação**: OVERFITTING severo
- O modelo v3 ajusta perfeitamente aos dados de treino
- Mas quando prediz dados novos (teste), erra muito
- A métrica R² é insensível a este tipo de erro em séries temporais

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
