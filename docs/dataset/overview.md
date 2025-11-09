# Descrição dos Dados

## Fonte e Escopo

Os dados foram coletados do mercado imobiliário chinês, cobrindo transações de propriedades residenciais no período de janeiro de 2019 a julho de 2024.

### Granularidade

- Nível de agregação: Setor (sector_id) + Mês (period)
- Total de observações: 5.433 registros
- Setores distintos: 95
- Período temporal: 67 meses

## Variáveis Principais

### Alvo (Target)

**amount_new_house_transactions**:

- Volume de transações de propriedades novas (em 10k yuan)
- Altamente assimétrica (skewness > 2)
- Contém zeros (períodos sem transações)
- Transformação log1p aplicada durante modelagem

### Features Originais (Básicas)

- price: Preço médio por m²
- area: Área construída total
- num: Número de unidades

### Agregações Temporais

- month: Mês do ano (1-12)
- quarter: Trimestre (1-4)
- year: Ano

### Indicadores de POI e Macroeconômicos

- Dados de Points of Interest (POI) para comércio e serviços
- Índices macroeconômicos (em sua maioria com dados faltantes)

## Preparação dos Dados

### Limpeza

- Remoção de registros com datas inválidas
- Verificação de consistência (amount ≈ area × price)
- Tratamento de valores anomalos

### Transformações

- Log1p na variável alvo para normalizar distribuição
- StandardScaler nas features numéricas
- Encoding ordinal para variáveis categóricas

---

**Próxima Seção**: [Exploração Inicial](eda.md)
