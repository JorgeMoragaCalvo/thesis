# 3. Análisis y definición de los requisitos

El Product Backlog (PB) representa la lista priorizada de características, mejoras y requisitos técnicos necesarios para la entrega del agente virtual educativo. Los elementos se organizan por prioridad mediante el método MoSCoW (Imprescindible, Debería, Podría, No) y se estiman mediante puntos de historia según su complejidad relativa (ver Tabla \ref{table:backlog}).

| ID   | Característica                              | Prioridad | Puntaje | Sprint |
| ---- | ------------------------------------------- | --------- | ------- | ------ |
| PB01 | Sistema de autenticación de usuarios        | Alta      | 8       | 1      |
| PB02 | Arquitectura de tutoría multiagente         | Alta      | 13      | 1 - 2  |
| PB03 | Agente de investigación de operaciones      | Alta      | 8       | 1      |
| PB04 | Agente de modelado matemático               | Alta      | 8       | 1      |
| PB05 | Agente de programación lineal               | Alta      | 8       | 2      |
| PB06 | Agente de programación entera               | Alta      | 8       | 2      |
| PB07 | Agente de programación no-lineal            | Alta      | 8       | 2      |
| PB08 | Interface conversacional (Streamlit)        | Alta      | 8       | 2      |
| PB09 | Sistema de detección de confusión           | Media     | 5       | 3      |
| PB10 | Generación de explicaciones alternativas    | Media     | 8       | 3      |
| PB11 | Motor de generación de evaluaciones         | Alta      | 13      | 3 - 4  |
| PB12 | Mecanismo de retroalimentación automatizado | Alta      | 8       | 3      |
| PB13 | Implementación nivel de dificultad          | Baja      | 5       | 4      |
| PB14 | Seguimiento del progreso del estudiante     | Alta      | 8       | 4      |
| PB15 | Vista del historial de evaluación           | Media     | 5       | 5      |
| PB16 | Panel de estadísticas de aprendizaje        | Media     | 5       | 5      |
| PB17 | Generación de consejos de aprendizaje       | Baja      | 5       | 6      |
| PB18 | Pruebas de integración de sistemas          | Alta      | 8       | 6      |

## 3.1. Requisitos de usuario (requisitos funcionales)

### Autenticación y gestión de usuarios

**US-01: Registro de usuario**

Como estudiante nuevo, deseo registrar una cuenta con mi nombre, correo electrónico y contraseña para poder acceder a la plataforma de tutorías y realizar un seguimiento de mi progreso de aprendizaje.

Criterios de aceptación:

- El formulario de registro valida el formato del correo electrónico y los requisitos de la contraseña.
- El sistema evita registros duplicados de correo electrónico.
- El campo de confirmación de contraseña coincide con la contraseña original.
- Al registrarse correctamente, se redirige a la pantalla de inicio de sesión con un mensaje de confirmación.

**Inicio de sesión de usuario**
Como estudiante registrado, deseo iniciar sesión con mi correo electrónico y contraseña para acceder a mi entorno de aprendizaje personalizado y a mi historial de conversaciones.

Criterios de aceptación:

- El sistema valida las credenciales con los datos de usuario almacenados.
- El \textit{token JWT} se genera tras la autenticación exitosa.
- La sesión del usuario persiste tras las actualizaciones de la página.
- Las credenciales no válidas muestran los mensajes de error correspondientes.

**US-03: Cierre de sesión**
Como estudiante que ha iniciado sesión, deseo cerrar mi sesión de forma segura para que mi cuenta permanezca protegida al usar dispositivos compartidos.

Criterios de aceptación:

- El botón de cierre de sesión es accesible desde todas las pantallas autenticadas.
- El token de sesión se invalida al cerrar sesión.
- El usuario es redirigido a la pantalla de inicio de sesión después de cerrar sesión.

### Chat del tutor

**US-04: Selección de Temas**
Como estudiante, deseo seleccionar un tema específico de optimización entre los agentes disponibles para recibir tutoría especializada que se ajuste a mis necesidades de aprendizaje.
Criterios de aceptación:

La barra lateral muestra las cinco áreas temáticas: Investigación de Operaciones, Modelado Matemático, Programación Lineal, Programación Entera y Programación No Lineal.
El tema seleccionado se resalta visualmente en la interfaz.
El contexto del agente cambia correctamente al cambiar de tema.

**US-05: Interacción Conversacional**
Como estudiante, quiero formular preguntas en lenguaje natural y recibir respuestas contextualmente relevantes para aprender conceptos de optimización de forma interactiva y conversacional.

Criterios de aceptación:

- La interfaz de chat acepta texto libre.
- Las respuestas incorporan el historial de conversaciones para una continuidad contextual.

**US-06: Detección de Confusión y Explicaciones Alternativas**
Como estudiante con dificultades con un concepto, quiero que el sistema detecte mi confusión y me ofrezca explicaciones alternativas para que pueda comprender temas difíciles mediante diferentes enfoques.

Criterios de aceptación:

- El sistema analiza los mensajes de los estudiantes en busca de indicadores de confusión (palabras clave, repetición de preguntas).
- Las explicaciones alternativas utilizan diferentes enfoques (ejemplos, analogías, desgloses paso a paso).
- El sistema rastrea qué estilos de explicación son más efectivos para cada estudiante.

### Sistema de evaluación

**US-07: Creación de Evaluaciones**
Como estudiante, quiero crear evaluaciones de práctica seleccionando un tema y un nivel de dificultad para evaluar mi comprensión de conceptos específicos de optimización.

Criterios de aceptación:

- La interfaz de creación de evaluaciones permite seleccionar un tema entre cinco disponibles.
- Se pueden seleccionar los niveles de dificultad (principiante, intermedio, avanzado) (no implementado aún).
- Las preguntas generadas se adaptan al contexto del tema y la dificultad seleccionados.
- Las preguntas consideran el historial de conversación y el nivel de conocimientos del estudiante.

**US-08: Envío y retroalimentación de evaluaciones**
Como estudiante, deseo enviar mis respuestas de evaluación y recibir retroalimentación detallada con calificaciones para poder comprender mis errores y mejorar mis conocimientos.

Criterios de aceptación:

- El sistema acepta respuestas de texto libre para cada pregunta.
- La calificación automatizada proporciona puntuaciones en una escala de 1.0 a 7.0.
- La retroalimentación detallada explica qué fue correcto, qué fue incorrecto y cómo mejorar.
- Se proporcionan las respuestas correctas para comparar y aprender.

**US-09: Revisión del historial de evaluaciones**
Como estudiante, quiero revisar mis evaluaciones anteriores filtradas por tema para poder hacer un seguimiento de mi progreso y revisar las áreas que me resultan difíciles.

Criterios de aceptación:

- El historial de evaluaciones muestra todas las evaluaciones completadas con fechas y puntuaciones.
- La función de filtro permite ver las evaluaciones por tema específico (no implementado aún).
- La vista detallada muestra preguntas, respuestas de los estudiantes, comentarios, calificaciones y respuestas correctas.
- Los detalles de la evaluación se pueden expandir y contraer para facilitar la navegación.

### Seguimiento del progreso

**US-10: Dashboard de progreso**
Como estudiante, quiero ver mi panel de progreso de aprendizaje, que muestra mi perfil, niveles de conocimiento y estadísticas, para poder comprender mi estado general de aprendizaje.

Criterios de aceptación:

- El panel muestra el nombre, el correo electrónico y la fecha de registro del estudiante.
- Se muestran indicadores de nivel de conocimiento para cada uno de los cinco temas.
- Las estadísticas de aprendizaje incluyen el total de conversaciones, las evaluaciones completadas y las puntuaciones promedio.
- Se puede acceder al historial de conversaciones recientes.

**US-11: Consejos de aprendizaje personalizados**
Como estudiante, deseo recibir consejos de aprendizaje personalizados según mi rendimiento y actividad, para poder optimizar mi enfoque de estudio.

Criterios de aceptación:

- Los consejos se generan en función del rendimiento en la evaluación y la cobertura del tema.
- Las recomendaciones identifican áreas de mejora.
- Los consejos se muestran en el panel de progreso.

## 3.2. Mapping entre las características del sistema y los requisitos de usuario

## 3.3. Requisitos no funcionales
