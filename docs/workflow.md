# Fluxo de Execucao

## Introducao

Este documento descreve como executar o projeto completo: notebooks, metricas e relatorios.

## Pré-requisitos

### Ambiente Python

```bash
python --version  # 3.8+
pip install -r requirements.txt
```

### Dependências

```
numpy
pandas
scikit-learn
matplotlib
seaborn
jupyter
nbconvert
```

## Execucao dos Notebooks

### Opcao 1: Sequencial (Recomendado)

```bash
# Terminal 1
jupyter nbconvert --to notebook --execute 3_training_v1.ipynb --output 3_training_v1.ipynb

# Aguarde conclusao (~10 min)
# Terminal 2
jupyter nbconvert --to notebook --execute 3_training_v2.ipynb --output 3_training_v2.ipynb

# Aguarde conclusao (~15 min)
# Terminal 3
jupyter nbconvert --to notebook --execute 3_training_v3.ipynb --output 3_training_v3.ipynb

# Aguarde conclusao (~2-3 horas)
```

### Opcao 2: Paralela (Avancado)

```bash
python executar_tudo_jupyter.py
```

Executa os tres notebooks em paralelo se forem independentes.

## Geracao de Metricas

### Arquivos Gerados Automaticamente

Cada notebook salva metricas em JSON:

```
3_training_v1.ipynb  →  metricas_v1.json
3_training_v2.ipynb  →  metricas_v2.json
3_training_v3.ipynb  →  metricas_v3.json
```

### Verificacao

```bash
ls -lh metricas_*.json
```

Deve listar 3 arquivos.

## Geracao de Relatorio Comparativo

### Script de Comparacao

```bash
python comparar_metricas.py
```

Produz: `relatorio_comparacao_YYYYMMDD_HHMMSS.txt`

### Saida Esperada

```
================================================================================
COMPARACAO DE METRICAS: v1 vs v2 vs v3
================================================================================

1. ROOT MEAN SQUARED ERROR (RMSE)
v1:     38.937,57  (Baseline)
v2:      7.547,03  (-80,6%)  *** MELHOR ***
v3:     19.991,72  (+165% vs v2)

...

RANKING FINAL
================================================================================
1º lugar: v2 (R2 = 0,9763) *** RECOMENDADO ***
2º lugar: v1 (R2 = 0,5513)
```

## Estrutura de Saídas

### Modelos Treinados

```
mlp_model_v1.joblib
mlp_model_v2.joblib
mlp_model_v3.joblib
```

### Dados de Metricas

```
metricas_v1.json   (RMSE, MAE, R2 treino/teste)
metricas_v2.json   (OOF, por-fold, Competition Score)
metricas_v3.json   (melhor config, grid search)
```

### Predicoes

```
submission_v1.csv
submission_v2.csv
submission_v3.csv
```

## Troubleshooting

### Problema: Notebook nao executado completamente

**Solucao:**
- Verificar se ha dados faltantes em arquivos .npy
- Revisar se seed 42 esta definido corretamente
- Checar se ha erro de memoria (reducir batch size)

### Problema: JSON nao encontrado

**Solucao:**
- Confirmar que notebook chegou na ultima celula
- Executar manualmente a ultima celula se necessario
- Verificar se arquivo foi salvo no diretorio correto

### Problema: Comparacao falha

**Solucao:**
- Verificar sintaxe do JSON: `python -m json.tool metricas_v1.json`
- Confirmar que todas tres metricas existem
- Revisar se valores nao sao None ou NaN

## Automacao (Opcional)

### Script Bash para Execucao Completa

```bash
#!/bin/bash
echo "Iniciando pipeline..."
jupyter nbconvert --to notebook --execute 3_training_v1.ipynb
jupyter nbconvert --to notebook --execute 3_training_v2.ipynb
jupyter nbconvert --to notebook --execute 3_training_v3.ipynb
python comparar_metricas.py
echo "Pipeline completo!"
```

## Tempo Estimado

| Etapa | Tempo |
|-------|-------|
| v1 Execucao | 10-15 min |
| v2 Execucao | 15-20 min |
| v3 Execucao | 2-3 horas |
| Comparacao | 2-5 seg |
| **Total** | **~3-4 horas** |

---

**Proxima Secao**: [Referencias](references.md)
