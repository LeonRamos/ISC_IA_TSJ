# Ejercicios: El Proceso de Razonamiento Según la Lógica

Con estos ejercicios comprenderas la importancia del razonamiento lógico en el desarrollo de sistemas inteligentes o modelos. Los ejercicios están orientados a reforzar los conceptos de axiomas, teoremas y demostraciones, así como a explorar su relevancia en la inteligencia artificial.

---

## **Ejercicio 1: Creación de un Sistema Axiomático**
**Objetivo:** Comprender cómo los axiomas forman la base de un sistema lógico y su aplicación en sistemas inteligentes.

1. Define un sistema axiomático simple relacionado con un problema cotidiano. Por ejemplo, considera un sistema para determinar si un robot puede moverse en una cuadrícula:
   - Axioma 1: "Un robot puede moverse una casilla hacia adelante si no hay obstáculos."
   - Axioma 2: "Un robot puede girar 90 grados si está en una esquina."
   - Axioma 3: "Un robot no puede retroceder más de dos casillas consecutivas."

2. Con base en estos axiomas, formula dos teoremas que describan posibles movimientos del robot. Por ejemplo:
   - Teorema 1: "Si no hay obstáculos, el robot puede avanzar tres casillas consecutivas."
   - Teorema 2: "El robot puede girar dos veces consecutivas para cambiar de dirección."

3. Este sistema axiomático podría ser implementado en un modelo de inteligencia artificial para controlar el movimiento del robot con un MPC.

## Control Predictivo de Modelos (MPC)

El Control Predictivo de Modelos (MPC) es un modelo de inteligencia artificial avanzado ampliamente utilizado para controlar el movimiento de robots. Este enfoque permite a los robots realizar movimientos dinámicos complejos, mantener el equilibrio y adaptarse a entornos no estructurados.

### Funcionamiento del MPC

1. **Predicción y optimización**: Utiliza un modelo dinámico del robot para simular estados futuros y optimizar las acciones de control.

2. **Proceso iterativo**: Calcula una secuencia de acciones, pero solo ejecuta la primera, repitiendo el proceso en cada paso temporal.

3. **Ajuste en tiempo real**: Actualiza continuamente las predicciones y acciones basándose en retroalimentación en tiempo real, permitiendo que los robots se adapten a entornos cambiantes.

El MPC mejora significativamente las capacidades de robots como Atlas y Spot de Boston Dynamics, permitiéndoles realizar tareas complejas con mayor precisión y adaptabilidad.

## Otros Enfoques de IA para Control de Movimiento

Además del MPC, otros enfoques de IA para el control de movimiento de robots incluyen:

- Redes neuronales para planificación de movimiento en escenarios complicados.
- Aprendizaje por refuerzo para controlar el movimiento del robot.
- Sistemas de control basados en redes neuronales para tareas específicas, como balancear objetos.

Estas técnicas de IA permiten a los robots adaptarse a situaciones imprevistas, optimizar sus movimientos y mejorar su eficiencia en diversas aplicaciones industriales y de investigación.


**Preguntas para reflexionar:**
- ¿Qué tan importante es definir axiomas claros y consistentes al diseñar sistemas inteligentes?
- ¿Cómo pueden los axiomas influir en la capacidad del sistema para resolver problemas complejos?

---

## **Ejercicio 2: Demostración de un Teorema en Lógica Formal**
**Objetivo:** Practicar el proceso de demostración lógica y analizar su importancia en la validación de modelos.

1. Considera el siguiente conjunto de axiomas relacionados con sistemas expertos:
   - Axioma 1: "Si una condición es verdadera, entonces se activa una regla asociada."
   - Axioma 2: "Si una regla se activa, entonces se genera una acción correspondiente."
   - Axioma 3: "Una acción no puede activarse si no hay reglas asociadas activadas."

2. Demuestra el siguiente teorema utilizando los axiomas anteriores:
   - Teorema: "Si una condición es verdadera, entonces se genera al menos una acción."

3. Realiza la demostración paso a paso utilizando razonamiento deductivo.

# Sistema Experto de Diagnóstico de Problemas de Arranque de Automóviles

Este ejemplo de sistema experto utiliza razonamiento deductivo simple para diagnosticar problemas de arranque en automóviles,y demuestra cómo se puede aplicar la lógica formal para resolver problemas cotidianos.

## Reglas del Sistema

1. Si el motor no gira Y las luces no encienden, ENTONCES la batería está muerta.
2. Si el motor gira pero no arranca Y hay olor a gasolina, ENTONCES el motor está ahogado.
3. Si el motor no gira Y las luces encienden, ENTONCES el motor de arranque está fallando.
4. Si el motor gira pero no arranca Y no hay olor a gasolina, ENTONCES falta combustible.

## Demostración del Teorema

Utilizaremos la lógica proposicional para demostrar cómo el sistema llega a una conclusión.

### Símbolos:
- A: El motor no gira
- B: Las luces no encienden
- C: La batería está muerta
- D: El motor gira pero no arranca
- E: Hay olor a gasolina
- F: El motor está ahogado
- G: Las luces encienden
- H: El motor de arranque está fallando
- I: No hay olor a gasolina
- J: Falta combustible

### Reglas en Lógica Formal:
1. A ∧ B → C
2. D ∧ E → F
3. A ∧ G → H
4. D ∧ I → J

### Ejemplo de Deducción:

Supongamos que observamos:
- El motor no gira (A)
- Las luces no encienden (B)

Aplicando la regla 1:
1. A ∧ B (Premisa observada)
2. A ∧ B → C (Regla 1)
3. C (Modus Ponens, 1, 2)

Conclusión: La batería está muerta (C).

## Aplicación en la Vida Real

Este sistema experto podría implementarse como una aplicación móvil para ayudar a conductores a diagnosticar problemas básicos de arranque en sus vehículos. El usuario respondería a preguntas simples sobre el comportamiento del automóvil, y el sistema aplicaría las reglas lógicas para proporcionar un diagnóstico inicial.

La demostración del teorema ilustra cómo el razonamiento deductivo y la lógica formal pueden aplicarse a problemas cotidianos, proporcionando una base sólida para sistemas de diagnóstico automatizados.


**Preguntas para reflexionar:**
- ¿Cómo ayuda el proceso de demostración a garantizar que un modelo lógico funcione correctamente?
- ¿Por qué es importante validar las reglas y teoremas en sistemas inteligentes?

---

## **Ejercicio 3: Aplicación del Razonamiento Lógico en Modelos Predictivos**
**Objetivo:** Identificar cómo el razonamiento lógico se aplica al diseño y mejora de modelos predictivos.

1. Imagina que estás desarrollando un modelo predictivo basado en reglas para predecir si un cliente realizará una compra. Define los siguientes axiomas:
   - Axioma 1: "Si un cliente visita la página del producto más de tres veces, entonces está interesado."
   - Axioma 2: "Si un cliente añade un producto al carrito, entonces tiene intención de compra."
   - Axioma 3: "Si un cliente abandona el carrito sin comprar, entonces necesita un incentivo adicional."

2. Formula dos teoremas basados en estos axiomas. Por ejemplo:
   - Teorema 1: "Si un cliente visita la página del producto más de tres veces y añade el producto al carrito, entonces probablemente realizará una compra."
   - Teorema 2: "Si un cliente abandona el carrito después de añadir un producto, entonces enviarle un descuento puede aumentar las probabilidades de compra."

3. Una posible implementación de este razonamiento lógico podría integrarse en sistemas inteligentes como motores de recomendación o estrategias de marketing automatizadas como se muestra a continuación:

# Estrategia de Marketing Basada en un Modelo Predictivo

Este ejemplo muestra cómo se puede utilizar un modelo predictivo para diseñar una estrategia de marketing efectiva en el sector automotriz, tomando como base datos obtenidos de un sistema experto que diagnostica problemas de arranque en automóviles.

## Contexto

Un taller mecánico quiere aumentar sus ventas de servicios y repuestos relacionados con problemas comunes de arranque en automóviles. Para ello, utiliza los datos generados por el sistema experto descrito anteriormente, que identifica las causas más probables de fallas en el arranque.

### Datos Disponibles

El sistema experto genera diagnósticos basados en las siguientes reglas:

1. Si el motor no gira Y las luces no encienden, ENTONCES la batería está muerta.
2. Si el motor gira pero no arranca Y hay olor a gasolina, ENTONCES el motor está ahogado.
3. Si el motor no gira Y las luces encienden, ENTONCES el motor de arranque está fallando.
4. Si el motor gira pero no arranca Y no hay olor a gasolina, ENTONCES falta combustible.

Estos diagnósticos permiten identificar patrones frecuentes en los problemas de los clientes.

## Estrategia de Marketing

### Objetivo

Aumentar las ventas de baterías, motores de arranque y servicios relacionados mediante campañas dirigidas y personalizadas.

### Aplicación del Modelo Predictivo

El taller utiliza un modelo predictivo para analizar datos históricos y predecir qué servicios o productos serán más demandados según las características del cliente y su vehículo. 

#### Variables del Modelo:
- **Frecuencia de diagnósticos**: ¿Qué problema ocurre con mayor frecuencia? (Ejemplo: baterías descargadas representan el 60% de los casos).
- **Estacionalidad**: ¿En qué épocas del año aumentan ciertos problemas? (Ejemplo: baterías descargadas son más comunes en invierno).
- **Características del cliente**: Edad del vehículo, historial de mantenimiento, etc.

#### Predicción:
El modelo predice que:
1. Durante el invierno, habrá un aumento del 40% en problemas relacionados con baterías descargadas.
2. Los motores de arranque defectuosos son más comunes en vehículos con más de 5 años.
3. Los clientes con vehículos antiguos tienen mayor probabilidad de necesitar revisiones completas.

### Campañas Basadas en las Predicciones

1. **Campaña para baterías**:
   - Envío de correos electrónicos y mensajes SMS a clientes con vehículos mayores a 3 años, ofreciendo descuentos en baterías durante los meses invernales.
   - Publicidad en redes sociales destacando la importancia de revisar la batería antes del invierno.

2. **Campaña para motores de arranque**:
   - Promociones específicas para clientes con vehículos mayores a 5 años.
   - Ofrecer revisiones gratuitas del sistema eléctrico para detectar problemas antes de que ocurran fallas graves.

3. **Campaña general**:
   - Ofrecer paquetes promocionales que incluyan revisión completa del sistema eléctrico y diagnóstico preventivo.

## Ejemplo Práctico

Supongamos que un cliente tiene un automóvil que no arranca y consulta al taller:

1. El sistema experto diagnostica que "la batería está muerta".
2. El cliente recibe una oferta personalizada para reemplazar la batería con un descuento especial.
3. El taller también ofrece una revisión completa del sistema eléctrico como valor agregado.

Gracias al modelo predictivo, el taller ya había anticipado este tipo de problema y preparado inventario suficiente para satisfacer la demanda estacional.

## Beneficios

- **Personalización**: Los clientes reciben ofertas relevantes basadas en sus necesidades reales.
- **Optimización del inventario**: El taller puede anticipar la demanda y evitar faltantes o excesos.
- **Aumento de ventas**: Las campañas dirigidas generan mayor conversión al enfocarse en problemas específicos.

---

Este ejemplo demuestra cómo los modelos predictivos pueden transformar datos técnicos (como diagnósticos automotrices) en estrategias efectivas para aumentar ventas y mejorar la experiencia del cliente.


**Preguntas para reflexionar, se entregan en la actividad:**
- ¿Cómo pueden los axiomas y teoremas mejorar la precisión y efectividad de los modelos predictivos?
- ¿Qué desafíos podrían surgir al intentar implementar este razonamiento lógico en sistemas reales?
