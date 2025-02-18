# 🧠 Redes Neuronales Artificiales

![GitHub](https://img.shields.io/badge/GitHub-Markdown-blue?logo=markdown)
![Python](https://img.shields.io/badge/Python-3.8+-yellow?logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-orange?logo=tensorflow)

## 📌 Contenido

1️⃣ **Paradigma Conexionista**
   - Definición y fundamentos
   - Características principales
   - Ventajas del enfoque conexionista

2️⃣ **Redes Neuronales Artificiales**
   - ¿Qué son las redes neuronales?
   - Clasificación según el número de capas
   - Tipos de redes neuronales según su arquitectura
   - Características clave
   - Campos de aplicación

3️⃣ **📚 Librerías de Python para Redes Neuronales**
   - `TensorFlow` y `Keras`: Para la construcción y entrenamiento de modelos.
   - `PyTorch`: Alternativa flexible para investigación y producción.
   - `Scikit-learn`: Para modelos más simples y herramientas de preprocesamiento.
   - `OpenCV`: Para procesamiento de imágenes en conjunto con redes neuronales.

4️⃣ **🔍 Ejemplos de Aplicación en la Vida Real**
   - **Redes Feedforward:** Clasificación de dígitos escritos a mano (MNIST).
   - **Redes Convolucionales (CNNs):** Detección de objetos en imágenes.
   - **Redes Recurrentes (RNNs):** Predicción de series de tiempo y procesamiento de texto.

5️⃣ **💻 Implementación en Python**
   - Desarrollo de un modelo de **red neuronal convolucional (CNN)** en **Google Colab** utilizando **TensorFlow** y **Keras**.
   - Explicación **paso a paso** de la implementación.

### 📝 Código de Ejemplo: Red Convolucional en TensorFlow/Keras
```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers
import matplotlib.pyplot as plt
from tensorflow.keras.datasets import mnist

# Cargar el conjunto de datos MNIST
(x_train, y_train), (x_test, y_test) = mnist.load_data()

# Normalizar los datos
x_train, x_test = x_train / 255.0, x_test / 255.0

# Expandir dimensiones para el modelo convolucional
x_train = x_train.reshape(-1, 28, 28, 1)
x_test = x_test.reshape(-1, 28, 28, 1)

# Definir la arquitectura de la red neuronal convolucional
model = keras.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(28,28,1)),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])

# Compilar el modelo
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# Entrenar el modelo
model.fit(x_train, y_train, epochs=5, validation_data=(x_test, y_test))

# Evaluar el modelo
test_loss, test_acc = model.evaluate(x_test, y_test)
print(f"\nPrecisión en el conjunto de prueba: {test_acc:.4f}")
```

6️⃣ **🚀 Mejoras y Optimización del Modelo**
   - **Data Augmentation**: Aumentar la cantidad de datos aplicando transformaciones a las imágenes.
   - **Ajuste de Hiperparámetros**: Probar diferentes configuraciones de capas, filtros y funciones de activación.
   - **Transfer Learning**: Usar modelos preentrenados como `VGG16` o `ResNet`.
   - **Implementación de técnicas de regularización** como Dropout para reducir el sobreajuste.

---

¡Esperamos que este material te ayude a comprender mejor las redes neuronales! 🚀
