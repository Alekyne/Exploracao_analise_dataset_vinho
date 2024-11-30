# README - Normalização e Análise Exploratória do Dataset de Vinho

## Descrição do Projeto

Este projeto envolve a normalização e análise exploratória de dados (EDA) do dataset **wine.dat**, que contém informações sobre diferentes características de vinhos, como acidez fixa, acidez volátil, teor alcoólico, entre outras. O objetivo da atividade é aplicar técnicas de normalização e explorar os dados para entender melhor as relações entre as variáveis.

### Alunos:
- **Alekyne Ribeiro** (Matrícula: 541062)
- **Ana Livia** (Matrícula: 536158)

### Professor:
- **Julio**

## Objetivo

O objetivo principal da atividade foi aplicar três métodos diferentes de normalização sobre o dataset **wine.dat**:
1. **Normalização por norma constante (L2)**: Cada variável é dividida pela sua norma (magnitude), garantindo que as variáveis estejam em uma escala comparável.
2. **Normalização Min-Max**: As variáveis são escaladas para um intervalo entre 0 e 1, mantendo as relações entre os dados.
3. **Padronização**: A transformação das variáveis para que possuam média igual a 0 e desvio padrão igual a 1, o que é útil para modelos que assumem distribuições normais.

Além disso, foi realizada uma análise exploratória para observar as propriedades dos dados, como valores ausentes, estatísticas descritivas e visualizações gráficas (boxplot, histograma, heatmap de correlação).

## Etapas do Projeto

1. **Carregamento dos Dados**:
   O arquivo `WineQT.dat` foi carregado em um DataFrame utilizando a biblioteca **pandas**.
   
2. **Renomeação das Colunas**:
   As colunas do dataset foram renomeadas para o português para facilitar a compreensão.

3. **Análise Descritiva**:
   - Verificação de valores ausentes.
   - Cálculo de estatísticas descritivas, como mínimo, máximo, média e desvio padrão.
   - Visualização da distribuição do valor alcoólico e outros aspectos importantes dos dados.

4. **Normalização**:
   Três métodos de normalização foram aplicados:
   - **Normalização por norma constante (L2)**: Cada variável numérica foi dividida pela sua norma.
   - **Min-Max Scaling**: Os dados foram escalados para o intervalo [0, 1].
   - **Padronização**: As variáveis foram transformadas para média 0 e desvio padrão 1.

5. **Análise de Outliers**:
   Através do cálculo de Z-Scores, foram identificados os outliers, que foram posteriormente analisados.

6. **Correlação e Colinearidade**:
   A matriz de correlação foi calculada e, com base nela, as variáveis com alta colinearidade (coeficiente de correlação superior a 0.9) foram removidas para evitar multicolinearidade nos modelos.

7. **Visualizações Gráficas**:
   - **Boxplot**: Utilizado para analisar a distribuição dos dados de cada variável.
   - **Histograma**: Para observar a distribuição do teor alcoólico.
   - **Heatmap de Correlação**: Para entender melhor as relações entre as variáveis.

## Bibliotecas Utilizadas

As seguintes bibliotecas foram utilizadas para realizar a análise:
- `pandas` para manipulação e análise de dados.
- `numpy` para cálculos numéricos.
- `matplotlib` e `seaborn` para visualizações gráficas.
- `scipy.stats` para o cálculo do Z-Score.

## Código

### 1. Carregamento dos dados

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import zscore

data = pd.read_csv('WineQT.dat')
colunas_port = ['acidez fixa', 'acidez volátil', 'acido citrico', 'açúcar residual', 'cloretos', 'dióxido de enxofre livre', 'dióxido de enxofre total', 'densidade', 'ph', 'sulfatos', 'alcool', 'qualidade', 'ID']
data.columns = colunas_port
2. Análise Descritiva
python
Copiar código
data.describe()
print(data.isnull().sum())
print(data.min(), data.max(), data.mean(), data.std())
3. Normalização por Norma Constante (L2)
python
Copiar código
numeric_cols = data.select_dtypes(include=[np.number]).columns
for col in numeric_cols:
    norma = np.sqrt(np.sum(data[col] ** 2))
    if norma != 0:
        data[col] = data[col] / norma
4. Normalização Min-Max
python
Copiar código
data_std = (data - data.min(axis=0)) / (data.max(axis=0) - data.min(axis=0))
data = data_std * (1 - 0) + 0
5. Padronização
python
Copiar código
for col in numeric_cols:
    media = np.mean(data[col])
    desvio_padrao = np.std(data[col])
    if desvio_padrao != 0:
        data[col] = (data[col] - media) / desvio_padrao
6. Análise de Outliers
python
Copiar código
z_scores = np.abs(zscore(data.select_dtypes(include=[np.number])))
outliers = (z_scores > 3).sum(axis=0)
print(outliers)
7. Visualizações
python
Copiar código
plt.figure(figsize=(12, 6))
plt.boxplot(data, labels=data.columns)
plt.title("Boxplot das Variáveis do Vinho")
plt.xlabel("Variáveis")
plt.ylabel("Escala Normalizada")
plt.xticks(rotation=45)
plt.show()

# Heatmap da Matriz de Correlação
correlation_matrix = data.corr()
sns.heatmap(correlation_matrix, annot=True, fmt=".2f", cmap='coolwarm', square=True, cbar=True, linewidths=.5)
plt.title("Matriz de Correlação das Variáveis do Vinho")
plt.show()

# Histograma do Álcool
data['alcool'].hist(bins=20, color='lightblue', edgecolor='black')
plt.title('Distribuição do Álcool')
plt.xlabel('Teor Alcoólico')
plt.ylabel('Frequência')
plt.show()
Conclusões
A normalização e padronização dos dados são essenciais para modelos de aprendizado de máquina, especialmente quando lidamos com variáveis de diferentes escalas.
O processo de análise exploratória permitiu uma melhor compreensão das distribuições dos dados e a detecção de possíveis outliers.
A matriz de correlação e o heatmap ajudaram a identificar relações entre as variáveis, e a remoção das variáveis com alta colinearidade pode melhorar a eficiência de modelos preditivos futuros.
Este README oferece um resumo da atividade realizada, destacando o processo de normalização e análise dos dados de vinho, além das ferramentas e técnicas utilizadas para a análise exploratória.

arduino
Copiar código
