# Previsão de Torque em Máquinas com Machine Learning

Este projeto explora técnicas de aprendizado de máquina para prever o torque de operação de uma máquina a partir de variáveis de processo, como temperatura, velocidade de rotação, desgaste da ferramenta e tipo de produto.

O estudo compara modelos tradicionais de regressão e redes neurais MLP, incluindo uma busca exploratória por diferentes arquiteturas e hiperparâmetros.

## Notebook

- `regressao_torque.ipynb`

## Objetivo

Estimar a variável `Torque [Nm]` e comparar o desempenho de diferentes algoritmos por meio das métricas:

- MAE — erro absoluto médio;
- RMSE — raiz do erro quadrático médio;
- R² — coeficiente de determinação.

## Dataset

O notebook espera o arquivo abaixo no mesmo diretório:

```text
fresadera_dataset.csv
```

O conjunto utilizado na execução registrada possui 10.000 observações e 14 colunas. Entre as variáveis disponíveis estão:

- tipo do produto;
- temperatura do ar;
- temperatura do processo;
- velocidade de rotação;
- desgaste da ferramenta;
- indicadores de falha da máquina;
- torque, utilizado como variável-alvo.

As colunas `UDI` e `Product ID` são removidas antes do treinamento. A variável categórica `Type` passa por one-hot encoding, enquanto as variáveis numéricas são padronizadas.

> O dataset não está incluído neste repositório. Antes de distribuí-lo, verifique sua origem, licença e condições de uso.

## Modelos avaliados

- Regressão Linear;
- Ridge;
- Árvore de Decisão;
- Random Forest;
- XGBoost;
- K-Nearest Neighbors;
- Support Vector Regression;
- redes neurais MLP com TensorFlow/Keras.

O notebook também experimenta diferentes números de camadas e neurônios, funções de ativação, otimizadores, taxas de aprendizado, tamanhos de lote, dropout e gradient clipping.

## Resultados registrados

Os resultados abaixo foram extraídos da última execução salva no notebook:

| Modelo otimizado | MAE | RMSE | R² |
|---|---:|---:|---:|
| XGBoost | 2,8803 | 3,7656 | 0,8561 |
| Random Forest | 2,8873 | 3,7847 | 0,8547 |
| SVR | 2,9455 | 3,9540 | 0,8414 |

A melhor configuração de MLP registrada atingiu aproximadamente `R² = 0,8544`, resultado próximo aos melhores métodos de ensemble.

Esses números são apresentados para documentar a execução existente. Eles não foram recalculados durante a preparação deste repositório.

## Como executar

1. Instale o Python 3.10 ou superior.
2. Coloque `fresadera_dataset.csv` no mesmo diretório do notebook.
3. Instale as dependências:

```bash
pip install jupyter pandas numpy matplotlib seaborn scikit-learn tensorflow xgboost
```

4. Inicie o Jupyter:

```bash
jupyter notebook regressao_torque.ipynb
```

O notebook executa buscas extensas de hiperparâmetros de redes neurais e pode levar bastante tempo. Para uma validação rápida, execute inicialmente apenas as células de preparação e comparação dos modelos tradicionais.

## Observações metodológicas

O notebook tem caráter exploratório. Algumas configurações são comparadas repetidamente no conjunto de teste, o que pode produzir uma estimativa otimista de generalização. Para uso acadêmico rigoroso ou em produção, recomenda-se:

- reservar um conjunto de teste independente até a escolha final do modelo;
- fazer a seleção de hiperparâmetros somente com treino e validação cruzada;
- investigar possível vazamento de informação nas colunas indicadoras de falha, pois algumas podem estar relacionadas diretamente ao torque;
- encapsular todo o pré-processamento e o modelo em um único pipeline reproduzível.

## Tecnologias

- Python;
- pandas e NumPy;
- scikit-learn;
- XGBoost;
- TensorFlow/Keras;
- Matplotlib e Seaborn.

## Licença

Nenhuma licença foi definida para este projeto. Adicione um arquivo `LICENSE` antes de permitir reutilização ou redistribuição do código.
