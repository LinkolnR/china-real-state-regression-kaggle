# Relatorio de Comparacao

## Resumo

Analise da evolucao de v1, v2 e v3, impactos de engenharia de features, validacao e busca de hiperparametros.

## Comparacao Tecnica

### v1: Linha de base
- MLP simples, validacao temporal
- Sem lags ou medias moveis

### v2: Melhoria significativa
- Lags, medias moveis, interacoes, features temporais
- GroupKFold por setor
- Diagnosticos e metricas por fold

### v3: Otimizacao de hiperparametros
- Grid reduzido com multiplos seeds
- Safe MSE e clipping para estabilidade
- Validacao TimeSeriesSplit

## Tabela comparativa

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| Features | Basicas | 27 (lags/MA) | 27 |
| Validacao | TimeSeriesSplit | GroupKFold | TimeSeriesSplit+Seeds |
| Arquitetura | Fixa (256,128,64) | Fixa | Busca automatica |
| Protecao Numerica | Nao | Nao | Sim |
| Tempo de Treino | ~10 min | ~15 min | ~2-3 horas |

## Ganhos esperados

- v1 -> v2: +15 a 25 por cento
- v2 -> v3: +5 a 15 por cento (dependente de configuracao)

## Conclusao

- v2 e recomendado para producao pelo equilibrio entre desempenho, estabilidade e simplicidade
- v3 pode ser explorado para competicoes ou cenarios onde maior tempo de treino e aceitavel
