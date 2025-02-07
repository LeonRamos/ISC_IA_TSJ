
```


Para comprender este tema utilizaremos un ejemplo simple de búsqueda local para resolver el problema de encontrar el máximo de una función en un intervalo dado. Puedes encontrar el código y ejecutarlo en el siguiente notebook de Google Colab:

[Enlace al notebook de Google Colab](https://colab.research.google.com/drive/1234567890abcdefghijklmnopqrstuvwxyz)

## Explicación del Algoritmo

1. **Función objetivo**: Definimos una función simple que queremos maximizar.
2. **Solución inicial**: Elegimos un punto de partida aleatorio dentro del intervalo dado.
3. **Vecindario**: Generamos soluciones vecinas añadiendo pequeñas perturbaciones a la solución actual.
4. **Iteración**: En cada paso, evaluamos las soluciones vecinas y nos movemos a la mejor si mejora la solución actual.
5. **Criterio de parada**: El algoritmo se detiene después de un número fijo de iteraciones o cuando no se encuentran mejoras.

## Código Python

```
import random
import math

def funcion_objetivo(x):
    return math.sin(x) * math.exp(-0.1 * abs(x))

def busqueda_local(intervalo, num_iteraciones):
    # Solución inicial aleatoria
    solucion_actual = random.uniform(intervalo, intervalo[1])
    mejor_valor = funcion_objetivo(solucion_actual)

    for _ in range(num_iteraciones):
        # Generar vecino
        vecino = solucion_actual + random.uniform(-0.1, 0.1)
        vecino = max(min(vecino, intervalo[1]), intervalo)  # Mantener dentro del intervalo
        
        valor_vecino = funcion_objetivo(vecino)
        
        # Mover a la mejor solución
        if valor_vecino > mejor_valor:
            solucion_actual = vecino
            mejor_valor = valor_vecino

    return solucion_actual, mejor_valor

# Ejecutar el algoritmo
intervalo = (-10, 10)
num_iteraciones = 1000
mejor_solucion, mejor_valor = busqueda_local(intervalo, num_iteraciones)

print(f"Mejor solución encontrada: x = {mejor_solucion:.4f}")
print(f"Valor de la función objetivo: f(x) = {mejor_valor:.4f}")
```

## Conclusión

Este ejemplo ilustra cómo la búsqueda local puede encontrar soluciones aproximadas a problemas de optimización. Aunque simple, este enfoque es la base de muchos algoritmos más avanzados en inteligencia artificial y optimización.
```
