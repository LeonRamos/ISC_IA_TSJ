
# 🧠 Paradigma Basado en Datos en Inteligencia Artificial
[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

El **paradigma basado en datos** es un enfoque fundamental en la Inteligencia Artificial (IA) que se centra en el uso de grandes cantidades de información para desarrollar sistemas capaces de aprender y tomar decisiones. 

## 🔍 ¿Qué incluye este paradigma?
Este paradigma incluye dos áreas principales:

### 🤖 Aprendizaje Automático (*Machine Learning*)
El **aprendizaje automático** es un subconjunto de la IA que permite a las máquinas aprender y mejorar automáticamente a partir de la experiencia. 

📌 **Características clave:**
- Utiliza algoritmos para analizar grandes cantidades de datos 📊
- Aprende de estadísticas y toma decisiones fundamentadas 📈
- Mejora el rendimiento con el tiempo al exponerse a más datos ⚙️
- Aplicaciones: motores de búsqueda, diagnósticos médicos, detección de fraude, entre otros 💡

🔹 **Tipos de Aprendizaje Automático:**
- 📗 *Aprendizaje Supervisado*
- 📘 *Aprendizaje No Supervisado*
- 📙 *Aprendizaje por Refuerzo*

### 🏛️ Aprendizaje Profundo (*Deep Learning*)
El **aprendizaje profundo** es una rama avanzada del aprendizaje automático que utiliza **redes neuronales artificiales** inspiradas en el cerebro humano.

📌 **Características principales:**
- Basado en redes neuronales con múltiples capas 🧩
- Capaz de modelar abstracciones de alto nivel en datos 🔬
- Utiliza transformaciones no lineales múltiples e iterativas 🔄
- Especialmente eficaz en tareas como reconocimiento de voz e imágenes 🖼️🔊

🔹 **Arquitecturas de Aprendizaje Profundo:**
- 🏗️ *Redes Neuronales Profundas (DNNs)*
- 🖼️ *Redes Neuronales Convolucionales (CNNs)*
- 🔗 *Redes de Creencia Profunda (DBNs)*
- 🧠 *Transformers*

## 📊 Diferencias entre Aprendizaje Automático y Aprendizaje Profundo
| Característica | Aprendizaje Automático | Aprendizaje Profundo |
|--------------|---------------------|--------------------|
| 📈 Dependencia de Datos | Menos datos necesarios | Grandes volúmenes de datos 📡 |
| 🔄 Procesamiento | Algoritmos tradicionales | Redes neuronales profundas 🏛️ |
| 🎯 Aplicaciones | Análisis de datos, predicciones | Visión por computadora, NLP 🗣️ |

## 🚀 Aplicaciones del Paradigma Basado en Datos
Este paradigma ha impulsado grandes avances en IA, permitiendo el desarrollo de sistemas más sofisticados y capaces. Algunas aplicaciones incluyen:

- **Reconocimiento de voz y lenguaje natural** 🗣️

- **Visión por computadora** 👁️

- **Sistemas de recomendación** 📌

- **Vehículos autónomos** 🚗

- **Diagnóstico médico** 🏥

- **Análisis de mercado** 📊

## 📌 Importancia en la IA Moderna
El enfoque en el procesamiento de grandes volúmenes de información lo hace especialmente relevante en la era del **Big Data**. Su integración con tecnologías avanzadas como la computación en la nube y hardware especializado ha impulsado el desarrollo de soluciones más inteligentes y eficientes.

## Práctica 👍🏼
Práctica: Implementación de un Sistema de Recomendación Básico en Google Colab

En esta práctica, los alumnos desarrollarán un sistema de recomendación simple utilizando Google Colab. Seguirán estos pasos:

## Paso 1: Configuración del entorno

1. Abrir Google Colab en https://colab.research.google.com/
2. Crear un nuevo notebook haciendo clic en "File" > "New Notebook"

## Paso 2: Importación de bibliotecas

Copiar y ejecutar el siguiente código en una celda:

```python
import pandas as pd
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
```

## Paso 3: Carga de datos

1. Crear un conjunto de datos simple en una celda:

```python
data = {
    'Usuario': ['A', 'A', 'A', 'B', 'B', 'C', 'C', 'C', 'D', 'D'],
    'Película': ['X', 'Y', 'Z', 'X', 'Z', 'X', 'Y', 'Z', 'Y', 'Z'],
    'Calificación': [5, 3, 4, 2, 5, 3, 4, 3, 5, 2]
}
df = pd.DataFrame(data)
print(df)
```

2. Ejecutar la celda para ver el DataFrame

## Paso 4: Preparación de datos

Crear una matriz de usuarios y películas:

```python
user_movie_matrix = df.pivot(index='Usuario', columns='Película', values='Calificación').fillna(0)
print(user_movie_matrix)
```

## Paso 5: Cálculo de similitud

Calcular la similitud del coseno entre usuarios:

```python
user_similarity = cosine_similarity(user_movie_matrix)
user_similarity_df = pd.DataFrame(user_similarity, index=user_movie_matrix.index, columns=user_movie_matrix.index)
print(user_similarity_df)
```

## Paso 6: Función de recomendación

Implementar una función de recomendación simple:

```python
def recommend_movies(user, user_similarity_df, user_movie_matrix, n_recommendations=2):
    similar_users = user_similarity_df[user].sort_values(ascending=False)[1:3]
    recommendations = pd.Series()
    
    for similar_user, similarity in similar_users.items():
        similar_user_ratings = user_movie_matrix.loc[similar_user]
        recommendations = recommendations.add(similar_user_ratings * similarity, fill_value=0)
    
    recommendations = recommendations[recommendations.index.isin(user_movie_matrix.loc[user][user_movie_matrix.loc[user] == 0].index)]
    return recommendations.sort_values(ascending=False).head(n_recommendations)

# Ejemplo de uso
user_to_recommend = 'B'
recommendations = recommend_movies(user_to_recommend, user_similarity_df, user_movie_matrix)
print(f"Recomendaciones para el usuario {user_to_recommend}:")
print(recommendations)
```

Esta práctica básica te introducirá a los sistemas de recomendación utilizando Google Colab, permitiendo a los estudiantes experimentar con conceptos fundamentales de IA y aprendizaje automático.

> [!IMPORTANT]
> ### Actividad 📢
>
>Para hacer más robusta la práctica del sistema de recomendación, el alumno deberá implementar las siguientes mejoras:
>
> 1. Incorporar filtrado basado en contenido: Además del filtrado colaborativo, el alumno debe implementar un enfoque basado en contenido. Esto implicaría añadir características a las películas (como género, director, actores) y recomendar películas con atributos similares a las que el usuario ha calificado positivamente.
>
> 2. Manejar el problema de arranque en frío: Desarrollar una estrategia para nuevos usuarios o películas sin calificaciones. Por ejemplo, podrían implementar un sistema híbrido que combine filtrado colaborativo con recomendaciones populares o basadas en contenido para usuarios nuevos.
>
> 3. Implementar validación cruzada: Para evaluar la robustez del modelo, los alumnos pueden dividir los datos en conjuntos de entrenamiento y prueba, y utilizar técnicas de validación cruzada. Esto les permitirá medir la precisión de las recomendaciones y ajustar el modelo para mejorar su rendimiento.


## 📚 Referencias y enlaces útiles
- [Google Cloud - IA vs Machine Learning](https://cloud.google.com/learn/artificial-intelligence-vs-machine-learning?hl=es-419)
- [Wikipedia - Aprendizaje Automático](https://es.wikipedia.org/wiki/Aprendizaje_autom%C3%A1tico)
- [Tableau - Deep Learning en IA](https://www.tableau.com/es-mx/data-insights/ai/ml-deep-learning-in-ai)
- [4Geeks Academy - Deep Learning](https://github.com/4GeeksAcademy/machine-learning-content/blob/master/06-ml_algos/intro-to-deep-learning.es.md)
- [Wikipedia - Aprendizaje Profundo](https://es.wikipedia.org/wiki/Aprendizaje_profundo)
- [NetApp - Deep Learning](https://www.netapp.com/es/artificial-intelligence/what-is-deep-learning/)
- [Cibernética - Paradigmas de IA](https://cibernetica.wordpress.com/2021/11/03/paradigmas-y-modelos-de-la-inteligencia-artificial/)
- https://iayrobotica.com/preguntas-frecuentes/como-se-utilizan-los-sistemas-de-recomendacion-en-ia/
- https://www.aluracursos.com/blog/google-colab-que-es-y-como-usarlo
- https://www.ibm.com/mx-es/think/topics/recommendation-engine
- http://fcaglp.unlp.edu.ar/~gbaume/grupo/Publicaciones/Apuntes/GoogleColab.pdf
- https://dialnet.unirioja.es/descarga/articulo/9282023.pdf
- https://www.youtube.com/watch?v=b9yi63T4KNI
- https://www.tutellus.com/tecnologia/inteligencia-artificial/sistemas-de-recomendacion-con-inteligencia-artificial-31139
- https://www.youtube.com/watch?v=9g61bnipcSs
---
![GitHub last commit](https://img.shields.io/github/last-commit/tuusuario/turepositorio)
![GitHub stars](https://img.shields.io/github/stars/tuusuario/turepositorio?style=social)
