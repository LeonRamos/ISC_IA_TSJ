# 🔢 Teorema de Pitágoras y Paradigma Simbólico en IA 🤖

GitHub last commit
GitHub stars

## 1. Teorema de Pitágoras y su Campo de Aplicación 📐

El Teorema de Pitágoras establece que en un triángulo rectángulo, el cuadrado de la hipotenusa es igual a la suma de los cuadrados de los otros dos lados[1]. Se expresa matemáticamente como:

$$ a^2 + b^2 = c^2 $$

Donde c es la hipotenusa y a y b son los catetos.

### Campos de Aplicación 🌐

- **Arquitectura y Construcción**: Para calcular distancias y alturas de estructuras[4].
- **Navegación**: En cálculos de rutas y distancias[4].
- **Topografía**: Para medir terrenos y determinar alturas[4].
- **Astronomía**: En el cálculo de distancias espaciales[4].
- **Ingeniería**: En diversos cálculos y diseños estructurales[9].

## 2. Paradigma Simbólico en IA 🧠

### Axioma
En el paradigma simbólico, un axioma es una afirmación fundamental considerada verdadera sin necesidad de demostración[5].

### Teorema
Un teorema es una proposición que se puede demostrar lógicamente a partir de axiomas o teoremas previamente establecidos[5].

### Comprobación
La comprobación en el paradigma simbólico implica el uso de reglas lógicas y deducciones para verificar la validez de una afirmación basándose en los axiomas y teoremas conocidos[5].

## 3. Algoritmo Simbólico para Cálculo de Superficie 🏞️

```
INICIO
  DEFINIR reglas_calculo_superficie
  DEFINIR reglas_comprobacion_garfield
  
  FUNCIÓN calcular_superficie(lado1, lado2, lado3)
    SI es_triangulo_rectangulo(lado1, lado2, lado3) ENTONCES
      area = (lado1 * lado2) / 2
      RETORNAR area
    SINO
      RETORNAR "No es un triángulo rectángulo"
    FIN SI
  FIN FUNCIÓN
  
  FUNCIÓN comprobar_garfield(area_calculada, lado1, lado2, lado3)
    area_garfield = (lado1 + lado2 + lado3) * (lado1 + lado2 - lado3) * 
                    (lado1 - lado2 + lado3) * (-lado1 + lado2 + lado3) / (4 * 16)
    SI area_calculada == area_garfield ENTONCES
      RETORNAR "Comprobación exitosa"
    SINO
      RETORNAR "Error en el cálculo"
    FIN SI
  FIN FUNCIÓN
  
  LEER lado1, lado2, lado3
  area = calcular_superficie(lado1, lado2, lado3)
  resultado_comprobacion = comprobar_garfield(area, lado1, lado2, lado3)
  MOSTRAR area, resultado_comprobacion
FIN
```

## 4. Implementación en Python usando Google Colab 🐍

```python
import math

def es_triangulo_rectangulo(a, b, c):
    lados = sorted([a, b, c])
    return math.isclose(lados[0]**2 + lados[1]**2, lados[2]**2, rel_tol=1e-9)

def calcular_superficie(a, b, c):
    if es_triangulo_rectangulo(a, b, c):
        lados = sorted([a, b, c])
        return (lados[0] * lados[1]) / 2
    else:
        return "No es un triángulo rectángulo"

def comprobar_garfield(area, a, b, c):
    s = (a + b + c) / 2
    area_garfield = math.sqrt(s * (s-a) * (s-b) * (s-c))
    return math.isclose(area, area_garfield, rel_tol=1e-9)

# Ejemplo de uso
lado1, lado2, lado3 = 3, 4, 5
area = calcular_superficie(lado1, lado2, lado3)
comprobacion = comprobar_garfield(area, lado1, lado2, lado3)

print(f"Área calculada: {area}")
print(f"Comprobación Garfield: {'Exitosa' if comprobacion else 'Fallida'}")
```

## 5. Mejoras para un Agente Inteligente 🚀

Para mejorar este programa y convertirlo en un agente inteligente más robusto, los alumnos deberían considerar:

1. **Base de Conocimientos**: Implementar una base de datos de reglas y hechos sobre geometría[5].
2. **Interfaz de Usuario**: Desarrollar una interfaz más amigable para la entrada de datos y visualización de resultados[3].
3. **Manejo de Errores**: Incorporar un sistema robusto de manejo de excepciones y validación de entradas[5].
4. **Aprendizaje**: Implementar un mecanismo para que el agente aprenda de nuevos casos y mejore sus cálculos con el tiempo[5].
5. **Explicaciones**: Añadir la capacidad de explicar el razonamiento detrás de cada cálculo y decisión[5].
6. **Integración con Otros Sistemas**: Permitir la interacción con otros sistemas o bases de datos geométricas[3].

Estas mejoras ayudarán a superar las limitaciones del paradigma simbólico, como la rigidez en el razonamiento y la dificultad para manejar incertidumbre, acercando el sistema a un verdadero agente inteligente[5][2].

Citations:
[1] https://academiacartablanca.es/matematicas/teorema-pitagoras-que-es/
[2] https://www.datacamp.com/es/blog/what-is-symbolic-ai
[3] https://blog.evoacademy.cl/introduccion-a-google-colab/
[4] https://www.clarin.com/viste/puede-aplicar-teorema-pitagoras-ejemplos-vida-real_0_uz78WJLYNP.html
[5] https://iccsi.com.ar/paradigma-simbolico-inteligencia-artificial/
[6] https://planetachatbot.com/como-utilizar-api-chatgpt-para-interaccion-directa-desde-colab-o-databricks/
[7] https://koruro.com/teorema-de-pitagoras
[8] https://cibernetica.wordpress.com/2020/03/17/paradigmas-y-tendencias-en-la-investigacion-de-la-ia/
[9] https://unibetas.com/teorema-de-pitagoras/
[10] https://content.nroc.org/Algebra.HTML5/U07L2T1/TopicText/es/text.html
