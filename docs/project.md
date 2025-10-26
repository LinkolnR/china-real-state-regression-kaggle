# Contexto do Projeto

## Disciplina

**Artificial Neural Networks and Deep Learning - Redes Neurais (2025.2)**  
**Projeto 2: Regressão com MLP**

### Informacoes Administrativas

- **Deadline**: 19 de outubro (domingo) - commits até 23:59
- **Equipe**: 2-3 membros
- **Submissão**: GitHub Pages link via insper.blackboard.com
- **Professor**: Humberto Sandmann

## Competicao Kaggle

### Informacoes Gerais

- **Nome**: Real Estate Demand Prediction Challenge
- **Plataforma**: Kaggle
- **Periodo**: 3 meses de duracao
- **Status**: Em andamento

## Objetivo Principal

Desenvolver um modelo de regressão neural (MLP) que preve o volume mensal de transações de propriedades residenciais no mercado chinês para cada setor, usando dados históricos de 2019 a 2024.

### Impacto

- Influenciará decisões de investimento e desenvolvimento estratégico
- Ajudará a moldar o futuro do mercado imobiliário chinês
- Oportunidade de reconhecimento em painel de IA de grupo imobiliário renomado

## Dados e Granularidade

### Cobertura

- **Periodo**: Janeiro 2019 a Julho 2024 (67 meses)
- **Setores**: 95 setores distintos
- **Observacoes**: 5.433 registros (setor + mês)
- **Variavel Alvo**: new_house_transaction_amount (em 10 mil Yuan)

### Requisitos Minimos de Dataset

- Minimo de 1.000 amostras
- Minimo de 5 features (variáveis independentes)
- Dados numericos para regressao
- Rejeição automática: Boston Housing, California Housing ou datasets clássicos

## Metrica de Avaliacao (Kaggle)

### Estrategia em Dois Estapos

#### Estagio 1: Penalidade Severa

Se mais de 30% das amostras tiverem erro percentual absoluto (APE) > 100%:
- Score = 0 imediatamente

#### Estagio 2: MAPE Escalado

Caso contrário, calcula-se MAPE apenas para predições com APE ≤ 100%:

```
D = {|y_i^pred - y_i^true| / |y_i^true| : APE ≤ 1}

Score = 1 - average(D) / (|D| / n)
```

### Metricas de Regressao (Projeto)

Para avaliação do projeto, calcular:
- **MAE** (Mean Absolute Error): Erro médio absoluto
- **MAPE** (Mean Absolute Percentage Error): Erro percentual absoluto médio
- **MSE** (Mean Squared Error): Erro quadrático médio
- **RMSE** (Root Mean Squared Error): Raiz do erro quadrático médio
- **R²** (Coeficiente de Determinação): Proporção de variância explicada

## Formato de Submissao (Kaggle)

### Arquivo Requerido

Nome: submission.csv

Colunas:
- `id`: Formato "YYYY MMM_sector N" (ex: "2024 Aug_sector 1")
- `new_house_transaction_amount`: Valor predito em 10 mil Yuan

### Requisitos

- Preservar ordem exata de test.csv
- Incluir header
- Arquivo CSV com exatamente 2 colunas

## Oito Passos Obrigatorios do Projeto

### 1. Dataset Selection
- Escolher dataset público para regressão
- Fontes: Kaggle, UCI ML Repository, OpenML, data.gov
- Documentar: nome, URL, tamanho, justificativa

### 2. Dataset Explanation
- Descrever o que o dataset representa
- Listar features (entradas) e tipos (numérico, categórico)
- Identificar variável alvo (valor contínuo)
- Discutir conhecimento de domínio
- Identificar problemas potenciais (valores faltantes, outliers)

### 3. Data Cleaning and Normalization
- Lidar com valores faltantes (imputação ou remoção)
- Remover duplicatas
- Detectar e tratar outliers
- Encoding de variáveis categóricas
- Normalizar/escalar features numéricas

### 4. MLP Implementation
- Arquitetura: camada entrada, pelo menos 1 oculta, camada saída
- Funções de ativação: sigmoid, ReLU ou tanh
- Função de perda: apropriada para regressão (MSE, MAE)
- Otimizador: SGD ou variante
- Bibliotecas permitidas: TensorFlow, PyTorch, scikit-learn (ENTENDER TUDO)

### 5. Model Training
- Implementar loop de treinamento
- Forward propagation, cálculo de perda, backpropagation
- Inicialização de pesos
- Regularização se necessário (L2, dropout)

### 6. Training and Testing Strategy
- Split de dados: train/validation/test (ex: 70/15/15)
- Ou k-fold cross-validation
- Modo de treinamento: batch, mini-batch ou online
- Early stopping para evitar overfitting
- Random seeds para reproducibilidade

### 7. Error Curves and Visualization
- Plotar loss/accuracy vs epochs (treino e validação)
- Analisar convergência, overfitting/underfitting
- Discutir ajustes realizados

### 8. Evaluation Metrics
- Aplicar métricas de regressão (MAE, MAPE, MSE, RMSE, R²)
- Comparar com baselines (ex: preditor de média)
- Apresentar em tabelas e visualizações
- Discutir força/fraquezas do modelo

## Estrutura de Relatorio

### Secoes Obrigatorias

1. Dataset Selection
2. Dataset Explanation
3. Data Cleaning and Normalization
4. MLP Implementation
5. Model Training
6. Training and Testing Strategy
7. Error Curves and Visualization
8. Evaluation Metrics
9. Conclusion
10. References

### Formato

- **Entrega**: GitHub Pages
- **Link**: Submitir via insper.blackboard.com
- **Não aceitar**: Outros formatos (PDF, Word, etc.)

## Bonus: Competicao Kaggle

### Pontos Adicionais

- **+0.5**: Submissão válida em competição reconhecida (Kaggle, DrivenData, Zindi)
  - Requer prova: link, screenshot
  
- **+0.5**: Ranking no top 50% do leaderboard
  - Requer prova: link, screenshot

**Total possível com bonus**: até +1 ponto

## Rubrica de Avaliacao (10 pontos)

| Criterio | Pontos | Descricao |
|----------|--------|-----------|
| **Dataset Selection** | 1 pt | Escolha apropriada, diversa de clássicos |
| **Data Cleaning/Normalization** | 1 pt | Limpeza justificada e completa |
| **MLP Implementation** | 2 pts | Correção e originalidade |
| **Training Strategy** | 1.5 pts | Split, validação, técnicas de regularização |
| **Error Curves** | 1 pt | Visualizações apropriadas e análise |
| **Metrics and Analysis** | 1.5 pts | Cálculo correto, interpretação |
| **Report Quality** | 1 pt | Clareza, estrutura, visualizações |
| **Bonus (Competição)** | +1 pt | Submissão + top 50% |

## Restricoes e Politicas

### O que NÃO fazer

- Não usar Boston Housing, California Housing ou datasets clássicos
- Não plagiar (zero automático + ação disciplinar)
- Não perder deadline (sem exceções)

### O que e Permitido

- Usar bibliotecas: TensorFlow, PyTorch, Keras, scikit-learn
- Usar NumPy, Matplotlib, Seaborn, Pandas, SciPy
- Usar IA para auxiliar (DEVE citar e ENTENDER tudo)
- Trabalhar em equipe (2-3 membros)

## Defesa Oral

**Aviso**: Pode haver exame oral onde você deve explicar todos os detalhes do trabalho. Entender o código é obrigatório.

## Desafios Principais

### 1. Distribuicao Temporal Complexa

O mercado imobiliário chinês apresenta padrões sazonais:
- Picos durante festas nacionais (Ano Novo Chinês)
- Variação por cidade e tier (tier-1, tier-2, etc.)
- Efeitos de políticas governamentais de controle de preço

### 2. Heterogeneidade Geografica

95 setores com dinâmicas próprias:
- Mercados consolidados vs emergentes
- Variações significativas em preço, volume e tendências
- Necessidade de validação respeitando estrutura hierárquica

### 3. Escalas e Distribuicoes

- Variável alvo altamente assimétrica
- Valores variando em múltiplas ordens de magnitude
- Presença de zeros legítimos (períodos sem transações)

### 4. Dados Externos Limitados

- Indicadores macroeconômicos indisponíveis
- Dados de POI (Point of Interest) em sua maioria ausentes
- Conhecimento específico do mercado chinês necessário

## Solucao Proposta

### Abordagem em Tres Versoes

1. **v1 - Baseline**: MLP simples para estabelecer referência
2. **v2 - Feature Engineering**: Lags, médias móveis e validação por setor
3. **v3 - Otimização**: Busca sistemática de hiperparâmetros

### Arquitetura

Todas as versões usam MLPRegressor (redes neurais artificiais) com 3 camadas ocultas.

## Premios e Oportunidades

- Reconhecimento em painel de IA de grupo imobiliário renomado
- Oportunidade de trabalho com profissionais do setor
- Exposição em comunidade global Kaggle
- Até +1 ponto de bonus por submissão em competição

---

**Proxima Secao**: [Dataset e Preparacao](../dataset/overview.md)
