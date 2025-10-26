# Relatório de Comparação

## Resumo

Análise da evolução de v1, v2 e v3, impactos de engenharia de features, validação e busca de hiperparâmetros.

## Comparação Técnica

### v1: Linha de base
- MLP simples, validação temporal
- Sem defasagens ou médias móveis

### v2: Melhoria significativa
- Defasagens, médias móveis, interações, features temporais
- GroupKFold por setor
- Diagnósticos e métricas por fold

### v3: Otimização de hiperparâmetros
- Grade reduzida com múltiplos seeds
- Safe MSE e clipping para estabilidade
- Validação TimeSeriesSplit

## Tabela comparativa

| Aspecto | v1 | v2 | v3 |
|---------|----|----|-----|
| Features | Básicas | 27 (defasagens/MA) | 27 |
| Validação | TimeSeriesSplit | GroupKFold | TimeSeriesSplit+Seeds |
| Arquitetura | Fixa (256,128,64) | Fixa | Busca automática |
| Proteção Numérica | Não | Não | Sim |
| Tempo de Treino | ~10 min | ~15 min | ~2-3 horas |

## Ganhos esperados

- v1 -> v2: +15 a 25 por cento
- v2 -> v3: +5 a 15 por cento (dependente de configuração)

## Conclusão

- v2 é recomendado para produção pelo equilíbrio entre desempenho, estabilidade e simplicidade
- v3 pode ser explorado para competições ou cenários onde maior tempo de treino é aceitável
