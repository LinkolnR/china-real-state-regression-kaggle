# Descricao dos Dados

## Fonte e Escopo

Os dados foram coletados do mercado imobiliario chines, cobrindo transacoes de propriedades residenciais no periodo de janeiro de 2019 a julho de 2024.

### Granularidade

- Nivel de agregacao: Setor (sector_id) + Mes (period)
- Total de observacoes: 5.433 registros
- Setores distintos: 95
- Periodo temporal: 67 meses

## Variaveis Principais

### Alvo (Target)

**amount_new_house_transactions**: Volume de transacoes de propriedades novas (em 10k yuan)
- Altamente assimetrica (skewness > 2)
- Contem zeros (periodos sem transacoes)
- Transformacao log1p aplicada durante modelagem

### Features Originais (Basicas)

- price: Preco medio por m²
- area: Area construida total
- num: Numero de unidades

### Aggregacoes Temporais

- month: Mes do ano (1-12)
- quarter: Trimestre (1-4)
- year: Ano

### Indicadores de POI e Macroeconomicos

- Dados de Points of Interest (POI) para comercio e servicos
- Indices macroeconômicos (em sua maioria com dados faltantes)

## Preparacao dos Dados

### Limpeza

- Remocao de registros com datas invalidas
- Verificacao de consistencia (amount ≈ area × price)
- Tratamento de valores anomalos

### Transformacoes

- Log1p na variavel alvo para normalizar distribuicao
- StandardScaler nas features numericas
- Encoding ordinal para variaveis categoricas

---

**Proxima Secao**: [Exploracao Inicial](eda.md)
