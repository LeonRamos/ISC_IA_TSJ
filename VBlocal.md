

```
# Búsqueda Local para Encontrar el Máximo de una Función

## Contexto

Este ejemplo implementa un algoritmo de búsqueda local para encontrar el máximo de la función `f(x) = sin(x) * exp(-0.1 * |x|)` en el intervalo [-10, 10]. La búsqueda local es una técnica de optimización que parte de una solución inicial y la mejora iterativamente explorando soluciones vecinas.

### Características de la función:
- Es una función continua y suave.
- Tiene múltiples máximos locales.
- El factor exponencial hace que los valores disminuyan a medida que |x| aumenta.

### Funcionamiento del algoritmo:
1. Inicia con una solución aleatoria en el intervalo dado.
2. En cada iteración, genera una solución vecina con una pequeña perturbación.
3. Si la solución vecina es mejor (mayor valor de la función), se mueve a ella.
4. Repite este proceso un número fijo de veces.

Este enfoque es eficiente para encontrar un máximo local, aunque no garantiza encontrar el máximo global.

## (Código Python)[https://colab.research.google.com/drive/1WzAzwzZ2cff8vXPhCdh7KlLEYSW-OOuq?usp=sharing]

```
import random
import math
import numpy as np
import matplotlib.pyplot as plt

def funcion_objetivo(x):
    return math.sin(x) * math.exp(-0.1 * abs(x))

def busqueda_local(intervalo, num_iteraciones):
    solucion_actual = random.uniform(*intervalo)
    mejor_valor = funcion_objetivo(solucion_actual)
    
    for _ in range(num_iteraciones):
        vecino = solucion_actual + random.uniform(-0.1, 0.1)
        vecino = max(min(vecino, intervalo), intervalo)
        valor_vecino = funcion_objetivo(vecino)
        
        if valor_vecino > mejor_valor:
            solucion_actual = vecino
            mejor_valor = valor_vecino
    
    return solucion_actual, mejor_valor

# Parámetros
intervalo = (-10, 10)
num_iteraciones = 1000

# Ejecutar el algoritmo
mejor_solucion, mejor_valor = busqueda_local(intervalo, num_iteraciones)

print(f"Mejor solución encontrada: x = {mejor_solucion:.4f}")
print(f"Valor máximo de la función: f(x) = {mejor_valor:.4f}")

# Visualización
x = np.linspace(*intervalo, 1000)
y = [funcion_objetivo(xi) for xi in x]

plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.scatter([mejor_solucion], [mejor_valor], color='red', s=100, label='Máximo encontrado')
plt.title('Búsqueda Local - Máximo de la Función')
plt.xlabel('x')
plt.ylabel('f(x)')
plt.legend()
plt.grid(True)
plt.show()
```

Este código se puede ejecutar en Google Colab para visualizar el resultado de la búsqueda local.
```

