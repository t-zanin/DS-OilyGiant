#### (Portuguese version below)

# OilyGiant Oil Well Analysis

## Project Overview

This project was developed for the OilyGiant mining company to identify the best region for developing new oil wells, maximizing profit while minimizing risks. Using geological exploration data from three regions, a linear regression model was built to predict the volume of reserves in new wells. The *bootstrapping* technique was used to assess potential profit and risks, considering a budget of $100 million for 200 wells and a maximum loss risk of less than 2.5%.

## Objectives

- Load and prepare data from the three regions provided in the files `geo_data_0.csv`, `geo_data_1.csv`, and `geo_data_2.csv`.
- Train a linear regression model to predict the volume of reserves in each region.
- Select the 200 wells with the highest estimated values per region.
- Calculate potential profit based on predictions and actual values.
- Apply the *bootstrapping* technique to estimate profit distribution, average profit, 95% confidence interval, and risk of loss.
- Recommend the most suitable region for well development, justifying the choice based on average profit and risk.

## Data Description

The dataset consists of three files:

1. **geo_data_0.csv**: Data for Region 1.
2. **geo_data_1.csv**: Data for Region 2.
3. **geo_data_2.csv**: Data for Region 3.

Each file contains the following columns:
- `id`: Unique identifier for the oil well.
- `f0`, `f1`, `f2`: Three geological features (significant but without specific meaning).
- `product`: Volume of reserves in the well (in thousands of barrels).

### Business Conditions
- **Budget**: $100 million for the development of 200 wells.
- **Revenue**: $4,500 per unit of product (thousands of barrels).
- **Cost per well**: $500,000 ($100M ÷ 200 wells).
- **Minimum volume per well**: 111.11 thousand barrels to avoid losses ($500,000 ÷ $4,500).
- **Maximum risk**: Loss risk below 2.5% in selected regions.
- **Well selection**: 500 points are studied, and the top 200 are chosen for development.

*Note*: The data is synthetic and does not include contract details or specific well characteristics.

## Data Preprocessing

- **Data Types**:
  - The files were loaded using Pandas, and the columns `f0`, `f1`, `f2`, and `product` were verified as numeric, requiring no conversion.
- **Missing Values**:
  - No missing values were found in the files `geo_data_0.csv`, `geo_data_1.csv`, and `geo_data_2.csv`.
- **Data Quality**:
  - No duplicates or inconsistencies were identified.
  - The features `f0`, `f1`, and `f2` were used directly as predictor variables, with no need for scaling, as linear regression does not require standardization in this case.

## Analysis Steps

1. **Data Splitting**:
   - Each dataset was split into 75% for training and 25% for validation, using `train_test_split` with `random_state=42` for reproducibility.
   - Created the `split_data` function to modularize the splitting process.

2. **Model Training**:
   - A linear regression model (`LinearRegression`) was trained for each region using the `train_model` function.
   - The features `f0`, `f1`, and `f2` were used to predict the volume of reserves (`product`).

3. **Predictions and Evaluation**:
   - Predictions were generated on the validation set using the `make_predictions` function.
   - Calculated the average predicted volume and root mean squared error (RMSE) using the `evaluate_model` function.
   - Results:
     - **Region 1**: Average predicted volume of 92.40 thousand barrels, RMSE of 37.76 thousand barrels.
     - **Region 2**: Average predicted volume of 68.71 thousand barrels, RMSE of 0.89 thousand barrels.
     - **Region 3**: Average predicted volume of 94.77 thousand barrels, RMSE of 40.15 thousand barrels.

4. **Profit Calculation**:
   - Defined business variables: budget ($100M), number of wells (200), revenue per unit ($4,500).
   - Created the `calculate_profit` function to select the 200 wells with the highest predictions, calculate the actual volume, and compute net profit.
   - Results:
     - **Region 1**: Total volume of 29,686.98 thousand barrels, profit of $33,591,411.14.
     - **Region 2**: Total volume of 27,589.08 thousand barrels, profit of $24,150,866.97.
     - **Region 3**: Total volume of 27,996.83 thousand barrels, profit of $25,985,717.59.

5. **Risk Analysis with Bootstrapping**:
   - Created the `bootstrap_profit` function to perform 1,000 samples of 500 wells with replacement, select the top 200, and calculate profit.
   - The `analyze_bootstrap` function calculated average profit, 95% confidence interval, and risk of loss.
   - Results:
     - **Region 1**: Average profit of $6,061,226.32, confidence interval ($100,894.12, $12,463,709.81), loss risk of 2.50%.
     - **Region 2**: Average profit of $6,651,176.54, confidence interval ($1,808,515.85, $12,057,104.61), loss risk of 0.20%.
     - **Region 3**: Average profit of $5,851,036.38, confidence interval (-$8,369.42, $12,120,508.98), loss risk of 2.60%.

## Key Findings

- **Model Performance**:
  - Region 2 showed the highest accuracy (RMSE of 0.89 thousand barrels), indicating highly reliable predictions.
  - Regions 1 and 3 had higher errors (RMSE ~37-40 thousand barrels), but still within an acceptable range (less than 50% of the average volume).

- **Potential Profit**:
  - Region 1 initially appeared the most profitable ($33.59M), followed by Region 3 ($25.99M) and Region 2 ($24.15M).
  - No region met the minimum average volume of 111.11 thousand barrels per well, highlighting the importance of selecting the best wells.

- **Risk Analysis**:
  - Region 2 is the only region with a loss risk below 2.5% (0.20%), while also having the highest average profit ($6.65M).
  - Region 1 is at the acceptable risk limit (2.50%), and Region 3 exceeds the limit (2.60%).

## Conclusions and Recommendations

- **Recommended Region**:
  - **Region 2** is the best choice for well development, offering the highest average profit ($6.65M) and the lowest loss risk (0.20%), meeting the risk criterion of < 2.5%.
  - Although Region 1 showed higher potential profit in the initial analysis ($33.59M), *bootstrapping* revealed greater instability, with risk at the acceptable limit.

- **Justification**:
  - The high model accuracy in Region 2 (low RMSE) ensures reliable predictions, reducing uncertainties.
  - The 0.20% loss risk provides financial security for the $100 million investment.
  - The competitive average profit makes Region 2 the most balanced choice.

- **Business Impact**:
  - Focusing on Region 2 maximizes financial return with minimal risk, aligning with OilyGiant’s objectives.
  - It is recommended to explore the 200 best wells identified by the model to optimize profit.

## Tools and Technologies

- **Language**: Python
- **Libraries**: Pandas, NumPy, Scikit-learn (LinearRegression, train_test_split, mean_squared_error)
- **Environment**: Jupyter Notebook

## Project Structure

- `notebooks/`: Jupyter Notebook with preprocessing, model training, profit calculations, *bootstrapping*, and analyses.
- `data/`: Files `geo_data_0.csv`, `geo_data_1.csv`, and `geo_data_2.csv` (not included in the repository due to size).
- `README.md`: Project overview and documentation.

____________________________________
____________________________________
____________________________________
____________________________________

# Análise de Poços de Petróleo da OilyGiant

## Visão Geral do Projeto

Este projeto foi desenvolvido para a empresa de mineração OilyGiant, com o objetivo de identificar a melhor região para o desenvolvimento de novos poços de petróleo, maximizando o lucro e minimizando os riscos. Com base em dados de exploração geológica de três regiões, foi construído um modelo de regressão linear para prever o volume de reservas em novos poços. A técnica de *bootstrapping* foi utilizada para avaliar o lucro potencial e os riscos, considerando um orçamento de 100 milhões de dólares para 200 poços e um limite de risco de prejuízo inferior a 2,5%.

## Objetivos

- Carregar e preparar os dados das três regiões fornecidas nos arquivos `geo_data_0.csv`, `geo_data_1.csv` e `geo_data_2.csv`.
- Treinar um modelo de regressão linear para prever o volume de reservas em cada região.
- Selecionar os 200 poços com maiores valores estimados por região.
- Calcular o lucro potencial com base nas predições e nos valores reais.
- Aplicar a técnica de *bootstrapping* para estimar a distribuição de lucros, lucro médio, intervalo de confiança de 95% e risco de prejuízo.
- Recomendar a região mais adequada para o desenvolvimento de poços, justificando a escolha com base no lucro médio e no risco.

## Descrição dos Dados

O conjunto de dados é composto por três arquivos:

1. **geo_data_0.csv**: Dados da Região 1.
2. **geo_data_1.csv**: Dados da Região 2.
3. **geo_data_2.csv**: Dados da Região 3.

Cada arquivo contém as seguintes colunas:
- `id`: Identificador único do poço de petróleo.
- `f0`, `f1`, `f2`: Três características geológicas (significativas, mas sem significado específico).
- `product`: Volume de reservas no poço (em milhares de barris).

### Condições do Negócio
- **Orçamento**: $100 milhões para o desenvolvimento de 200 poços.
- **Receita**: $4.500 por unidade de produto (milhares de barris).
- **Custo por poço**: $500.000 ($100M ÷ 200 poços).
- **Volume mínimo por poço**: 111,11 mil barris para evitar prejuízo ($500.000 ÷ $4.500).
- **Risco máximo**: Prejuízo inferior a 2,5% nas regiões selecionadas.
- **Seleção de poços**: 500 pontos são estudados, e os 200 melhores são escolhidos para desenvolvimento.

*Nota*: Os dados são sintéticos e não incluem detalhes de contratos ou características específicas dos poços.

## Pré-processamento dos Dados

- **Tipos de Dados**:
  - Os arquivos foram carregados com Pandas, e as colunas `f0`, `f1`, `f2` e `product` foram verificadas como numéricas, não exigindo conversão.
- **Valores Ausentes**:
  - Não foram encontrados valores ausentes nos arquivos `geo_data_0.csv`, `geo_data_1.csv` e `geo_data_2.csv`.
- **Qualidade dos Dados**:
  - Não foram identificadas duplicatas ou inconsistências.
  - As características `f0`, `f1` e `f2` foram usadas diretamente como variáveis preditoras, sem necessidade de escalonamento, pois a regressão linear não exige padronização neste caso.

## Etapas da Análise

1. **Divisão dos Dados**:
   - Cada conjunto de dados foi dividido em 75% para treinamento e 25% para validação, usando `train_test_split` com `random_state=42` para reprodutibilidade.
   - Criada a função `split_data` para modularizar o processo de divisão.

2. **Treinamento do Modelo**:
   - Um modelo de regressão linear (`LinearRegression`) foi treinado para cada região usando a função `train_model`.
   - As características `f0`, `f1` e `f2` foram usadas para prever o volume de reservas (`product`).

3. **Predições e Avaliação**:
   - Predições foram geradas no conjunto de validação com a função `make_predictions`.
   - Calculados o volume médio previsto e o erro quadrático médio da raiz (REQM) com a função `evaluate_model`.
   - Resultados:
     - **Região 1**: Volume médio previsto de 92,40 mil barris, REQM de 37,76 mil barris.
     - **Região 2**: Volume médio previsto de 68,71 mil barris, REQM de 0,89 mil barris.
     - **Região 3**: Volume médio previsto de 94,77 mil barris, REQM de 40,15 mil barris.

4. **Cálculo de Lucro**:
   - Definidas variáveis do negócio: orçamento ($100M), número de poços (200), receita por unidade ($4.500).
   - Criada a função `calculate_profit` para selecionar os 200 poços com maiores predições, calcular o volume real e o lucro líquido.
   - Resultados:
     - **Região 1**: Volume total de 29.686,98 mil barris, lucro de $33.591.411,14.
     - **Região 2**: Volume total de 27.589,08 mil barris, lucro de $24.150.866,97.
     - **Região 3**: Volume total de 27.996,83 mil barris, lucro de $25.985.717,59.

5. **Análise de Riscos com Bootstrapping**:
   - Criada a função `bootstrap_profit` para realizar 1.000 amostras de 500 poços com reposição, selecionar os 200 melhores e calcular o lucro.
   - Função `analyze_bootstrap` calculou lucro médio, intervalo de confiança de 95% e risco de prejuízo.
   - Resultados:
     - **Região 1**: Lucro médio de $6.061.226,32, intervalo de confiança ($100.894,12, $12.463.709,81), risco de 2,50%.
     - **Região 2**: Lucro médio de $6.651.176,54, intervalo de confiança ($1.808.515,85, $12.057.104,61), risco de 0,20%.
     - **Região 3**: Lucro médio de $5.851.036,38, intervalo de confiança (-$8.369,42, $12.120.508,98), risco de 2,60%.

## Principais Descobertas

- **Desempenho do Modelo**:
  - A Região 2 apresentou a maior precisão (REQM de 0,89 mil barris), indicando predições altamente confiáveis.
  - As Regiões 1 e 3 tiveram erros maiores (REQM ~37-40 mil barris), mas ainda dentro de um limite aceitável (menos de 50% do volume médio).

- **Lucro Potencial**:
  - A Região 1 inicialmente pareceu a mais lucrativa ($33,59M), seguida pela Região 3 ($25,99M) e Região 2 ($24,15M).
  - Nenhuma região atingiu o volume mínimo médio de 111,11 mil barris por poço, destacando a importância de selecionar os melhores poços.

- **Análise de Riscos**:
  - A Região 2 é a única com risco de prejuízo abaixo de 2,5% (0,20%), além de apresentar o maior lucro médio ($6,65M).
  - A Região 1 está no limite do risco aceitável (2,50%), e a Região 3 excede o limite (2,60%).

## Conclusões e Recomendações

- **Região Recomendada**:
  - A **Região 2** é a melhor escolha para o desenvolvimento de poços, pois oferece o maior lucro médio ($6,65M) e o menor risco de prejuízo (0,20%), atendendo ao critério de risco < 2,5%.
  - Apesar de a Região 1 ter maior lucro potencial na análise inicial ($33,59M), o *bootstrapping* revelou maior instabilidade, com risco no limite aceitável.

- **Justificativa**:
  - A alta precisão do modelo na Região 2 (REQM baixo) garante predições confiáveis, reduzindo incertezas.
  - O risco de prejuízo de 0,20% oferece segurança financeira para o investimento de 100 milhões de dólares.
  - O lucro médio competitivo torna a Região 2 a escolha mais equilibrada.

- **Impacto no Negócio**:
  - Focar na Região 2 maximiza o retorno financeiro com risco mínimo, alinhando-se aos objetivos da OilyGiant.
  - Recomenda-se explorar os 200 melhores poços identificados pelo modelo para otimizar o lucro.

## Ferramentas e Tecnologias

- **Linguagem**: Python
- **Bibliotecas**: Pandas, NumPy, Scikit-learn (LinearRegression, train_test_split, mean_squared_error)
- **Ambiente**: Jupyter Notebook

## Estrutura do Projeto

- `notebooks/`: Notebook Jupyter com pré-processamento, treinamento do modelo, cálculos de lucro, *bootstrapping* e análises.
- `data/`: Arquivos `geo_data_0.csv`, `geo_data_1.csv` e `geo_data_2.csv` (não incluídos no repositório devido ao tamanho).
- `README.md`: Visão geral e documentação do projeto.