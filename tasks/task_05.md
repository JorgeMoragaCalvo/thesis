# Task five
## Task
Esta tarea del capítulo **Verificación y Validación**, proporciona información de cómo se verificaron y validaron los requisitos funcionales y no funcionales.

### 5.1 Descripción Verificación y Validación de Requisitos Funcionales

Describir en detalle el proceso que se realizó (qué se hizo, qué herramientas se usaron, etc.) y cuáles fueron los resultados obtenidos.

Describir las pruebas funcionales que se diseñaron y usaron. Solo describir una prueba funcional en detalle y el resto de las pruebas deben ser colocadas en el Apéndice (al final del documento). Se deben tener al menos 3 pruebas por cada Historia de Usuario.


### 5.2 Descripción Verificación y Validación de Requisitos No Funcionales

En esta sección se debe describir en detalle cómo se verificó y validó cada uno de los requisitos NO funcionales definidos en la Sección 3.3 de este documento. Para verificar y validar cada requisito no funcional se debe describir en detalle el proceso que se realizó (qué se hizo, qué herramientas se usaron, etc.) y cuáles fueron los resultados obtenidos.

#### 5.2.1 Portabilidad

Se deben mostrar los resultados de cargar el sistema en diferentes navegadores (Firefox, Chrome, Edge). Mostrar imágenes de cómo se ve el sistema en los diferentes navegadores.

#### 5.2.2 Usabilidad

Se debe reportar los resultados de haber aplicado el cuestionario SUS a 10 personas del público objetivo del proyecto. Mas detalles de este cuestionario en: [cuestionario] (https://medium.com/thinking-design/the-system-usability-scale-how-its-used-in-ux-b823045270b7)

Indicar en el texto que se usaron 10 usuarios siguiendo la recomendación de Jakob Nielsen quien dice que no es necesario muchos usuarios para este tipo de pruebas. Incluso solo se necesitan 5 usuarios. [Nielsen] (https://www.nngroup.com/articles/why-you-only-need-to-test-with-5-users/)

#### 5.2.3 Autenticación y Autorización
Se debe realizar tres tipos de pruebas. De autenticación (usuario y psw). De Autorización, ingresando con cada tipo de usuario y tratando de acceder a opciones que no le corresponden, y verificando que el sistema no le deje usar la opción.

#### 5.2.4 Corrección matemática de las respuestas

Para probar esto, construir un conjunto entre 30 y 50 ejercicios de Programación Lineal y Programación Entera, cada uno con su solución correcta previamente comprobada. Esta solución puede verificarse usando herramientas como GLPK, PuLP, etc. Luego, se le pide al tutor inteligente que resuelva cada ejercicio y se comparan sus respuestas con las soluciones correctas. Para evaluar su desempeño, se revisa: cuántas veces obtiene el valor óptimo correcto, cuántas veces formula bien el modelo matemático y cuántas veces explica correctamente el método simplex, sin caer en contradicciones. Como criterio de aceptación, se puede establecer que el sistema no debería cometer errores en más del 5% de los casos evaluados.

#### 5.2.5 Consistencia de respuestas entre sesiones independientes

Se debe probar porque los LLM son estocásticos: el mismo problema puede recibir respuestas distintas en distintas sesiones. Se podría proceder así: tomar 10 a 15 problemas representativos y los ejecutas 10 veces cada uno. Luego se revisa si hay contradicciones en los pasos, en las explicaciones, o terminología inconsistente. Como criterio de aceptación se puede calcular un porcentaje de ejecuciones sin contradicciones.

#### 5.2.6 Calidad del andamiaje pedagógico

Se necesita una rúbrica para que un experto (ojalá el docente del curso) evalúe la calidad pedagógica. La rúbrica debería tener al menos 4 criterios: si el tutor guía en lugar de dar la respuesta directa, si la pista es proporcional al error del estudiante si la ayuda progresa ante errores reiterados y si adapta el lenguaje al nivel del problema. Se podría exigir al menos 75% de cumplimiento.
