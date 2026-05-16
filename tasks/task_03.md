# Task three

## Análisis y definición de los Requisitos

### Requisitos de usuario (requisitos funcionales)

#### Task 1

Redactar los requisitos (que describen, en una o dos frases, una funcionalidad de software desde el punto de vista del usuario, con el lenguaje que éste emplearía) usando el formato de las **historias de usuario (HU)**. Como rol de [tipo de usuario], quiero [meta u objetivo] (en este campo se explica su intención, no la funcionalidad que usará) para poder [beneficio o resultado] (se trata de un beneficio que va relacionado con la visión del producto) y sus respectivos criterios de aceptación (casos de prueba).

Los **criterios de aceptación** deben ser redactados usando lenguaje Gherkin.

> Ejemplo **Gherking**:
> `Feature`: descripción de alto nivel de una característica del software y agrupar escenarios relacionados.
> `Scenario`: ejemplo que ilustra cómo debería comportarse el software.
> `Given`: estado o contexto inicial antes de que ocurra una acción.
> `When`: describe la acción o el desencadenante que realiza el usuario o el sistema.
> `Then`: el resultado esperado después de la acción.
> `And` / `But`: utilizados para encadenar instrucciones consecutivas sin repetir las palabras clave principales.

Cada **HU** debe tener asociado su respectivos **Story Points** y **Prioridad**.

> NOTE: Completar y mejorar las HU existentes, ¿hacen falta más?. ¿Se deben crear HU para el rol de `admin`? Este rol puede eliminar usuarios, aceptar usuarios de otro dominios de correo diferente a `@usach.cl`, puede ver el rendimiento de los alumnos, métricas referentes a cuáles son los agentes más usados, tiempo promedio de permanencia, uso por días y horas.

### Mapping entre las características del sistema y los requisitos de usuario

#### Task 2

Hacer una tabla donde se haga un _mapping_ entre las características definidas en el [capítulo 1](/chapters/chapter_01.md) y los requisitos de la [sección 3.1](/tasks/task_03.md#requisitos-de-usuario-requisitos-funcionales). Se debe redactar un párrafo introductorio antes de la Tabla. Después de la tabla se debe redactar un párrafo que describa el contenido de la Tabla.

### Requisitos No Funcionales (RNF)

#### Task 3

Redactar textualmente los siguientes requisitos no funcionales, los cuales representan cualidades generales y restricciones que afectan a aplicaciones y sistemas enteros:

- **RNF1 - Portabilidad**: El sistema deberá ser compatible con los navegadores Mozilla Firefox, Google Chrome, Microsoft Edge, asegurando su correcto funcionamiento y visualización.
- **RNF2 - Usabilidad**: El sistema deberá alcanzar una puntuación promedio igual o superior a 75 puntos en el Cuestionario de Usabilidad del Sistema —SUS—, aplicado a usuarios representativos del público objetivo.
- **RNF3 - Autenticación y Autorización**: El sistema deberá implementar mecanismos de autenticación y autorización que garanticen que solo usuarios autenticados accedan a recursos protegidos, restringiendo las operaciones permitidas según el rol asignado a cada usuario.
- **RNF4 - Corrección matemática de las respuestas**: El sistema deberá generar respuestas matemáticamente correctas en problemas de Optimización, evitando errores en la formulación del modelo, la aplicación del método de solución y la interpretación de los resultados.
- **RNF5 - Consistencia de respuestas entre sesiones independientes**: El sistema deberá mantener coherencia en sus respuestas ante una misma consulta ejecutada en sesiones independientes, permitiendo variaciones en la redacción, pero evitando contradicciones en el razonamiento, la formulación matemática o el resultado entregado.
- **RNF6 - Calidad del andamiaje pedagógico**: El sistema deberá proporcionar retroalimentación progresiva y adaptada al desempeño del estudiante, promoviendo el aprendizaje guiado y evitando la entrega directa de soluciones cuando corresponda.
