# Descrição dos Dados

## Fonte e Escopo

Os dados foram coletados do mercado imobiliário chinês, cobrindo transações de propriedades residenciais no periodo de janeiro de 2019 a julho de 2024.

### Granularidade

- Nivel de agregacao: Setor (sector_id) + Mes (period)
- Total de observacoes: 5.433 registros
- Setores distintos: 95
- Periodo temporal: 67 meses

## Variáveis Principais

### Alvo (Target)

**amount_new_house_transactions**:

- Volume de transações de propriedades novas (em 10k yuan)
- Altamente assimetrica (skewness > 2)
- Contem zeros (periodos sem transações)
- Transformacao log1p aplicada durante modelagem

### Features Originais (Basicas)

- price: Preco medio por m²
- area: Area construida total
- num: Numero de unidades

### Aggregacoes Temporais

- month: Mes do ano (1-12)
- quarter: Trimestre (1-4)
- year: Ano

### Indicadores de POI e Macroeconômicos

- Dados de Points of Interest (POI) para comercio e servicos
- Indices macroeconômicos (em sua maioria com dados faltantes)

## Preparação dos Dados

### Limpeza

- Remoção de registros com datas inválidas
- Verificação de consistência (amount ≈ area × price)
- Tratamento de valores anomalos

### Transformações

- Log1p na variavel alvo para normalizar distribuicao
- StandardScaler nas features numericas
- Encoding ordinal para variaveis categoricas

---

**Proxima Secao**: [Exploracao Inicial](eda.md)
