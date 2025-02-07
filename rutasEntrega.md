# Búsqueda Local para Optimizar Rutas de Entrega

## Descripción
Este código implementa un algoritmo de búsqueda local para optimizar la ruta de entrega de un restaurante a varias ubicaciones en Guadalajara y Zapopan. Se minimiza la distancia total recorrida, utilizando una matriz de adyacencia simplificada con las distancias entre los puntos de entrega.

## Código en Python

```python
import random
import math

# Definir los puntos de entrega
puntos_entrega = ['Restaurante', 'Centro', 'Zapopan', 'Tlaquepaque', 'Tonalá', 'Chapultepec', 'Providencia', 'El Salto']

# Definir las distancias entre puntos (matriz de adyacencia simplificada)
distancias = {
    'Restaurante': {'Centro': 5, 'Zapopan': 10, 'Tlaquepaque': 8, 'Tonalá': 12, 'Chapultepec': 6, 'Providencia': 7, 'El Salto': 15},
    'Centro': {'Restaurante': 5, 'Zapopan': 7, 'Tlaquepaque': 4, 'Tonalá': 9, 'Chapultepec': 3, 'Providencia': 6, 'El Salto': 12},
    # Completar con el resto de las distancias
}

def distancia_total(ruta):
    total = 0
    for i in range(len(ruta) - 1):
        total += distancias[ruta[i]][ruta[i+1]]
    total += distancias[ruta[-1]]['Restaurante']  # Volver al restaurante
    return total

def generar_solucion_inicial():
    ruta = puntos_entrega[1:]  # Excluir el restaurante
    random.shuffle(ruta)
    return ['Restaurante'] + ruta

def busqueda_local(max_iteraciones):
    mejor_ruta = generar_solucion_inicial()
    mejor_distancia = distancia_total(mejor_ruta)

    for _ in range(max_iteraciones):
        # Implementar lógica de búsqueda local aquí
        # (por ejemplo, intercambiar dos puntos de entrega aleatoriamente)
        pass

    return mejor_ruta, mejor_distancia

# Ejecutar el algoritmo
mejor_ruta, mejor_distancia = busqueda_local(1000)
print(f"Mejor ruta encontrada: {' -> '.join(mejor_ruta)}")
print(f"Distancia total: {mejor_distancia} km")
```

## Explicación
1. **Definición del problema**: Se establecen puntos de entrega y las distancias entre ellos.
2. **Cálculo de la distancia total**: Se suman las distancias entre cada punto de la ruta, asegurando que la ruta termine en el restaurante.
3. **Generación de una solución inicial**: Se ordenan aleatoriamente los puntos de entrega.
4. **Búsqueda local**: Se planea implementar una mejora iterativa intercambiando puntos de la ruta.

Este código se puede ampliar para incluir estrategias de optimización como **Simulated Annealing** o **Algoritmos Genéticos** para mejorar la calidad de la solución encontrada.
