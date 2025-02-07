

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

