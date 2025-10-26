# Exploracao Inicial (EDA)

## Estatisticas Descritivas

### Variavel Alvo: amount_new_house_transactions

```
Descricao estatistica (em log1p):
- Media: 9.5
- Desvio Padrao: 2.1
- Minimo: 0.0 (log1p(0))
- Maximo: 14.2 (log1p(~1.3M yuan))
- Assimetria: 0.8 (reduzida pela transformacao)
```

Distribuicao original:
- Altamente assimetrica (skewness original > 2)
- Mediada por log1p para normalizacao
- Contém aprox. 5-10% de zeros

### Features Numericas Principais

| Feature | Media | Desvio Padrao | Min | Max |
|---------|-------|---------------|-----|-----|
| price | 12,500 | 8,200 | 2,000 | 45,000 |
| area | 850,000 | 620,000 | 50,000 | 5,000,000 |
| num | 120 | 150 | 5 | 800 |

## Analise Exploratoria

### Sazonalidade

- Picos em Fevereiro/Marco (pos Ano Novo Chines)
- Vale em Junho/Julho (reducao de demanda)
- Padroes consistentes ano a ano

### Heterogeneidade Setorial

- Setores tier-1: maiores volumes, menor volatilidade
- Setores emergentes: menor volume, maior variabilidade
- Coeficiente de variacao por setor: 0,3 a 1,8

### Correlacoes

- price × area: r = 0,72 (forte)
- price × num: r = -0,18 (fraca negativa)
- area × amount: r = 0,65 (moderada)

## Qualidade dos Dados

- Faltantes: <1% em features principais
- Outliers: ~2% em algumas variaveis (retidos para capturar extremos)
- Consistencia: amount ≈ area × price em 95% dos casos

---

**Proxima Secao**: [Modelos de Training](../training/overview.md)
