## Modelos e Arquiteturas

### 1. Pipeline de Pré-processamento
- Imputação: `SimpleImputer(strategy='median')` para numéricos.
- Escala: `StandardScaler`.
- Transformação de alvo: `log1p` no treino; `expm1` após predição.
- Seleção de features: numéricas derivadas do dataset unificado, excluindo chaves (`month_index`, `sector_int`) e o alvo.

### 2. MLP (sklearn MLPRegressor)
- Camadas ocultas: exploradas combinações como `(64,64)`, `(128,128)`, `(128,64,64)`, `(256,128)`, `(256,128,64)`.
- Ativações: `relu` e `tanh`.
- Regularização: `alpha` (L2) ~ [1e-6, 1e-2] (loguniform).
- Otimizador: `adam` com `learning_rate_init` ~ [1e-4, 5e-2] (loguniform).
- Tamanho de batch: {64, 128, 256}.
- Early stopping: `early_stopping=True`, `validation_fraction=0.15`, `n_iter_no_change=30`, `max_iter=400`.

### 3. Melhor Configuração Observada (OOF)
- `hidden_layer_sizes=(256,128,64)`
- `activation='tanh'`
- `alpha≈2.4e-6`
- `batch_size=256`
- `learning_rate_init≈9.3e-3`
- `solver='adam'`

### 4. Estratégia de Validação
- `TimeSeriesSplit(n_splits=5)` garantindo ordem temporal.
- Avaliação por MSE em escala linear do alvo (após `expm1`).

### 5. Espaços para Gráficos e Tabelas
- Curva de perda (train): `loss_curve_`.
- Tabela de hiperparâmetros testados e MSE OOF por combinação.
- Importância por permutação (top 20 features).

Insira as figuras/tabelas:

![Curva de perda](imgs/loss_curve.png)

![Importância por permutação](imgs/perm_importance.png)

```text
Tabela: Hiperparâmetros vs MSE (preencher)
- Comb # | hidden_layer_sizes | activation | alpha | batch | lr_init | OOF MSE
```


