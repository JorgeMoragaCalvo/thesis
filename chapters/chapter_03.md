# 3. Análisis y definición de los requisitos

Este capítulo presenta el análisis y la definición de requisitos del agente virtual educativo, formalizados según los artefactos propios de la metodología SCRUM adoptada en el proyecto. La especificación parte del Product Backlog, donde se listan y priorizan las características del sistema, y se descompone en historias de usuario que describen el comportamiento esperado desde la perspectiva del estudiante y del administrador. El capítulo se organiza en tres secciones. Primero, se detallan los requisitos funcionales mediante historias de usuario con criterios de aceptación expresados en Gherkin. A continuación, se establece la trazabilidad entre las características del Product Backlog y las historias de usuario asociadas. Por último, se enuncian los requisitos no funcionales que condicionan la arquitectura y la operación de la plataforma.

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

Las historias de usuario (HU) describen las funcionalidades del sistema desde la perspectiva de los actores que lo utilizan: el rol **estudiante** (usuario principal) y el rol **administrador** (gestión de la plataforma). Cada HU se redacta con el formato canónico *Como [rol], quiero [meta] para poder [beneficio]*, incluye sus **Story Points** y **Prioridad**, y define los criterios de aceptación en lenguaje **Gherkin** (`Feature`/`Scenario`/`Given`/`When`/`Then`/`And`).

### 3.1.1. Autenticación y gestión de usuarios

**US-01: Registro de usuario**

Como estudiante nuevo, quiero registrar una cuenta con mi nombre, correo institucional y contraseña, para poder acceder a la plataforma de tutorías y realizar un seguimiento de mi progreso de aprendizaje.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Registro de usuario

  Scenario: Registro exitoso con correo institucional
    Given el estudiante se encuentra en la pantalla de registro
    When ingresa un nombre, un correo con dominio "@usach.cl" y una contraseña que cumple los requisitos
    And confirma la contraseña con el mismo valor
    And envía el formulario
    Then el sistema crea la cuenta del estudiante
    And lo redirige a la pantalla de inicio de sesión
    And muestra un mensaje de confirmación de registro

  Scenario: Correo electrónico ya registrado
    Given existe una cuenta asociada al correo "alumno@usach.cl"
    When el estudiante intenta registrarse con el mismo correo
    Then el sistema rechaza el registro
    And muestra el mensaje "El correo electrónico ya está registrado"

  Scenario: Confirmación de contraseña no coincide
    Given el estudiante completa el formulario de registro
    When el campo de confirmación difiere de la contraseña original
    Then el sistema bloquea el envío del formulario
    And muestra el mensaje "Las contraseñas no coinciden"
```

**US-02: Inicio de sesión**

Como estudiante registrado, quiero iniciar sesión con mi correo electrónico y contraseña, para poder acceder a mi entorno de aprendizaje personalizado y a mi historial de conversaciones.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Inicio de sesión

  Scenario: Autenticación exitosa
    Given el estudiante tiene una cuenta activa
    When ingresa credenciales válidas en el formulario de inicio de sesión
    Then el sistema valida las credenciales
    And genera un token JWT
    And redirige al estudiante a la página principal autenticada

  Scenario: Credenciales inválidas
    Given el estudiante se encuentra en el formulario de inicio de sesión
    When ingresa un correo o contraseña incorrectos
    Then el sistema rechaza la autenticación
    And muestra el mensaje "Credenciales inválidas"

  Scenario: Persistencia de sesión
    Given el estudiante ha iniciado sesión correctamente
    When recarga la página del navegador
    Then la sesión se mantiene activa
    And el estudiante conserva el acceso a su entorno personalizado
```

**US-03: Cierre de sesión**

Como estudiante que ha iniciado sesión, quiero cerrar mi sesión de forma segura, para poder proteger mi cuenta al usar dispositivos compartidos.

| Story Points | Prioridad      |
|--------------|----------------|
| 3            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Cierre de sesión

  Scenario: Cierre de sesión desde una pantalla autenticada
    Given el estudiante tiene una sesión activa
    When pulsa el botón "Cerrar sesión" desde cualquier pantalla autenticada
    Then el sistema invalida el token de sesión
    And lo redirige a la pantalla de inicio de sesión

  Scenario: Acceso a rutas protegidas tras cerrar sesión
    Given el estudiante ha cerrado sesión
    When intenta acceder a una ruta que requiere autenticación
    Then el sistema deniega el acceso
    And lo redirige al formulario de inicio de sesión
```

### 3.1.2. Chat del tutor

**US-04: Selección de tema**

Como estudiante, quiero seleccionar un tema específico de optimización entre los agentes disponibles, para poder recibir tutoría especializada que se ajuste a mis necesidades de aprendizaje.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Selección de tema de tutoría

  Scenario: Visualización de los temas disponibles
    Given el estudiante ha iniciado sesión y se encuentra en la pantalla de chat
    When abre la barra lateral de selección de temas
    Then el sistema muestra los cinco temas: Investigación de Operaciones, Modelado Matemático, Programación Lineal, Programación Entera y Programación No Lineal

  Scenario: Cambio de agente al seleccionar un tema
    Given el estudiante tiene un tema seleccionado actualmente
    When selecciona un tema distinto en la barra lateral
    Then el sistema resalta visualmente el nuevo tema
    And cambia el agente especialista activo al correspondiente al tema seleccionado
    And el contexto de la conversación se ajusta al nuevo agente
```

**US-05: Interacción conversacional**

Como estudiante, quiero formular preguntas en lenguaje natural y recibir respuestas contextualmente relevantes, para poder aprender conceptos de optimización de forma interactiva y conversacional.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Conversación con el tutor

  Scenario: Envío de una pregunta en lenguaje natural
    Given el estudiante tiene seleccionado un tema y un agente activo
    When escribe una pregunta en el campo de chat y la envía
    Then el sistema muestra la pregunta en el hilo de conversación
    And el agente responde con contenido relevante al tema seleccionado

  Scenario: Continuidad contextual
    Given el estudiante ha intercambiado varios mensajes con el agente
    When formula una nueva pregunta que hace referencia a mensajes anteriores
    Then la respuesta del agente incorpora el historial de la conversación
    And mantiene coherencia con las explicaciones previas
```

**US-06: Detección de confusión y explicaciones alternativas**

Como estudiante con dificultades para comprender un concepto, quiero que el sistema detecte mi confusión y me ofrezca explicaciones alternativas, para poder comprender los temas difíciles mediante distintos enfoques.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Detección de confusión y andamiaje pedagógico

  Scenario: Detección de confusión mediante palabras clave
    Given el estudiante mantiene una conversación con el agente
    When envía un mensaje con indicadores de confusión (por ejemplo "no entiendo", "estoy perdido")
    Then el sistema identifica la confusión
    And el agente cambia su estrategia de explicación

  Scenario: Detección por repetición de la misma duda
    Given el estudiante ha preguntado por el mismo concepto en mensajes recientes
    When vuelve a preguntar por el concepto sin haberlo resuelto
    Then el sistema detecta la repetición
    And el agente ofrece una explicación alternativa con un enfoque distinto (ejemplo, analogía o desglose paso a paso)

  Scenario: Seguimiento de la efectividad de cada estrategia
    Given el agente ha aplicado varias estrategias de explicación con el estudiante
    When el estudiante envía retroalimentación o continúa la conversación
    Then el sistema registra qué estrategias resultaron más efectivas para ese estudiante
```

**US-07: Repaso espaciado de conceptos**

Como estudiante, quiero que el sistema me sugiera sesiones de repaso de conceptos previamente estudiados según el algoritmo SM-2, para poder consolidar el aprendizaje a largo plazo y reactivar lo aprendido antes de olvidarlo.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Repaso espaciado (algoritmo SM-2)

  Scenario: Sugerencia de conceptos a repasar
    Given el estudiante tiene conceptos con fecha de repaso vencida según SM-2
    When ingresa a la sesión de tutoría
    Then el sistema le sugiere repasar dichos conceptos antes de avanzar

  Scenario: Actualización del intervalo de repaso
    Given el estudiante completa una sesión de repaso sobre un concepto
    When el agente evalúa la calidad de la respuesta
    Then el sistema actualiza el factor de facilidad y el siguiente intervalo de repaso del concepto según SM-2
    And programa la próxima fecha de repaso
```

### 3.1.3. Sistema de evaluación

**US-08: Creación de evaluaciones**

Como estudiante, quiero crear evaluaciones de práctica seleccionando un tema y un nivel de dificultad, para poder evaluar mi comprensión de conceptos específicos de optimización.

| Story Points | Prioridad      |
|--------------|----------------|
| 13           | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Generación de evaluaciones

  Scenario: Selección de tema y dificultad
    Given el estudiante se encuentra en la pantalla de evaluaciones
    When selecciona un tema de los cinco disponibles
    And selecciona un nivel de dificultad (principiante, intermedio o avanzado)
    And solicita generar la evaluación
    Then el sistema genera un conjunto de preguntas acorde al tema y a la dificultad seleccionados

  Scenario: Adaptación al nivel del estudiante
    Given el estudiante posee un historial de conversaciones y niveles de conocimiento por tema
    When solicita generar una evaluación
    Then las preguntas se adaptan al nivel de conocimiento previo del estudiante
    And consideran el historial conversacional asociado al tema
```

**US-09: Envío y retroalimentación de evaluaciones**

Como estudiante, quiero enviar mis respuestas y recibir retroalimentación detallada junto con una calificación, para poder comprender mis errores y mejorar mi nivel de dominio.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Envío y retroalimentación de evaluaciones

  Scenario: Envío de respuestas en texto libre
    Given el estudiante tiene una evaluación generada y abierta
    When ingresa respuestas en texto libre para cada pregunta
    And envía la evaluación
    Then el sistema acepta las respuestas
    And inicia el proceso de calificación automatizada

  Scenario: Calificación automatizada y retroalimentación
    Given el estudiante ha enviado sus respuestas
    When el sistema completa la calificación
    Then asigna una puntuación en la escala de 1.0 a 7.0
    And entrega retroalimentación que detalla aciertos, errores y sugerencias de mejora
    And muestra las respuestas correctas para que el estudiante las contraste con las suyas
```

**US-10: Revisión del historial de evaluaciones**

Como estudiante, quiero revisar mis evaluaciones anteriores filtradas por tema, para poder hacer un seguimiento de mi progreso y reforzar las áreas en las que tengo dificultades.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Historial de evaluaciones

  Scenario: Listado del historial completo
    Given el estudiante ha completado al menos una evaluación
    When accede a la sección de historial de evaluaciones
    Then el sistema muestra todas las evaluaciones completadas con su fecha y puntuación

  Scenario: Filtrado por tema
    Given el estudiante tiene evaluaciones en distintos temas
    When aplica un filtro por tema específico
    Then el sistema muestra únicamente las evaluaciones correspondientes a ese tema

  Scenario: Vista detallada de una evaluación
    Given el estudiante visualiza el historial
    When expande una evaluación específica
    Then el sistema muestra las preguntas, las respuestas enviadas, la retroalimentación, la calificación y las respuestas correctas
    And permite contraer la vista nuevamente
```

### 3.1.4. Seguimiento del progreso

**US-11: Dashboard de progreso**

Como estudiante, quiero visualizar un panel de progreso con mi perfil, niveles de conocimiento y estadísticas, para poder comprender mi estado general de aprendizaje en la plataforma.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Dashboard de progreso del estudiante

  Scenario: Visualización del perfil del estudiante
    Given el estudiante ha iniciado sesión
    When ingresa al panel de progreso
    Then el sistema muestra su nombre, correo electrónico y fecha de registro

  Scenario: Niveles de conocimiento por tema
    Given el estudiante ha interactuado con uno o más agentes
    When visualiza el panel de progreso
    Then el sistema muestra un indicador de nivel de conocimiento para cada uno de los cinco temas

  Scenario: Estadísticas globales y conversaciones recientes
    Given el estudiante ha generado actividad en la plataforma
    When visualiza el panel de progreso
    Then el sistema muestra el total de conversaciones, las evaluaciones completadas y la puntuación promedio
    And permite acceder al historial de conversaciones recientes
```

**US-12: Seguimiento de competencias por concepto**

Como estudiante, quiero ver el nivel de dominio que tengo en cada concepto del temario (según la taxonomía de Bloom), para poder identificar conceptos específicos en los que debo profundizar.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Seguimiento de competencias por concepto

  Scenario: Visualización de la jerarquía de conceptos
    Given el estudiante accede al panel de competencias
    When selecciona un tema
    Then el sistema muestra la jerarquía de conceptos del tema con su nivel de dominio actual

  Scenario: Actualización del dominio tras una evaluación
    Given el estudiante ha completado una evaluación que cubre ciertos conceptos
    When el sistema procesa la calificación
    Then actualiza el nivel de dominio del estudiante en los conceptos evaluados según la taxonomía de Bloom
```

**US-13: Consejos de aprendizaje personalizados**

Como estudiante, quiero recibir consejos de aprendizaje personalizados según mi rendimiento y actividad, para poder optimizar mi enfoque de estudio.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Podría         |

Criterios de aceptación:

```gherkin
Feature: Consejos de aprendizaje personalizados

  Scenario: Generación de consejos basados en rendimiento
    Given el estudiante tiene un historial de evaluaciones y de cobertura de temas
    When accede al panel de progreso
    Then el sistema muestra consejos generados a partir de su rendimiento en evaluaciones y de los temas que ha trabajado

  Scenario: Identificación de áreas de mejora
    Given el estudiante presenta puntuaciones bajas en uno o más temas
    When se generan los consejos de aprendizaje
    Then las recomendaciones identifican explícitamente esas áreas como prioritarias de mejora
```

### 3.1.5. Administración de la plataforma

**US-14: Gestión de usuarios**

Como administrador, quiero listar, activar y desactivar cuentas de usuario, para poder controlar el acceso a la plataforma y deshabilitar cuentas inadecuadas.

| Story Points | Prioridad      |
|--------------|----------------|
| 8            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Gestión de usuarios por el administrador

  Scenario: Listado de usuarios registrados
    Given el administrador ha iniciado sesión en el panel de administración
    When accede a la pestaña de gestión de usuarios
    Then el sistema muestra todos los usuarios con su nombre, correo, rol y estado (activo/inactivo)

  Scenario: Desactivación de una cuenta
    Given el administrador visualiza el listado de usuarios
    When desactiva la cuenta de un usuario
    Then el sistema marca la cuenta como inactiva
    And el usuario ya no puede iniciar sesión hasta que se reactive

  Scenario: Reactivación de una cuenta
    Given existe un usuario con cuenta desactivada
    When el administrador activa nuevamente la cuenta
    Then el sistema marca la cuenta como activa
    And el usuario recupera el acceso a la plataforma
```

**US-15: Asignación de roles**

Como administrador, quiero asignar el rol de usuario o administrador a las cuentas, para poder delegar funciones de administración cuando sea necesario.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Asignación de roles

  Scenario: Promoción de un usuario a administrador
    Given el administrador visualiza el detalle de un usuario con rol "user"
    When cambia su rol a "admin"
    Then el sistema actualiza el rol del usuario
    And el usuario obtiene acceso al panel de administración en su próximo inicio de sesión

  Scenario: Degradación de un administrador a usuario
    Given existe un usuario con rol "admin"
    When el administrador cambia su rol a "user"
    Then el sistema actualiza el rol del usuario
    And el usuario pierde el acceso a las rutas exclusivas de administración
```

**US-16: Aceptación de dominios de correo externos**

Como administrador, quiero autorizar registros con dominios de correo distintos a `@usach.cl`, para poder incluir a usuarios externos invitados (por ejemplo, docentes colaboradores o estudiantes de otras instituciones).

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Debería        |

Criterios de aceptación:

```gherkin
Feature: Autorización de dominios de correo externos

  Scenario: Solicitud de registro con dominio no autorizado
    Given un usuario externo intenta registrarse con un correo distinto a "@usach.cl"
    When envía el formulario de registro
    Then el sistema crea una solicitud pendiente de aprobación
    And notifica al administrador

  Scenario: Aprobación de un dominio externo por el administrador
    Given existe una solicitud pendiente de un correo con dominio externo
    When el administrador aprueba la solicitud desde el panel de administración
    Then el sistema activa la cuenta del usuario
    And el usuario externo puede iniciar sesión

  Scenario: Rechazo de un dominio externo
    Given existe una solicitud pendiente
    When el administrador rechaza la solicitud
    Then el sistema elimina la solicitud
    And notifica al usuario que su registro no fue autorizado
```

**US-17: Panel de estadísticas del sistema**

Como administrador, quiero ver estadísticas agregadas del sistema (totales de usuarios, conversaciones y evaluaciones), para poder tener una visión general del uso de la plataforma.

| Story Points | Prioridad      |
|--------------|----------------|
| 5            | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Estadísticas del sistema

  Scenario: Visualización de métricas globales
    Given el administrador accede al panel de estadísticas del sistema
    When carga la pestaña correspondiente
    Then el sistema muestra el número total de usuarios, usuarios activos, conversaciones y evaluaciones completadas

  Scenario: Actualización de métricas
    Given el panel de estadísticas está abierto
    When el administrador refresca la vista
    Then el sistema recalcula y muestra los valores actualizados
```

**US-18: Analítica de uso de la plataforma**

Como administrador, quiero consultar métricas de uso (usuarios activos diarios, duración promedio de sesiones, horas pico, popularidad de páginas, popularidad de agentes y engagement), para poder tomar decisiones informadas sobre la evolución de la plataforma.

| Story Points | Prioridad      |
|--------------|----------------|
| 13           | Imprescindible |

Criterios de aceptación:

```gherkin
Feature: Analítica de uso

  Scenario: Usuarios activos diarios (DAU)
    Given el administrador accede a la pestaña de analítica
    When selecciona un rango de días
    Then el sistema muestra la serie temporal de usuarios activos diarios para ese rango

  Scenario: Duración promedio de sesión
    Given el administrador visualiza la analítica
    When consulta la métrica de duración de sesiones
    Then el sistema muestra la duración promedio y la distribución de sesiones en el período seleccionado

  Scenario: Horas pico de uso
    Given el administrador consulta los patrones de uso
    When abre el reporte de horas pico
    Then el sistema muestra una distribución del uso por hora del día y por día de la semana

  Scenario: Popularidad de páginas y agentes
    Given el administrador revisa la analítica
    When abre los reportes de popularidad
    Then el sistema muestra las páginas más visitadas
    And muestra el ranking de agentes/temas más utilizados

  Scenario: Métricas de engagement
    Given el administrador consulta el engagement
    When carga la pestaña correspondiente
    Then el sistema muestra indicadores como tasa de retención, frecuencia de uso y eventos de actividad agregados
```

## 3.2. Mapping entre las características del sistema y los requisitos de usuario

## 3.3. Requisitos no funcionales
