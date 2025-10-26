# Contexto do Projeto

## Disciplina

**Artificial Neural Networks and Deep Learning - Redes Neurais (2025.2)**  
**Projeto 2: Regressão com MLP**

## Competição Kaggle

### Informações Gerais

- **Nome**: Real Estate Demand Prediction Challenge
- **Plataforma**: Kaggle
- **Período**: 3 meses de duração
- **Status**: Em andamento

## Objetivo Principal

Desenvolver um modelo de regressão neural (MLP) que prevê o volume mensal de transações de propriedades residenciais no mercado chinês para cada setor, usando dados históricos de 2019 a 2024.

## Dados e Granularidade

### Cobertura

- **Período**: Janeiro 2019 a Julho 2024 (67 meses)
- **Setores**: 95 setores distintos
- **Observações**: 5.433 registros (setor + mês)
- **Variável Alvo**: new_house_transaction_amount (em 10 mil Yuan)

## Métrica de Avaliação (Kaggle)

### Estratégia em Duas Etapas

#### Estágio 1

Se mais de 30% das amostras tiverem erro percentual absoluto (APE) > 100%:
- Score = 0 imediatamente

#### Estagio 2

Caso contrário, calcula-se MAPE apenas para predições com APE ≤ 100%:

$$
D = \\left\\{\frac{|y_i^{pred} - y_i^{true}|}{|y_i^{true}|} : \text{APE} \leq 1\\right\\}
$$

$$
\text{Score} = 1 - \frac{\text{average}(D)}{|D| / n}
$$

### Metricas de Regressão (Projeto)

Para avaliação do projeto, calcular:

- **MAE** (Mean Absolute Error): Erro médio absoluto
- **MAPE** (Mean Absolute Percentage Error): Erro percentual absoluto médio
- **MSE** (Mean Squared Error): Erro quadrático médio
- **RMSE** (Root Mean Squared Error): Raiz do erro quadrático médio
- **$R^2$** (Coeficiente de Determinação): Proporção de variância explicada

## Formato de Submissão (Kaggle)

### Arquivo Requerido

Nome: submission.csv

Colunas:

- `id`: Formato "YYYY MMM_sector N" (ex: "2024 Aug_sector 1")
- `new_house_transaction_amount`: Valor predito em 10 mil Yuan

### Requisitos

- Preservar ordem exata de test.csv
- Incluir header
- Arquivo CSV com exatamente 2 colunas

## Desafios Principais

### 1. Distribuição Temporal Complexa

O mercado imobiliário chinês apresenta padrões sazonais:

- Picos durante festas nacionais (Ano Novo Chinês)
- Variação por cidade e tier (tier-1, tier-2, etc.)
- Efeitos de políticas governamentais de controle de preço

### 2. Heterogeneidade Geográfica

95 setores com dinâmicas próprias:

- Mercados consolidados vs emergentes
- Variações significativas em preço, volume e tendências
- Necessidade de validação respeitando estrutura hierárquica

### 3. Escalas e Distribuições

- Variável alvo altamente assimétrica
- Valores variando em múltiplas ordens de magnitude
- Presença de zeros legítimos (períodos sem transações)

### 4. Dados Externos Limitados

- Indicadores macroeconômicos indisponíveis
- Dados de POI (Point of Interest) em sua maioria ausentes
- Conhecimento específico do mercado chinês necessário

## Solução Proposta

### Abordagem em Três Versões

1. **v1 - Baseline**: MLP simples para estabelecer referência
2. **v2 - Feature Engineering**: Lags, médias móveis e validação por setor
3. **v3 - Otimização**: Busca sistemática de hiperparâmetros

### Arquitetura

Todas as versões usam MLPRegressor (redes neurais artificiais) com 3 camadas ocultas.


---

**Próxima Seção**: [Dataset e Preparação](../dataset/overview.md)
