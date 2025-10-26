# Conclusão

Este projeto se propôs a desenvolver e avaliar um modelo de regressão para a previsão de demanda no mercado imobiliário chinês, utilizando uma abordagem incremental que culminou na comparação de três versões de um Perceptron Multicamadas (MLP). A análise dos resultados não apenas permitiu a identificação de um modelo superior, mas também gerou insights valiosos sobre a metodologia de modelagem para dados temporais e hierárquicos.

## Síntese dos Principais Achados

A evolução do Modelo v1 ao v3 demonstrou três lições:

1.  **A Superioridade da Engenharia de Atributos:** A transição do Modelo v1 para o v2, que introduziu atributos baseados em defasagens temporais (*lags*) e médias móveis (*moving averages*), resultou em uma melhoria drástica no desempenho. A redução de **80,6% no RMSE** e o aumento de **77 pontos percentuais no coeficiente de determinação ($R^2$)** demonstram que uma engenharia de atributos bem fundamentada, capaz de capturar as dinâmicas intrínsecas dos dados, possui um impacto superior ao de ajustes finos na arquitetura do modelo.

2.  **A Importância da Estratégia de Validação:** A escolha de uma estratégia de validação adequada ao problema foi crucial. O Modelo v2, que utilizou `GroupKFold` para respeitar a estrutura hierárquica dos setores, apresentou uma generalização muito superior ao Modelo v3, que retornou a uma abordagem de `TimeSeriesSplit`. Isso evidencia que a prevenção de vazamento de dados (*data leakage*) e a representação correta da estrutura dos dados no processo de validação são tão críticas quanto a própria arquitetura do modelo.

3.  **Os Limites da Otimização de Hiperparâmetros:** O Modelo v3, apesar de empregar uma busca sistemática por hiperparâmetros, não apenas falhou em superar o Modelo v2, como também apresentou um desempenho inferior em métricas de generalização (RMSE e *Competition Score*). Este resultado exemplifica um caso clássico de retornos decrescentes, onde a complexidade adicional e o custo computacional não se traduziram em ganhos de performance, indicando um sobreajuste ao conjunto de validação.

## Recomendações e Justificativa

Com base na análise comparativa, o **Modelo v2 é recomendado** como a solução final. Pelos seguintes motivos:

-   **Desempenho de Generalização:** Obteve o menor RMSE (7.547,03) e o segundo maior *Competition Score* (0,46430), bem próximo do score de v3, mas com menor RMSE, o que significa que ele seria melhor em prever dados nunca vistos.
-   **Capacidade Explicativa:** Alcançou um $R^2$ de 0,9763, explicando 97,6% da variância da variável alvo.
-   **Eficiência Computacional:** Exige um tempo de treinamento moderado (15-20 minutos).
-   **Interpretabilidade:** As 27 features projetadas possuem um significado claro e conectado ao domínio do problema.


---
