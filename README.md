# Miniprojeto - Análise de Densidade Populacional com K-means

Este projeto utiliza o algoritmo de K-means para analisar a densidade populacional de estados brasileiros. A visualização dos dados é feita em um mapa geográfico usando a biblioteca Basemap, exibindo clusters de densidade para melhor entendimento da distribuição populacional.

## Objetivo

O objetivo do projeto é aplicar a técnica de K-means para identificar e visualizar clusters de densidade populacional nos estados brasileiros, utilizando dados fictícios. A análise foca em agrupar estados com densidades similares e representar visualmente esses clusters.

## Tecnologias e Bibliotecas Utilizadas

- Python
- Google Colab
- Bibliotecas Python:
  - `numpy`
  - `matplotlib`
  - `scikit-learn`
  - `basemap` (e `basemap-data-hires` para mapas de alta resolução)

## Estrutura do Código

1. **Instalação das Dependências**  
   Instalação da biblioteca `basemap` e suas dependências no Google Colab.

   ```python
   !pip install basemap basemap-data-hires
   ```

### 2. Importação das Bibliotecas

Importe as bibliotecas necessárias para o projeto:

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from mpl_toolkits.basemap import Basemap
```
### 3. Definição dos Dados

Defina os dados fictícios para latitude, longitude e densidade populacional para cada estado brasileiro. Esses dados são utilizados para simular a análise de densidade.

```python
estados = ['SP', 'RJ', 'MG', 'ES', 'RS', 'SC', 'PR', 'BA', 'PE', 'CE']
latitude = [-23.55, -22.90, -19.92, -20.32, -30.03, -27.59, -25.43, -12.97, -8.05, -3.71]
longitude = [-46.63, -43.20, -43.93, -40.34, -51.23, -48.55, -49.27, -38.51, -34.88, -38.54]
densidade_populacional = [300, 400, 250, 180, 200, 150, 180, 120, 170, 160]
```
### 4. Aplicação do Algoritmo K-means

Aplique o algoritmo de K-means nos dados de densidade populacional para identificar clusters.

```python
data = np.array(list(zip(latitude, longitude, densidade_populacional)))
kmeans = KMeans(n_clusters=3, random_state=0).fit(data[:, 2].reshape(-1, 1))
clusters = kmeans.predict(data[:, 2].reshape(-1, 1))
```
### 5. Visualização dos Clusters

Crie um gráfico de dispersão simples para visualizar os clusters de densidade populacional. Cada estado é representado por um ponto colorido de acordo com seu cluster.

```python
plt.scatter(densidade_populacional, [1]*len(densidade_populacional), c=clusters, cmap='viridis')
plt.title('Clusters de Densidade Populacional nos Estados Brasileiros')
plt.xlabel('Densidade Populacional (habitantes/km²)')
plt.ylabel('Estados')
plt.show()
```
### 6. Criação do Mapa Geográfico com Basemap

Configure o mapa do Brasil usando a biblioteca Basemap e plote os estados com suas respectivas densidades e clusters.

```python
plt.figure(figsize=(10, 8))
m = Basemap(projection='merc', llcrnrlat=-35, urcrnrlat=5, llcrnrlon=-75, urcrnrlon=-34, resolution='i')
m.drawcoastlines()
m.drawcountries()
m.drawstates()
```
### 7. Plotagem dos Pontos e Centros dos Clusters

Para cada estado, plote um ponto no mapa, colorido de acordo com o cluster ao qual pertence. Os centros dos clusters são indicados com um "X".

```python
colors = ['red', 'green', 'blue']
for i, estado in enumerate(estados):
    x, y = m(longitude[i], latitude[i])
    plt.scatter(x, y, c=colors[clusters[i]], s=densidade_populacional[i]/5, label=estado)

for i, centro in enumerate(kmeans.cluster_centers_):
    plt.scatter([], [], c=colors[i], s=100, marker='x', label=f'Centro do Cluster {i+1}')

```

### 8. Exibição do Mapa

Exiba o mapa com a legenda indicando os estados e os centros dos clusters.

```python
plt.title('K-means Clustering - Densidade Populacional dos Estados Brasileiros')
plt.legend(loc='lower left')
plt.show()
```

## Resultados

O código gera duas saídas principais:
1. Um gráfico de dispersão mostrando os clusters de densidade populacional.
2. Um mapa do Brasil com a localização dos estados coloridos de acordo com os clusters, indicando a distribuição da densidade populacional.

Essas visualizações ajudam a entender como os estados se agrupam em relação à densidade populacional, proporcionando uma análise geográfica e estatística dos dados.

## Contribuição

Sinta-se à vontade para contribuir com melhorias ou sugestões para o projeto. Abra uma issue ou envie um pull request!

## Licença

Este projeto é de uso educacional e está sob a licença MIT.


