

```
# Demostración Visual del Algoritmo A*

## Grafo de Ejemplo

Consideremos el siguiente grafo para encontrar el camino más corto desde el nodo **A** al nodo **G**:

```
            A
          /   \
        (1)    (4)
        B       C
       / \     / \
    (2) (5) (1) (3)
    D    E   F    G
```

Los números entre paréntesis representan los costos de cada arista.

## Costos Heurísticos

Costos estimados (h(n)) desde cada nodo al objetivo (G):

- A: 6
- B: 5
- C: 2
- D: 4
- E: 6
- F: 2
- G: 0

## Pasos del Algoritmo

### Paso 1: Inicialización

- Nodo inicial: A (f(A) = g(A) + h(A) = 0 + 6 = 6)
- Lista abierta: [A]
- Lista cerrada: []

### Paso 2: Expansión de A

- Sucesores: 
  - B (f(B) = 1 + 5 = 6)
  - C (f(C) = 4 + 2 = 6)
- Lista abierta: [B, C]
- Lista cerrada: [A]

### Paso 3: Expansión de B

- Sucesores:
  - D (f(D) = 3 + 4 = 7)
  - E (f(E) = 6 + 6 = 12)
- Lista abierta: [C, D, E]
- Lista cerrada: [A, B]

### Paso 4: Expansión de C

- Sucesores:
  - F (f(F) = 5 + 2 = 7)
  - G (f(G) = 7 + 0 = 7)
- Lista abierta: [D, E, F, G]
- Lista cerrada: [A, B, C]

### Paso 5: Expansión de G

- Nodo objetivo alcanzado
- Costo total del camino: g(G) = 7

## Camino Óptimo Encontrado

A -> C -> G

Costo total: 7
```

# Código Base para la Práctica
```
import heapq

class Nodo:
    def __init__(self, nombre, x, y):
        self.nombre = nombre
        self.x = x
        self.y = y
        self.g = float('inf')
        self.h = 0
        self.f = float('inf')
        self.padre = None

    def __lt__(self, otro):
        return self.f < otro.f

def distancia_euclidiana(a, b):
    return ((a.x - b.x) ** 2 + (a.y - b.y) ** 2) ** 0.5

def a_estrella(grafo, inicio, objetivo):
    abiertos = []
    cerrados = set()
    
    inicio.g = 0
    inicio.f = inicio.g + distancia_euclidiana(inicio, objetivo)
    heapq.heappush(abiertos, inicio)
    
    while abiertos:
        actual = heapq.heappop(abiertos)
        
        if actual == objetivo:
            camino = []
            while actual:
                camino.append(actual.nombre)
                actual = actual.padre
            return camino[::-1]
        
        cerrados.add(actual)
        
        for vecino, distancia in grafo[actual].items():
            if vecino in cerrados:
                continue
            
            tentativa_g = actual.g + distancia
            
            if vecino not in abiertos:
                heapq.heappush(abiertos, vecino)
            elif tentativa_g >= vecino.g:
                continue
            
            vecino.padre = actual
            vecino.g = tentativa_g
            vecino.f = vecino.g + distancia_euclidiana(vecino, objetivo)
    
    return None

# Definir nodos y grafo
nodos = {
    'Andares': Nodo('Andares', 0, 0),
    'Galerias': Nodo('Galerias', 1, 2),
    'Midtown': Nodo('Midtown', 3, 1),
    # Agregar más nodos aquí
}

grafo = {
    nodos['Andares']: {nodos['Galerias']: 3, nodos['Midtown']: 4},
    nodos['Galerias']: {nodos['Andares']: 3, nodos['Midtown']: 2},
    nodos['Midtown']: {nodos['Andares']: 4, nodos['Galerias']: 2},
    # Agregar más conexiones aquí
}

# Ejemplo de uso
inicio = nodos['Andares']
objetivo = nodos['Midtown']
ruta = a_estrella(grafo, inicio, objetivo)
print(f"Ruta más corta: {' -> '.join(ruta)}")
```
e
