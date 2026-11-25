# Clustering-de-clientes-de-un-centro-comercial-Mall-Customers-

Proyecto de **Machine Learning no supervisado** enfocado en la segmentación de clientes de un centro comercial (*Mall Customers*), utilizando algoritmos de clustering para identificar patrones de comportamiento según edad, ingresos anuales y nivel de gasto.

El objetivo es comparar **K-Means y DBSCAN**, evaluar su rendimiento con y sin reducción de dimensionalidad mediante PCA e interpretar los segmentos obtenidos desde una perspectiva de negocio.

## Objetivos

- Explorar y preparar un dataset de clientes.
- Aplicar estandarización para trabajar con algoritmos basados en distancias.
- Reducir dimensionalidad mediante PCA.
- Determinar el número óptimo de clusters para K-Means.
- Optimizar los parámetros `eps` y `min_samples` de DBSCAN.
- Evaluar los modelos mediante métricas de clustering.
- Interpretar los segmentos y obtener conclusiones comerciales.

## Dataset

Se utiliza **Mall Customers**, un conjunto de datos de 200 clientes con las siguientes variables:

| Variable | Descripción |
|---|---|
| CustomerID | Identificador del cliente |
| Gender | Género |
| Age | Edad |
| Annual Income (k$) | Ingreso anual |
| Spending Score (1-100) | Puntaje de gasto |

Para el clustering se utilizan tres variables: `Age`, `Annual Income` y `Spending Score`.

`CustomerID` se excluye por ser un identificador y `Gender` se reserva para el análisis descriptivo de los grupos.

## Tecnologías y herramientas

- Python
- Pandas y NumPy
- Matplotlib y Seaborn
- Scikit-learn
- Google Colab / Jupyter Notebook

## Metodología

### 1. Exploración y preprocesamiento
- Análisis exploratorio de datos (EDA).
- Distribución de variables y relaciones entre características.
- Verificación de valores nulos y duplicados.
- Estandarización mediante `StandardScaler`.

### 2. Reducción de dimensionalidad (PCA)

Se aplica Principal Component Analysis para reducir las tres variables originales a dos componentes principales.

Las dos componentes conservan aproximadamente el **77,6 % de la varianza** del conjunto original.

Se comparan los resultados de los algoritmos en el espacio original y en el espacio transformado.

### 3. K-Means

Se prueban valores de K entre 2 y 10.

Para seleccionar la cantidad de clusters se utilizan:

- **Método del codo (Inertia):** analiza la reducción de la inercia al aumentar K.
- **Silhouette Score:** evalúa cohesión y separación entre clusters.
- **Davies-Bouldin Index:** mide la similitud entre clusters; valores menores son mejores.

Se ajustan dos modelos independientes: K-Means sin PCA y K-Means con PCA.

### 4. DBSCAN

Se utiliza DBSCAN para identificar regiones de alta densidad y detectar observaciones atípicas.

La selección de parámetros se realiza mediante:

- Gráfico de k-distancias para orientar la elección de `eps`.
- Búsqueda de combinaciones de `eps` y `min_samples`.
- Evaluación mediante Silhouette Score.
- Control de cantidad de clusters y porcentaje de ruido.

Se comparan los resultados con y sin PCA.

### 5. Evaluación y comparación

Se utilizan las siguientes métricas:

| Métrica | Interpretación |
|---|---|
| Silhouette Score | Mayor es mejor |
| Davies-Bouldin Index | Menor es mejor |
| Calinski-Harabasz Index | Mayor es mejor |
| Adjusted Rand Index (ARI) | Compara la similitud entre particiones |

También se analizan los perfiles de cada grupo mediante edad promedio, ingreso, gasto, distribución por género y cantidad de clientes.

## Resultados

Comparación de los cuatro modelos obtenidos:

| Modelo | Clusters | Silhouette | Davies-Bouldin | Calinski-Harabasz |
|---|---:|---:|---:|---:|
| K-Means sin PCA | 6 | 0.427 | 0.828 | 135.102 |
| K-Means con PCA | 4 | 0.421 | 0.825 | 182.080 |
| DBSCAN sin PCA | 2 | 0.273 | 1.020 | 54.421 |
| DBSCAN con PCA | 2 | 0.371 | 0.701 | 63.095 |

*En DBSCAN, las métricas se calculan excluyendo los puntos clasificados como ruido.*

### Principales hallazgos

**K-Means sin PCA**
- Obtuvo el mayor Silhouette Score.
- Identificó seis segmentos de clientes.
- Permitió una segmentación más detallada e interpretable.

**K-Means con PCA**
- Redujo la dimensionalidad a dos componentes.
- Identificó cuatro grupos.
- Conservó aproximadamente el 77,6 % de la varianza original.

**DBSCAN**
- Identificó dos clusters y observaciones consideradas ruido.
- Con PCA obtuvo mejores valores de Silhouette y Davies-Bouldin que sin PCA.
- Resultó útil para identificar clientes atípicos, aunque produjo una segmentación menos detallada.

## Interpretación de negocio

A partir de los segmentos identificados se pueden plantear distintas estrategias comerciales:

- **Ingresos altos y gastos altos:** clientes de alto valor, potencialmente prioritarios para programas de fidelización.
- **Ingresos altos y gastos bajos:** clientes con capacidad adquisitiva y potencial de crecimiento mediante promociones personalizadas.
- **Ingresos bajos y gastos altos:** segmento joven con una elevada propensión al consumo.
- **Ingresos bajos y gastos bajos:** clientes con menor actividad de consumo, para quienes podrían diseñarse campañas específicas.

## Conclusiones

K-Means sin PCA presentó el mejor resultado general para este problema de segmentación, tanto por sus métricas como por la facilidad de interpretación de sus seis grupos.

DBSCAN permitió explorar una perspectiva diferente, identificando regiones densas y observaciones atípicas, aunque su capacidad de segmentación fue más limitada en este dataset.

Por su parte, PCA permitió analizar el impacto de la reducción de dimensionalidad. En este caso, al trabajar con solamente tres variables, la reducción a dos componentes implicó cierta pérdida de información y una menor granularidad en los grupos obtenidos.

**Conclusión final:** K-Means sin PCA resulta la alternativa más adecuada para desarrollar estrategias de segmentación comercial en este conjunto de datos, mientras que DBSCAN aporta valor complementario en la detección de clientes atípicos.

---

**Autor:** Lorenzo Ciprés  
**Área:** Data Science | Machine Learning | Unsupervised Learning
