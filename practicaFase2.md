# Continuación...
Implementación de Algoritmos de Aprendizaje Supervisado y No Supervisado para Predicción de Calidad del Aire

### Objetivo

El objetivo de esta práctica es aplicar algoritmos de aprendizaje supervisado y no supervisado para predecir la calidad del aire en una ciudad metropolitana. Utilizarás técnicas de machine learning implementadas en Python con la biblioteca scikit-learn.

### Datos

Utiliza tu conjunto de datos de la fase anterior de contaminantes atmosféricos (PM2.5, PM10, NO2, O3, SO2) y variables meteorológicas (temperatura, humedad, velocidad del viento, dirección del viento, precipitación) recopilados durante los últimos 5 años.

### Paso 1: Preprocesamiento de Datos

1. **Importación de Bibliotecas**
   ```python
   import pandas as pd
   import numpy as np
   from sklearn.model_selection import train_test_split
   from sklearn.preprocessing import StandardScaler
   from sklearn.ensemble import RandomForestRegressor
   from sklearn.metrics import mean_squared_error, r2_score
   from sklearn.decomposition import PCA
   from sklearn.cluster import KMeans
   import matplotlib.pyplot as plt
   ```

2. **Carga de Datos**
   ```python
   # Carga tus datos desde un archivo CSV
   df = pd.read_csv('datos_calidad_aire.csv')
   ```

3. **Limpieza y Transformación**
   ```python
   # Elimina valores faltantes si los hay
   df.dropna(inplace=True)
   
   # Normaliza las variables predictoras
   scaler = StandardScaler()
   df[['Temperatura', 'Humedad', 'VelocidadViento', 'Precipitacion']] = scaler.fit_transform(df[['Temperatura', 'Humedad', 'VelocidadViento', 'Precipitacion']])
   ```

### Paso 2: Análisis Exploratorio

1. **Visualización de Series Temporales**
   ```python
   plt.figure(figsize=(10,6))
   plt.plot(df['PM2.5'])
   plt.title('Concentración de PM2.5')
   plt.xlabel('Fecha')
   plt.ylabel('Concentración (μg/m³)')
   plt.show()
   ```

2. **Matriz de Correlación**
   ```python
   corr_matrix = df.corr()
   plt.figure(figsize=(10,8))
   plt.imshow(corr_matrix, cmap='coolwarm', interpolation='nearest')
   plt.title('Matriz de Correlación')
   plt.colorbar()
   plt.show()
   ```

### Paso 3: Aprendizaje Supervisado

1. **Divide Datos en Entrenamiento y Prueba**
   ```python
   X = df[['Temperatura', 'Humedad', 'VelocidadViento', 'Precipitacion']]
   y = df['PM2.5']
   X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
   ```

2. **Modelo de Regresión con Random Forest**
   ```python
   rf_model = RandomForestRegressor(n_estimators=100, random_state=42)
   rf_model.fit(X_train, y_train)
   y_pred = rf_model.predict(X_test)
   
   # Evaluación del modelo
   mse = mean_squared_error(y_test, y_pred)
   r2 = r2_score(y_test, y_pred)
   print(f"MSE: {mse}, R²: {r2}")
   ```

### Paso 4: Aprendizaje No Supervisado

1. **Análisis de Componentes Principales (PCA)**
   ```python
   pca = PCA(n_components=2)
   pca_data = pca.fit_transform(X)
   plt.figure(figsize=(8,6))
   plt.scatter(pca_data[:,0], pca_data[:,1])
   plt.title('Análisis de Componentes Principales')
   plt.xlabel('Componente Principal 1')
   plt.ylabel('Componente Principal 2')
   plt.show()
   ```

2. **Clustering con K-Means**
   ```python
   kmeans = KMeans(n_clusters=3, random_state=42)
   kmeans.fit(X)
   labels = kmeans.labels_
   plt.figure(figsize=(8,6))
   plt.scatter(X['Temperatura'], X['Humedad'], c=labels)
   plt.title('Clustering con K-Means')
   plt.xlabel('Temperatura')
   plt.ylabel('Humedad')
   plt.show()
   ```

### Paso 5: Evaluación y Validación de Modelos

1. **Validación Cruzada**
   ```python
   from sklearn.model_selection import cross_val_score
   scores = cross_val_score(rf_model, X_train, y_train, cv=5)
   print("Scores de Validación Cruzada:", scores)
   ```

2. **Realiza Mejoras del Modelo**
   - Ajusta hiperparámetros del modelo de Random Forest para mejorar su rendimiento.
   - Utiliza búsqueda en cuadrícula o búsqueda aleatoria para encontrar los mejores hiperparámetros.
