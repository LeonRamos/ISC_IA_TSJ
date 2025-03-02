
# Análisis Exploratorio de Datos para Predicción de Calidad del Aire
---
## Contexto del Problema
La contaminación del aire es un problema crítico que afecta a las grandes ciudades en todo el mundo. En nuestra metrópolis, las autoridades están cada vez más preocupadas por los niveles crecientes de contaminantes atmosféricos y sus efectos en la salud pública. Durante los últimos 5 años, se ha llevado a cabo un extenso programa de monitoreo que ha recopilado datos diarios de varios contaminantes atmosféricos y variables meteorológicas.

Los contaminantes principales que se están monitoreando incluyen partículas en suspensión (PM2.5 y PM10), dióxido de nitrógeno (NO2), ozono troposférico (O3) y dióxido de azufre (SO2). Estos contaminantes son conocidos por sus efectos adversos en la salud respiratoria y cardiovascular de la población. Además, se han registrado variables meteorológicas como temperatura, humedad, velocidad y dirección del viento, y precipitación, ya que estos factores pueden influir significativamente en la concentración y dispersión de los contaminantes.

El objetivo de este ejercicio es realizar un análisis exploratorio detallado de estos datos para comprender mejor los patrones de contaminación, identificar las variables más influyentes y preparar el terreno para el desarrollo de un modelo de machine learning que pueda predecir los niveles de contaminación con precisión.

---
### Datos Disponibles

Para este ejercicio, utilizaremos un conjunto de datos similar al que se puede encontrar en el portal de datos abiertos de la Ciudad de México (http://www.aire.cdmx.gob.mx/default.php?opc='aKBhnmM%3D'). Debras construir un dataset similar utilizando las bases de datos en formato Excel disponibles en este sitio, que incluyen información de la Red Automática de Monitoreo Atmosférico (RAMA) y la Red de Meteorología y Radiación Solar (REDMET).

El conjunto de datos contiene las siguientes variables:

- Fecha
- PM2.5 (μg/m³)
- PM10 (μg/m³)
- NO2 (ppb)
- O3 (ppb)
- SO2 (ppb)
- Temperatura (°C)
- Humedad (%)
- Velocidad del viento (km/h)
- Dirección del viento (grados)
- Precipitación (mm)


### Parte 1: Fundamentos Matemáticos y Estadísticos

#### Álgebra Lineal

1. Utiliza la biblioteca NumPy para crear una matriz de correlación entre todas las variables numéricas del conjunto de datos.

Ejemplo:

```python
import numpy as np
import pandas as pd

# Suponiendo que 'df' es tu DataFrame con los datos
correlation_matrix = np.corrcoef(df.values.T)
```

2. Calcula los autovalores y autovectores de esta matriz de correlación.

Ejemplo:

```python
eigenvalues, eigenvectors = np.linalg.eig(correlation_matrix)
```

3. Interpreta cómo estos autovalores y autovectores podrían ser útiles para el análisis de componentes principales (PCA) en el contexto de la reducción de dimensionalidad para este conjunto de datos.

**Explicación: Los autovalores representan la cantidad de varianza explicada por cada componente principal, mientras que los autovectores indican la dirección de estas componentes en el espacio de características original. Componentes con autovalores más altos explican una mayor proporción de la varianza total en los datos.**

#### Cálculos

1. Para la variable PM2.5, calcula la derivada numérica para estimar la tasa de cambio diaria.

Ejemplo:

```python
pm25_values = df['PM2.5'].values
daily_change = np.diff(pm25_values) / np.diff(df.index.astype(int) / 1e9 / 86400)
```

2. Utiliza la integración numérica para calcular la exposición acumulada a PM2.5 durante períodos de una semana.

Ejemplo:

```python
from scipy import integrate

weekly_exposure = integrate.cumtrapz(pm25_values, df.index.astype(int) / 1e9 / 86400, initial=0)
```


#### Estadística y Probabilidad

1. Calcula la media, mediana, desviación estándar y los cuartiles para cada contaminante.

Ejemplo:

```python
stats = df[['PM2.5', 'PM10', 'NO2', 'O3', 'SO2']].describe()
```

2. Realiza una prueba de hipótesis para determinar si hay una diferencia significativa en los niveles de PM2.5 entre el verano y el invierno.

Ejemplo:

```python
from scipy import stats

summer_pm25 = df[df.index.month.isin([6, 7, 8])]['PM2.5']
winter_pm25 = df[df.index.month.isin([12, 1, 2])]['PM2.5']
t_stat, p_value = stats.ttest_ind(summer_pm25, winter_pm25)
```

3. Ajusta una distribución de probabilidad (por ejemplo, normal o log-normal) a los datos de PM2.5 y evalúa la bondad del ajuste.

Ejemplo:

```python
from scipy import stats

params = stats.lognorm.fit(df['PM2.5'])
_, p_value = stats.kstest(df['PM2.5'], 'lognorm', args=params)
```


### Parte 2: Programación en Python


1. Crea una función que lea el conjunto de datos desde un archivo CSV y lo convierta en un DataFrame de pandas.

Pasos:
- a) Importa las bibliotecas necesarias (pandas).
- b) Define una función que tome como argumento la ruta del archivo CSV.
- c) Utiliza pd.read_csv() para leer el archivo.
- d) Configura la columna de fecha como índice del DataFrame.
- e) Retorna el DataFrame resultante.

2. Implementa una clase `ContaminationAnalyzer` que encapsule los métodos para realizar análisis estadísticos básicos y visualizaciones.

Pasos:
- a) Define la clase `ContaminationAnalyzer`.
- b) Crea un método __init__ que tome un DataFrame como argumento.
- c) Implementa métodos para calcular estadísticas descriptivas, crear gráficos de series temporales y generar histogramas de contaminantes.

#### Estructuras de Datos

1. Utiliza un diccionario para almacenar los estadísticos descriptivos de cada contaminante.

Pasos:
- a) Crea un diccionario vacío.
- b) Itera sobre cada contaminante en el DataFrame.
- c) Para cada contaminante, calcula las estadísticas descriptivas y almacénalas como un sub-diccionario.

2. Crea una lista de tuplas que contenga los 10 días con los niveles más altos de PM2.5, incluyendo la fecha y el valor.

Pasos:
- a) Ordena el DataFrame por los valores de PM2.5 en orden descendente.
- b) Selecciona las primeras 10 filas.
- c) Crea una lista de tuplas con la fecha y el valor de PM2.5 para cada fila.

#### Manipulación de Datos con NumPy y pandas

1. Utiliza pandas para realizar un resample de los datos a promedios semanales y mensuales.

Pasos:
- a) Utiliza el método resample() del DataFrame para crear promedios semanales.
- b) Repite el proceso para crear promedios mensuales.
- c) Guarda los resultados en nuevos DataFrames.

2. Crea una nueva columna que categorice los niveles de PM2.5 en "Bajo", "Moderado", "Alto" y "Muy Alto" basándote en umbrales predefinidos.

Pasos:
- a) Define los umbrales para cada categoría.
- b) Utiliza pd.cut() para crear la nueva columna basada en estos umbrales.

3. Utiliza NumPy para calcular la matriz de correlación entre los contaminantes y las variables meteorológicas.

Pasos:
- a) Selecciona las columnas relevantes del DataFrame.
- b) Utiliza np.corrcoef() para calcular la matriz de correlación.
- c) Crea un DataFrame de pandas con la matriz resultante para facilitar su visualización.

### Parte 3: Visualización y Análisis Exploratorio

1. Crea un gráfico de series temporales que muestre la evolución de PM2.5 y PM10 a lo largo del tiempo.

Pasos:
- a) Utiliza matplotlib o seaborn para crear el gráfico.
- b) Configura el eje x para mostrar las fechas correctamente.
- c) Añade leyendas y títulos apropiados.

2. Genera un heatmap de la matriz de correlación calculada anteriormente.

Pasos:
- a) Utiliza seaborn para crear el heatmap.
- b) Configura la paleta de colores y añade una barra de color.
- c) Añade anotaciones para mostrar los valores de correlación.

3. Realiza un análisis de componentes principales (PCA) utilizando sklearn y visualiza los resultados en un gráfico de dispersión 2D.

Pasos:
- a) Importa PCA de sklearn.decomposition.
- b) Ajusta el PCA a los datos normalizados.
- c) Transforma los datos y crea un gráfico de dispersión con las dos primeras componentes principales.

4. Crea un gráfico de cajas (boxplot) que compare los niveles de NO2 por estación del año.

Pasos:
- a) Crea una nueva columna en el DataFrame para la estación del año.
- b) Utiliza seaborn para crear el boxplot.
- c) Configura los colores y etiquetas apropiadamente.

### Parte 4: Preparación para Machine Learning

1. Divide el conjunto de datos en conjuntos de entrenamiento y prueba.

Pasos:
- a) Importa train_test_split de sklearn.model_selection.
- b) Define las variables predictoras (X) y la variable objetivo (y).
- c) Utiliza train_test_split para dividir los datos.

2. Normaliza las variables predictoras utilizando sklearn.

Pasos:
- a) Importa StandardScaler de sklearn.preprocessing.
- b) Ajusta el StandardScaler a los datos de entrenamiento.
- c) Transforma tanto los datos de entrenamiento como los de prueba.

3. Identifica y maneja los valores atípicos en el conjunto de datos.

Pasos:
- a) Utiliza el método IQR o z-score para identificar valores atípicos.
- b) Decide si eliminar o transformar estos valores atípicos.
- c) Documenta el impacto de esta decisión en el conjunto de datos.

4. Realiza una selección de características basada en la importancia de las variables para predecir los niveles de PM2.5.

Pasos:
- a) Utiliza un modelo simple como RandomForestRegressor para obtener importancias de características.
- b) Visualiza las importancias de las características.
- c) Selecciona un subconjunto de las características más importantes para el modelado posterior.

### Parte 5: Análisis Avanzado y Modelado Preliminar

1. Análisis de series temporales

Pasos:
- a) Descompón la serie temporal de PM2.5 en tendencia, estacionalidad y residuos utilizando la biblioteca statsmodels.
- b) Visualiza cada componente y interpreta los resultados.
- c) Realiza una prueba de estacionariedad (como la prueba de Dickey-Fuller aumentada) en la serie de PM2.5.

Ejemplo:

```python
from statsmodels.tsa.seasonal import seasonal_decompose
from statsmodels.tsa.stattools import adfuller

# Descomposición de la serie temporal
result = seasonal_decompose(df['PM2.5'], model='additive', period=365)
result.plot()

# Prueba de estacionariedad
result = adfuller(df['PM2.5'])
print('ADF Statistic: %f' % result[0])
print('p-value: %f' % result[1])
```

2. Análisis de autocorrelación y autocorrelación parcial

Pasos:
- a) Calcula y visualiza la función de autocorrelación (ACF) para PM2.5.
- b) Calcula y visualiza la función de autocorrelación parcial (PACF) para PM2.5.
- c) Interpreta los resultados en el contexto de la identificación de modelos ARIMA.

3. Modelado preliminar con ARIMA

Pasos:
- a) Basándote en los resultados de ACF y PACF, propón un modelo ARIMA inicial.
- b) Ajusta el modelo utilizando statsmodels.
- c) Evalúa el ajuste del modelo mediante diagnósticos de residuos y métricas como AIC y BIC.

Ejemplo:

```python
from statsmodels.tsa.arima.model import ARIMA

# Ajustar modelo ARIMA
model = ARIMA(df['PM2.5'], order=(1,1,1))
results = model.fit()
print(results.summary())

# Diagnóstico de residuos
results.plot_diagnostics(figsize=(15, 12))
```


### Parte 6: Modelado de Machine Learning

1. Preparación de características (feature engineering)

Pasos:
- a) Crea características de rezago (lag features) para las variables de contaminantes y meteorológicas.
- b) Genera características de promedio móvil para capturar tendencias a corto plazo.
- c) Crea variables dummy para días de la semana y meses para capturar patrones temporales.

2. Implementación de un modelo de regresión

Pasos:
- a) Elige un algoritmo de regresión (por ejemplo, Random Forest o Gradient Boosting).
- b) Divide los datos en conjuntos de entrenamiento y prueba, asegurándote de mantener la integridad temporal.
- c) Entrena el modelo en el conjunto de entrenamiento.
- d) Evalúa el rendimiento en el conjunto de prueba utilizando métricas como RMSE, MAE y R².

Ejemplo:

```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error, r2_score

# Entrenar el modelo
rf_model = RandomForestRegressor(n_estimators=100, random_state=42)
rf_model.fit(X_train, y_train)

# Evaluar el modelo
y_pred = rf_model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
print(f"MSE: {mse}, R²: {r2}")
```

3. Interpretación del modelo

Pasos:
- a) Calcula y visualiza la importancia de las características.
- b) Utiliza SHAP (SHapley Additive exPlanations) para interpretar las predicciones del modelo.
- c) Analiza las interacciones entre características utilizando gráficos de dependencia parcial.

### Parte 7: Validación y Ajuste del Modelo

1. Validación cruzada de series temporales

Pasos:
- a) Implementa una estrategia de validación cruzada específica para series temporales (por ejemplo, validación cruzada de ventana deslizante).
- b) Evalúa el rendimiento del modelo a través de múltiples períodos de tiempo.

2. Ajuste de hiperparámetros

Pasos:
- a) Define una cuadrícula de hiperparámetros para tu modelo.
- b) Utiliza búsqueda en cuadrícula o búsqueda aleatoria con validación cruzada para encontrar los mejores hiperparámetros.
- c) Entrena el modelo final con los mejores hiperparámetros encontrados.

3. Evaluación final y visualización de resultados

Pasos:
- a) Evalúa el modelo final en un conjunto de datos de prueba separado.
- b) Crea visualizaciones que comparen las predicciones del modelo con los valores reales.
- c) Analiza el rendimiento del modelo en diferentes condiciones (por ejemplo, días de alta contaminación vs. días de baja contaminación).

### Entregables Finales

1. Notebook de tú framework de elección completo con todo el código, análisis y visualizaciones.
2. Informe técnico detallado en **PDF** que incluya:
    - Resumen ejecutivo de los hallazgos principales
    - Metodología detallada
    - Resultados del análisis exploratorio de datos
    - Descripción del proceso de modelado y selección de características
    - Evaluación del rendimiento del modelo final
    - Interpretación de los resultados del modelo
    - Limitaciones del estudio y áreas de mejora futura
3. Presentación visual en Genially que resuma los puntos clave del proyecto para una audiencia no técnica.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)
![GitHub](https://img.shields.io/badge/GitHub-Repo-black?logo=github)
![IA](https://img.shields.io/badge/IA-Inteligencia%20Artificial-red?logo=openai)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-SciKit%20Learn-orange?logo=scikitlearn)
![Asombroso](https://img.shields.io/badge/Asombroso-100%25-brightgreen)
![Scrum](https://img.shields.io/badge/Scrum-Agile-blue?style=for-the-badge)
