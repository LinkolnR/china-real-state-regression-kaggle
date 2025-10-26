## Desafios, Lições e Próximos Passos

### 1. Desafios
- POIs com colunas inteiramente ausentes em subsets; necessidade de exclusão/ignorar no pré-processamento.
- Evitar vazamento temporal ao criar lags/MAs e ao mesclar tabelas de vizinhança.
- Escalonar adequadamente variáveis altamente assimétricas e com muitos zeros.
- Balancear capacidade do MLP e regularização para não superajustar.

### 2. Lições Aprendidas
- `log1p` no alvo facilita o aprendizado e estabiliza o treino.
- Lags e médias móveis são cruciais para séries temporais de montantes transacionais.
- Validação temporal é obrigatória; validação aleatória superestima desempenho.

### 3. Próximos Passos
- Testar GBDTs (LightGBM/XGBoost) com o mesmo conjunto de features.
- Experimentar modelos sequenciais (LSTM/TemporalConv) com atenção ao leakage.
- Explorar embeddings de `sector_int` e atenções entre setores (vizinhança).
- Refinar a seleção de POIs (agregações mais robustas ou exclusão sistemática).

### 4. Espaços para Gráficos/Quadros
- Quadro de riscos vs mitigação.
- Roadmap de próximos experimentos.

```text
Quadro: Riscos x Mitigações (preencher)
- Risco | Impacto | Probabilidade | Mitigação | Status
```


